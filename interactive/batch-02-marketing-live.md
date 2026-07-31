# Batch 02 — Marketing pages become live

**Goal:** every public page works for real — navigation, forms with validation, filtering,
blog routing, and a hero that actually demonstrates the product. Cheap, visible progress that
also forces you to confront the visualizer contract early.

**Prerequisites:** batch 01 complete.

**Note:** the hero demo in 2.2 is deliberately a *scripted* 12-frame teaser, not the real engine.
It must be a self-contained component so batch 04 can swap it for the real player in one prompt.

---

## Prompt 2.1 — Landing page, live

[PASTE SHARED CONTEXT]

```
Rebuild `/` (`src/pages/Landing/`) as composed sections in `src/pages/Landing/sections/`,
keeping the existing visual design from the static version:

Hero — h1 "See the algorithm think.", sub "Watch every comparison, every swap, every visit —
synced to the code and explained in plain English.", primary "Start free" → /signup,
secondary "Try the visualizer" → /visualizer, plus a mono trust line
"12 algorithms · 43 lessons · no credit card". Right side: <HeroDemo /> from prompt 2.2.

Then: LogoStrip (university names as styled mono text, no fake logos) · HowItWorks (3 numbered
steps with icons) · FeatureGrid (6 cards: synchronized code, scrub backwards, run your own input,
spaced repetition, mastery map, streaks & quests) · AlgorithmShowcase (horizontally scrollable
row of 8 real algorithms from src/data/algorithms.ts, each card links to /algorithms/:slug) ·
PathsPreview (4 path cards from src/data/paths.ts) · Testimonials (3, clearly plausible student
quotes, initials avatars — no stock photos) · PricingPreview (2 tiers + link to /pricing) ·
FAQ (6 questions in a shadcn accordion) · FinalCTA.

Interactions: framer-motion whileInView fade+rise 16px, once:true, stagger 0.06, all disabled
under prefers-reduced-motion. Sections use scroll-mt-24 and real ids so nav anchors work.
Every button and card must navigate somewhere real. No dead links.
```

---

## Prompt 2.2 — Hero demo teaser

[PASTE SHARED CONTEXT]

```
Create `src/components/marketing/HeroDemo.tsx` — a self-contained, looping teaser that sells the
core idea in 10 seconds. Isolated on purpose: a later batch will replace its internals with the
real engine, so keep ALL logic inside this one file.

Layout: a bg-card rounded-xl border-hairline shadow-3 panel, ~16:11, containing three regions:
- top-left 60%: an SVG bar array of 9 values animating a bubble-sort pass — compare pair in
  bg-viz-compare, swap animated with framer-motion layout, sorted suffix in bg-viz-found
- top-right 40%: 8 lines of mono pseudocode; the current line has a bg-tint background and a
  3px teal left bar
- bottom strip: one narration sentence that changes with the frame, plus mono counters
  "comparisons 14 · swaps 6"

Drive it from a hardcoded array of 12 frames inside the file, advancing every 1100ms, looping
with a 900ms pause at the end. Pause when the component is off-screen (IntersectionObserver) and
when the tab is hidden. Under prefers-reduced-motion, render frame 6 statically.
Add a small "Try it yourself →" link to /visualizer in the corner.
Purely presentational: no props required, no store, no router state.
```

---

## Prompt 2.3 — Pricing, About, Contact, Campus

[PASTE SHARED CONTEXT]

```
Make these four pages fully functional. Keep the existing static layouts.

/pricing — monthly/yearly toggle (yearly shows "2 months free" and recomputes displayed prices
from one PLANS constant), 3 tiers (Free / Pro / Campus) with real feature lists, a
feature-comparison table (24 rows, Check/Minus icons) collapsible on mobile, and a 5-question
billing FAQ. CTAs: Free → /signup, Pro → /signup?plan=pro, Campus → /contact?topic=campus.

/about — mission, the "why we built this" story, a 4-point principles list, a small
"how it works technically" section that explains the step-log idea in 3 sentences (this is real
differentiation — say it out loud), and a hiring CTA.

/contact — a real form with react-hook-form + zod: name, email, topic select
(General / Sales / Campus / Support / Bug), message (min 20 chars), honeypot field.
Inline field errors, disabled+spinner while submitting, fake 900ms submit, then a success state
that replaces the form. Prefill `topic` from the ?topic= query param. Left column: response-time
expectation, support email, link to /help.

/campus — pitch for departments: outcomes, cohort dashboard screenshot placeholder, 3 pricing
notes, and a lead form reusing the /contact form component with topic locked to Campus.
```

---

## Prompt 2.4 — Blog with routing and filters

[PASTE SHARED CONTEXT]

```
Create `src/data/posts.ts` with 9 posts: slug, title, excerpt, category
('engineering'|'learning'|'product'|'interview'), tags, author {name, role, initials},
publishedAt, readMinutes, and `body` as an array of blocks
({kind:'p'|'h2'|'ul'|'code'|'callout'|'quote', ...}).

/blog — search input (title + excerpt, debounced 200ms), category filter chips, sort by
newest/oldest, one featured post card on top, responsive grid for the rest, "no results"
EmptyState, and URL-synced state via useSearchParams so filters are shareable.

/blog/:slug — max-w-[720px] prose column rendering the block array with our tokens (no
markdown library, no dangerouslySetInnerHTML), sticky table-of-contents from the h2 blocks on
xl+ with scroll-spy, reading-progress bar under the nav, author box, prev/next post links,
3 related posts by shared tags, and a newsletter CTA. Unknown slug → 404 page.
```

---

## Prompt 2.5 — Auth screens (UI + validation only, no backend)

[PASTE SHARED CONTEXT]

```
Make /signup /login /forgot-password /reset-password /verify-email fully interactive with
react-hook-form + zod. No backend — simulate with an 800ms delay.

Shared: `src/pages/auth/AuthLayout.tsx` — centred max-w-[440px] card on bg-paper, wordmark on
top, title + subtitle, form, footer link, and a right-hand marketing panel on lg+ showing one
rotating student outcome stat (bg-tint, no dark panel).

/signup — name, email, password with a live strength meter (length/case/digit/symbol checks
listed as a checklist that ticks as you type), confirm password, terms checkbox. Read ?plan= and
show a "Pro plan selected" chip. On success → /verify-email?email=…
/login — email, password with a show/hide eye toggle, "remember me", forgot-password link.
Simulate a wrong-password error to prove the error state renders. On success → /onboarding/goals.
/forgot-password — email only → success panel "check your inbox" with a resend cooldown timer.
/reset-password — new password + confirm, reads ?token=, invalid-token state.
/verify-email — big mail icon, the email echoed from the query param, a 60s countdown resend
button, "wrong address?" link back to /signup, and a dev-only "Simulate verified" button → /onboarding/goals.

All: proper autoComplete attributes, aria-invalid + aria-describedby on errors, Enter submits,
and no password ever logged to the console.
```

---

## Acceptance checklist — Batch 02

- [ ] Every marketing link and button navigates somewhere real; zero dead `href="#"`.
- [ ] Hero demo loops, pauses off-screen, and is static under reduced-motion.
- [ ] Pricing yearly toggle recomputes from one constant, not two hardcoded lists.
- [ ] Contact form blocks submission on invalid input and shows per-field errors.
- [ ] `/blog?category=engineering&q=graph` restores state on reload.
- [ ] All 5 auth forms validate; success and error states both reachable.
- [ ] Lighthouse accessibility ≥ 95 on `/` and `/pricing`.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Landing became one 900-line file | `Split src/pages/Landing/index.tsx into one component per section under sections/. Behaviour must not change.` |
| Hero demo uses the engine early | `HeroDemo must stay self-contained with hardcoded frames. Remove all imports from src/engine.` |
| Forms use uncontrolled ad-hoc state | `Convert to react-hook-form + zod resolver. Keep the same fields and layout.` |
| Blog renders raw markdown | `Render the typed block array with our own components. No markdown parser, no dangerouslySetInnerHTML.` |
