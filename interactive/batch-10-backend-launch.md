# Batch 10 — Backend, admin, hardening, launch

**Goal:** replace persisted-localStorage with a real backend without rewriting the UI, then ship.
This is last because the client data contract is now frozen — the schema simply mirrors the stores
you already built.

**Prerequisites:** batches 01–09 all green.

**Choose your backend.** Lovable's native integration is Supabase, so these prompts assume
Supabase (Postgres + Auth + RLS). If you later move to Vercel + Neon, the schema below transfers
almost unchanged — keep all data access behind `src/services/*` so the swap is a one-file change.

---

## Prompt 10.1 — Schema and RLS

[PASTE SHARED CONTEXT]

```
Connect Supabase and create the schema. Mirror the existing zustand stores exactly — do not
invent new field names.

Tables (all with `user_id uuid references auth.users on delete cascade`, `created_at`, `updated_at`):
- profiles (id = auth.users.id, handle unique citext, name, bio, avatar_color, plan text default
  'free', created_at) — handle uniqueness enforced by a unique index
- user_stats (user_id pk, xp int, level int, streak_current int, streak_longest int,
  last_active_date date, freezes_left int)
- algorithm_progress (user_id, slug, status, steps_watched, lesson_done, quiz_score,
  mastery_pct, last_seen_at, pk(user_id, slug))
- lesson_progress (user_id, slug, section_index, completed_at, quiz_score, pk(user_id, slug))
- problem_progress (user_id, slug, attempts, solved_at, best_runtime_ms, last_code jsonb,
  pk(user_id, slug))
- review_cards (user_id, card_id, ease numeric, interval_days int, due_date date, reps int,
  lapses int, pk(user_id, card_id)) + index on (user_id, due_date)
- quests (user_id, quest_id, period_key, progress int, claimed_at, pk(user_id, quest_id, period_key))
- achievements (user_id, achievement_id, progress int, unlocked_at, pk(user_id, achievement_id))
- activity (user_id, day date, xp int, minutes int, steps int, solved int, pk(user_id, day))
- roadmaps (id uuid pk, user_id, title, goal, weeks, days jsonb, is_active bool, created_at)
- bookmarks (user_id, slug, pk(user_id, slug))
- xp_events (id uuid pk, user_id, amount int, reason text, idempotency_key text, created_at,
  unique(user_id, idempotency_key))  -- this table is what makes XP non-duplicable
- notifications (id uuid pk, user_id, kind, title, body, read_at, created_at)
- contact_messages (id uuid pk, name, email, topic, message, created_at)  -- insert-only
- waitlist (id uuid pk, email unique, created_at)

Enable RLS on EVERY table. Policies: authenticated users may select/insert/update/delete only
rows where user_id = auth.uid(). profiles: select is public (for /u/:handle) but update is
self-only. contact_messages and waitlist: insert allowed for anon, select denied to everyone.
No table may be readable without a policy — verify by querying as anon.

Add a Postgres function `award_xp(p_amount int, p_reason text, p_key text)` that inserts into
xp_events with ON CONFLICT DO NOTHING, and only when a row was inserted updates user_stats.xp and
recomputes level. Server-side idempotency beats client-side discipline.
Add a `handle_new_user` trigger that creates profiles + user_stats rows on signup.
```

---

## Prompt 10.2 — Real auth

[PASTE SHARED CONTEXT]

```
Wire the existing auth screens from batch 02 to Supabase Auth. Email + password only — no OAuth,
no magic links, unless explicitly added later.

- `src/services/auth.ts`: signUp, signIn, signOut, requestPasswordReset, updatePassword,
  resendVerification, getSession, onAuthStateChange. Map every Supabase error code to a friendly
  message ("that email is already registered — log in instead").
- `src/app/AuthProvider.tsx`: holds session + profile, exposes useAuth(), shows a full-page
  branded loader on the initial session check only.
- `<RequireAuth>` route wrapper for all /app, /explore, /practice, /review, gamification, account
  and roadmap routes: redirects to /login?next=<path> and returns there after login.
- Redirect logged-in users away from /login and /signup to /app.
- `<RequireOnboarded>` for /app: if profiles has no completed onboarding flag, redirect to
  /onboarding/goals.
- Email verification: real Supabase flow; /verify-email polls the session every 5s and advances
  automatically once verified. Remove the dev-only "simulate verified" button.
- Do not change the visual design of any auth screen in this prompt.
```

---

## Prompt 10.3 — Sync layer

[PASTE SHARED CONTEXT]

```
Make progress persist to the server without touching a single UI component.

1. Add TanStack Query. Create `src/services/progress.ts` with typed fetchers and mutators for each
   table, shaped to the EXACT store field names.
2. Refactor `progressStore` into a hybrid: keep the same public action names and selector hooks
   (components must not change) but have each mutation (a) update local state optimistically and
   (b) enqueue a server write. Add an outbox in `src/lib/outbox.ts` — a persisted queue with
   exponential-backoff retry, flushed on reconnect and on visibilitychange. Offline use must keep
   working; that is the whole point.
3. On login: hydrate stores from the server; if local anonymous progress exists, show a one-time
   "merge your guest progress?" dialog and merge with a last-write-wins-by-timestamp rule per row,
   taking the MAX for monotonic fields (xp, streak_longest, steps_watched).
4. All XP goes through the `award_xp` RPC with a deterministic idempotency key
   (`${kind}:${slug}:${dayOrEventId}`).
5. `src/services/waitlist.ts` + `contact.ts` for the public forms; wire the batch-02 forms to them.
6. Add error boundaries per route group and a toast on any failed sync that offers "retry now".
7. Do NOT put user code execution or algorithm logic on the server — the engine stays client-side.
```

---

## Prompt 10.4 — Admin console

[PASTE SHARED CONTEXT]

```
Build the admin area behind a role check (`profiles.role = 'admin'`, enforced by an RLS policy AND
a route guard; add admin-read policies for the tables it needs). Use the AdminShell placeholder
from batch 01: left nav, denser spacing, same tokens, mono-heavy tables.

/admin/login — separate login form, generic error messages, no signup link.
/admin — KPI row (total users, weekly active, lessons completed, problems solved, MRR placeholder),
a signups-over-time chart, a funnel (signup → onboarded → first lesson → first solve → day-7
return), and a recent-activity feed.
/admin/students — paginated, server-side searchable table (handle, email, plan, level, xp, streak,
last active) with sort, plan filter, CSV export, and row click → detail.
/admin/students/:id — profile summary, mastery breakdown, activity heatmap, submissions list,
and admin actions (grant plan, reset progress, send notification) each behind a confirm dialog and
written to an `admin_audit` table (add it).
/admin/content — tables for algorithms, lessons, problems, cards showing coverage gaps
("6 algorithms have no lesson", "3 have no engine module"), each row linking to the public page.
Read-only in this batch — content stays in code.
/admin/billing — subscriptions table, MRR/churn placeholders clearly labelled as beta.
/admin/analytics — retention cohort grid (weekly cohorts × 8 weeks, tint→accent intensity),
funnel breakdown, top algorithms by views, drop-off step ("users abandon quicksort at step 14" —
compute from a new `step_events` aggregate table, sampled 1-in-10 client-side).
/admin/settings — feature flags (stored in a `flags` table, read by the client at boot),
maintenance banner text, and a "recompute mastery for all users" job button.
/admin/profile — the admin's own account.
Every mutating action requires a confirm dialog and writes an audit row.
```

---

## Prompt 10.5 — Hardening and launch

[PASTE SHARED CONTEXT]

```
Final pass. No new features.

SECURITY
- Verify RLS by attempting a cross-user read from the browser console and confirming it fails;
  list any table that responded.
- Ensure only the anon/publishable Supabase key is in the client bundle; no service key anywhere.
- Add rate limiting on contact/waitlist inserts (a Postgres trigger capping N per email per hour).
- Sanitise every user-supplied string rendered anywhere (handles, bio, roadmap titles). No
  dangerouslySetInnerHTML in the codebase — confirm with a search.
- Add security headers via the host config: X-Content-Type-Options nosniff,
  Referrer-Policy strict-origin-when-cross-origin, X-Frame-Options SAMEORIGIN,
  Permissions-Policy camera=(), microphone=(), geolocation=(), and a
  Content-Security-Policy-Report-Only listing the Supabase and Google Fonts origins in connect-src
  and font-src. Report-only first — do not enforce CSP on launch day.

PERFORMANCE
- Route-level code splitting verified; CodeMirror, recharts and the worker must be in separate
  chunks loaded on demand. Report the bundle sizes.
- Lighthouse ≥ 90 performance and 100 accessibility on /, /pricing, /algorithms/bfs, /app.
- Preload both fonts with font-display: swap; no layout shift from font loading (CLS < 0.05).
- Memoize renderers with React.memo keyed on the frame reference; confirm 60fps at 4× on Dijkstra.

QUALITY
- Zero TypeScript errors with strict:true and noUncheckedIndexedAccess; zero `any`.
- Global ErrorBoundary with a branded "something broke" page offering reload + a copyable error id.
- 404 and offline pages on-brand.
- Full keyboard pass: every interactive element reachable, visible focus, no traps, one skip-link.
- Screen-reader pass on /algorithms/bfs: the visualization must announce state changes via a
  polite aria-live region carrying the narration text.
- Empty, loading and error states on every data-driven screen — no bare spinners.

LAUNCH
- SEO: per-route title/description via a <Seo> component, Open Graph + Twitter cards, a generated
  1200×630 OG image for the landing page and per-algorithm OG images using ShareCard's canvas,
  sitemap.xml, robots.txt, and JSON-LD (Course schema for paths, SoftwareApplication for the app).
- Analytics: a thin `src/lib/analytics.ts` wrapper with a no-op default and named events
  (signup_completed, lesson_completed, problem_solved, review_session_completed,
  visualizer_played, share_clicked). Never log PII or code contents.
- Add README with setup, env vars, architecture (explain the step-engine contract — future you
  will thank you), and the batch history.
```

---

## Acceptance checklist — Batch 10

- [ ] Signing in on a second browser shows identical XP, streak, mastery and review schedule.
- [ ] Going offline mid-session, doing work, then reconnecting flushes the outbox with no loss.
- [ ] Replaying the same XP event twice awards once (xp_events unique index proves it).
- [ ] A cross-user read attempt from the console fails on every table.
- [ ] Guest → signup merge keeps the higher values and never loses solved problems.
- [ ] Admin routes are unreachable for a non-admin, both by URL and by API.
- [ ] Lighthouse targets met on all four audited routes.
- [ ] `strict: true` build passes with zero errors and zero `any`.
- [ ] Screen reader announces each step's narration on `/algorithms/bfs`.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Components rewritten during the sync refactor | `Keep progressStore's public API identical. Only its internals may change. Revert component edits.` |
| RLS left off a table | `Enable RLS and add owner-only policies on <table>. Then prove an anon select returns zero rows.` |
| XP duplicates on retry | `Route all XP through the award_xp RPC with a deterministic idempotency key and rely on the unique index.` |
| Service key in the client | `Remove it immediately, rotate the key, and move that call into a Postgres function or edge function.` |
| Offline writes lost | `Persist the outbox to localStorage and flush on 'online' and visibilitychange with exponential backoff.` |
| CSP breaks the live site | `Switch to Content-Security-Policy-Report-Only, collect violations, then enforce.` |

---

## After launch — the growth loop to build first

1. **Step permalinks** (`/algorithms/bfs?input=…&step=7`) shared into study groups and Discord —
   already supported by batch 04. Add per-link OG images so they preview beautifully.
2. **Embeddable visualizer** (`<iframe src="/embed/bfs">`) for professors' slides and blog posts.
   Free distribution into exactly your audience.
3. **AI "explain this step"** grounded strictly in `steps[i]` — low hallucination risk because the
   model receives the actual state, not a guess.
4. **Content scale-up** to 60+ algorithms via the registry; each new one is a single engine file
   and inherits every renderer, quiz generator and review card type for free.
