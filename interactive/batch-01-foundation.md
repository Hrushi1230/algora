# Batch 01 — Foundation: tokens, shells, router, mock data

**Goal:** the static Lovable site becomes a real app skeleton. One source of truth for colour,
type, spacing and data. Nothing visual should look *worse* after this batch — it should look
identical but be driven by tokens.

**Prerequisites:** static site exists in Lovable. Nothing else.

**Do not** build the visualizer, the engine, or any algorithm logic in this batch.

---

## Prompt 1.1 — Design tokens (the single most important prompt in the project)

[PASTE SHARED CONTEXT]

```
Create the single source of truth for the design system. Do this and nothing else.

1. In `src/styles/tokens.css` define CSS custom properties on :root:
   --paper #F7F9F8, --card #FFFFFF, --hairline #E4E9E7,
   --ink #0E1513, --slate #5B6763, --slate-soft #8A9591,
   --accent #0E9C86, --accent-strong #0B7F6D, --highlight #14B8A6, --tint #E6F5F2,
   --warning #B4791A, --warning-tint #FBF3E3, --error #C0453E, --error-tint #FBECEB,
   --radius-sm 8px, --radius 12px, --radius-lg 16px, --radius-xl 24px,
   --shadow-1 0 1px 2px rgba(14,21,19,.05),
   --shadow-2 0 4px 16px -4px rgba(14,21,19,.10),
   --shadow-3 0 12px 32px -8px rgba(14,21,19,.14)
   Also define visualization-state tokens, used later by the algorithm renderers:
   --viz-idle #EEF2F1, --viz-idle-ink #5B6763,
   --viz-active #0E9C86, --viz-active-ink #FFFFFF,
   --viz-visited #B8DED6, --viz-visited-ink #0B4F44,
   --viz-frontier #FFE9BF, --viz-frontier-ink #7A5310,
   --viz-found #14B8A6, --viz-found-ink #FFFFFF,
   --viz-excluded #F1F3F2, --viz-excluded-ink #A7B0AD,
   --viz-compare #C0453E, --viz-compare-ink #FFFFFF,
   --viz-edge #C9D2CF, --viz-edge-active #0E9C86.

2. Map every token into the Tailwind theme in `tailwind.config.ts` so `bg-paper`, `bg-card`,
   `text-ink`, `text-slate`, `bg-tint`, `text-accent`, `border-hairline`, `rounded-lg`,
   `shadow-2`, `bg-viz-active` etc. all work. Extend, do not replace, the default theme.

3. Fonts: load "Instrument Sans" (400/500/600/700) and "JetBrains Mono" (400/500/600) from
   Google Fonts in index.html with preconnect. Set fontFamily.sans -> Instrument Sans and
   fontFamily.mono -> JetBrains Mono. Body text uses leading-relaxed.

4. Type scale utilities in tokens.css using @layer components:
   .t-display (clamp 2.5rem→4rem, 600, tracking-tight, text-balance)
   .t-h1 (2.25rem/600) .t-h2 (1.75rem/600) .t-h3 (1.25rem/600)
   .t-body (1rem/400/leading-relaxed) .t-small (0.875rem) .t-mono-label
   (0.75rem, mono, 500, uppercase, tracking-[0.08em], text-slate)

5. Add `@media (prefers-reduced-motion: reduce)` that reduces all animation and transition
   durations to 0.01ms globally.

6. Set `<html class="bg-paper">` and body `bg-paper text-ink font-sans antialiased`.

Do not modify any page or component in this prompt.
```

**Accept when:** app still renders, and `bg-paper` / `text-accent` / `font-mono` classes work.

---

## Prompt 1.2 — Replace hardcoded colours everywhere

[PASTE SHARED CONTEXT]

```
Refactor every existing page and component to use the Tailwind tokens from `tailwind.config.ts`
instead of hardcoded values. Replace:
- any hex literal, any `bg-white`/`bg-black`/`text-white`/`text-black`,
- any gray-* / zinc-* / neutral-* / slate-* Tailwind palette class,
- any teal-*/emerald-*/green-* numbered class
with the semantic token equivalent (bg-card, bg-paper, text-ink, text-slate, border-hairline,
bg-accent, text-accent, bg-tint…).

Rules: purely mechanical substitution. Do not change layout, spacing, copy, or structure.
If a colour has no sensible token, use the nearest token and list that file in your summary.
Then output the list of any remaining hex literals in the codebase.
```

**Accept when:** the app looks unchanged and a repo search for `#` hex colours returns only
`tokens.css`.

---

## Prompt 1.3 — Common component library

[PASTE SHARED CONTEXT]

```
Create reusable primitives in `src/components/common/`. Each one typed, each one used later by
every screen. No page changes in this prompt.

- `Button.tsx` — variants: primary (bg-accent, white text), secondary (bg-card + border-hairline),
  ghost, danger; sizes sm/md/lg; `loading` prop (spinner, disabled, aria-busy); optional
  leading/trailing lucide icon. Focus ring: ring-2 ring-accent/30 ring-offset-2.
- `Card.tsx` — bg-card, border-hairline, rounded-lg, shadow-1; `interactive` prop adds
  hover:shadow-2 + hover:-translate-y-0.5 transition.
- `Chip.tsx` — small mono uppercase label; tones: neutral / accent / warning / error / success.
- `StatCard.tsx` — mono label, large value, optional delta with ArrowUp/ArrowDown + colour.
- `ProgressBar.tsx` — track bg-viz-idle, fill bg-accent, rounded-full, animated width via
  framer-motion, `showLabel` prop, role="progressbar" with aria-valuenow.
- `RingProgress.tsx` — SVG circle, percent 0-100, size prop, accent stroke, centred mono label.
- `EmptyState.tsx` — lucide icon in a bg-tint circle, title, description, optional action Button.
- `SectionHeader.tsx` — eyebrow (mono label) + title + description + optional right-side action.
- `Skeleton.tsx` — bg-viz-idle shimmer respecting reduced-motion.
- `Tooltip.tsx` — thin wrapper over the shadcn tooltip with our tokens.
- `DifficultyBadge.tsx` — 'easy' | 'medium' | 'hard' → accent / warning / error tones.
- `ComplexityTag.tsx` — renders Big-O in mono inside a bg-tint pill, e.g. O(n log n).

Export all of them from `src/components/common/index.ts`.
```

---

## Prompt 1.4 — Shells and router

[PASTE SHARED CONTEXT]

```
Set up the application skeleton with react-router-dom. Two shells:

1. `src/app/MarketingShell.tsx` — sticky translucent top nav (bg-card/85 + backdrop-blur +
   border-b border-hairline): wordmark "algora" (mono, 600, with a small teal square glyph),
   links Visualizer / Paths / Pricing / Blog / About, then "Log in" ghost + "Start free"
   primary. Mobile: hamburger → full-screen sheet menu. Footer with 4 link columns
   (Product / Learn / Company / Legal) + copyright.

2. `src/app/AppShell.tsx` — fixed left sidebar 264px on lg+, collapsible to 72px icon rail,
   becomes a bottom tab bar under md. Sidebar sections:
   MAIN: Dashboard /app, Explore /explore, Practice /practice, Review /review
   PROGRESS: Mastery /mastery, Quests /quests, Achievements /achievements, Leaderboard /leaderboard
   Bottom: streak flame + day count, XP + level chip, avatar menu (Profile /u/me, Progress,
   Settings, Billing, Log out).
   Top bar inside the shell: page title slot, global search button (Cmd/Ctrl-K, opens nothing
   yet), notifications bell, "Continue learning" primary button.
   Active route: bg-tint + text-accent + a 3px teal left indicator bar.

3. `src/app/router.tsx` — wire EVERY route from the route map with `React.lazy` + a Suspense
   fallback skeleton. Any page that does not exist yet gets a placeholder component that renders
   `<EmptyState title="{Route name}" description="Coming in a later batch." />`. Marketing +
   auth routes use MarketingShell (auth pages: centred, no nav links). App/gamification/account/
   roadmap routes use AppShell. Admin routes use a placeholder AdminShell.
   Add a real 404 page.

4. `src/app/providers.tsx` — Router + TooltipProvider + a Toaster (sonner, top-right, our tokens).

Move existing static pages into `src/pages/<Name>/index.tsx` and keep their markup as-is.
```

**Accept when:** every route in the map loads without a console error, sidebar highlights the
current route, and the layout survives 375px width.

---

## Prompt 1.5 — Mock data + preferences store

[PASTE SHARED CONTEXT]

```
Create the static content layer. These types are permanent — later batches import them and must
never redefine them.

`src/data/types.ts`:
  Category = 'arrays' | 'strings' | 'linked-lists' | 'stacks-queues' | 'trees' | 'heaps' |
             'hashing' | 'graphs' | 'sorting' | 'searching' | 'greedy' | 'dp' |
             'backtracking' | 'bit-manipulation' | 'math'
  Difficulty = 'easy' | 'medium' | 'hard'
  VizKind = 'array' | 'tree' | 'graph' | 'grid' | 'table' | 'linked-list' | 'stack' | 'queue'
  Algorithm { slug; name; category; difficulty; vizKind; oneLiner; summary (2-3 sentences);
    timeBest; timeAvg; timeWorst; space; prerequisites: string[]; tags: string[];
    realWorldUses: string[]; commonMistakes: string[]; estMinutes; xp }
  Lesson { slug; algorithmSlug; title; estMinutes; xp;
    sections: Array<{ id; heading; markdown; visualStep?: number }>;
    quiz: QuizQuestion[] }
  QuizQuestion { id; kind: 'mcq' | 'predict-step' | 'order-steps' | 'true-false';
    prompt; options: string[]; answerIndex: number | number[]; explanation }
  Problem { slug; algorithmSlug; title; difficulty; statementMarkdown; constraints: string[];
    examples: Array<{input;output;explanation?}>; starterCode: Record<'js'|'ts'|'py', string>;
    tests: Array<{ id; input: unknown[]; expected: unknown; hidden: boolean }>;
    hints: string[]; xp }
  Path { slug; title; subtitle; weeks; audience; outcomes: string[];
    modules: Array<{ title; itemSlugs: string[] }> }
  Achievement { id; name; description; icon; tier: 'bronze'|'silver'|'gold'|'platinum';
    xp; criteria }
  Quest { id; title; description; kind:'daily'|'weekly'; target; xp; icon }

`src/data/algorithms.ts` — 24 real algorithms with accurate complexities, spread across
categories. Must include: binary-search, linear-search, bubble-sort, insertion-sort,
selection-sort, merge-sort, quicksort, heap-sort, counting-sort, two-pointers, sliding-window,
stack-basics, queue-basics, linked-list-reversal, bst-insert, bst-traversals, level-order,
heap-insert, hash-table-chaining, bfs, dfs, dijkstra, topological-sort, union-find.
Plus helpers: `getAlgorithm(slug)`, `algorithmsByCategory()`, `CATEGORY_META` (label, lucide
icon name, one-line description for each category).

`src/data/lessons.ts` — 6 full lessons (binary-search, bfs, dfs, quicksort, merge-sort,
dijkstra) with 4-6 real sections of genuinely good teaching prose and 4 quiz questions each.
`src/data/problems.ts` — 10 problems with real statements, examples and tests.
`src/data/paths.ts` — 4 paths: "Interview Sprint" (6 weeks), "CS Fundamentals" (12 weeks),
"Graphs Deep Dive" (4 weeks), "DP from Zero" (5 weeks).
`src/data/achievements.ts` — 24 achievements. `src/data/quests.ts` — 12 quests.
`src/data/user.ts` — one mock user: handle, name, level 7, xp 4820, streak 12, longest 21,
joinedAt, per-category mastery percentages, 30 days of activity history.

`src/stores/prefsStore.ts` — zustand + persist('algora-prefs'): language 'js'|'ts'|'py',
playbackSpeed 1, narrationOn, soundOn, reducedMotion, sidebarCollapsed. Typed setters.

No UI in this prompt. Content quality matters — no lorem ipsum, no placeholder strings.
```

---

## Acceptance checklist — Batch 01

- [ ] Zero hex colours outside `src/styles/tokens.css`.
- [ ] Both fonts load; code/labels are visibly JetBrains Mono.
- [ ] All 52 routes render (placeholder is fine); no console errors.
- [ ] Sidebar collapse works; bottom tab bar appears under md; 375px is clean.
- [ ] `src/components/common/index.ts` exports all 12 primitives.
- [ ] `src/data/algorithms.ts` has 24 entries with real Big-O values.
- [ ] Reduced-motion OS setting visibly stops animation.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Lovable rebuilt pages while doing 1.2 | `Revert all layout/markup changes from the last edit. Reapply ONLY colour-class substitutions.` |
| It invents a dark theme / dark editor | `Remove every dark: variant and dark background. This product is light-only, including the code editor.` |
| Data files are stubs | `Rewrite src/data/algorithms.ts with all 24 entries fully populated. No TODOs, no empty arrays, accurate Big-O.` |
| Router uses nested `<Routes>` chaos | `Flatten to a single route table in src/app/router.tsx using layout routes with <Outlet/>.` |
