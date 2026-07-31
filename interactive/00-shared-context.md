# Algora — Shared Context Block (paste into EVERY Lovable prompt)

> **How to use this file:** every prompt in `batch-01` … `batch-10` starts with the line
> `[PASTE SHARED CONTEXT]`. Replace that line with the **CONTEXT BLOCK** below, then paste the rest.
> Lovable has short memory across long sessions — re-pasting the constraints is what keeps
> screen 30 looking identical to screen 1.

---

## CONTEXT BLOCK (copy from here)

```
PROJECT: "algora" — a gamified platform where CS students master data structures & algorithms
through synchronized visualization, code, and plain-English explanation.
Tagline: "See the algorithm think."

STACK (do not change): Vite + React + TypeScript + Tailwind CSS + shadcn/ui + react-router-dom.
Animation: framer-motion for UI transitions; hand-written SVG (and Canvas only where noted) for
algorithm visuals. State: zustand for engine/playback state, TanStack Query only when a real
backend exists. No Redux, no MUI, no Chakra, no styled-components, no D3 for layout.

DESIGN SYSTEM — LIGHT THEME ONLY (strict):
- paper background #F7F9F8, cards pure white #FFFFFF, hairline borders #E4E9E7
- ink text #0E1513 (headings/body), slate #5B6763 (secondary)
- ONE accent: teal #0E9C86, highlight #14B8A6, tint #E6F5F2
- semantic-only extras: amber #B4791A (warning), rose #C0453E (error) — never decorative
- Fonts: "Instrument Sans" for UI/headings, "JetBrains Mono" for code, stats, chips, field labels
- radius 12–16px, 1px borders, pale-teal focus ring, generous whitespace, WCAG-AA contrast
- FORBIDDEN: dark backgrounds or black panels (the code editor is LIGHT too), purple/violet,
  rainbow gradients, glowing blobs/orbs, glassmorphism, neon, emojis as icons, stock photos of
  people, lorem ipsum. Flat solid colors, crisp edges, soft realistic shadows only.
- Icons: lucide-react, 1.5px stroke, sizes 16/20/24 only.

ALWAYS use CSS variables / Tailwind theme tokens (bg-paper, bg-card, text-ink, text-slate,
text-accent, border-hairline…). Never hardcode a hex value inside a component.

RULES OF ENGAGEMENT for this prompt:
- Change ONLY what this prompt asks for. Do not refactor, rename, restyle or "improve"
  unrelated files. Do not touch the design tokens unless the prompt says so.
- Reuse existing components before creating new ones. Search the repo first.
- Every new file is TypeScript with explicit prop types. No `any`.
- Keyboard + screen-reader accessible: real <button>, aria-labels, visible focus rings,
  and respect `prefers-reduced-motion` on every animation.
- Mobile-first: must not break at 375px width.
- At the end, list the files you created/modified and nothing else.
```

## (copy to here)

---

## Golden rules for driving Lovable on this project

1. **One concern per prompt.** "Build the visualizer" fails. "Build the playback controls bar,
   wired to the existing store, no renderers" succeeds.
2. **Engine before UI.** Batches 3 → 4 exist in that order on purpose. If you let Lovable build
   pretty visualizer screens before the step-engine exists, it will fake the animations with
   `setTimeout` and you will rewrite everything.
3. **Never let it invent data shapes twice.** Types live in `src/engine/types.ts` and
   `src/data/*`. Every later prompt says "import the existing types — do not redefine them."
4. **Lock files.** When a file is finished, add to the prompt:
   `Do NOT modify src/engine/** — it is final.`
5. **Verify before moving on.** Each batch ends with an Acceptance Checklist. Do not start the
   next batch with a red checkbox — errors compound geometrically in AI codegen.
6. **Commit / snapshot after every green batch** so you can roll back one batch, not ten.
7. **When it breaks:** paste the exact error + the file name + "fix only this, change nothing
   else." Do not re-describe the feature; that triggers a rewrite.
8. **Static images stay as reference, not as truth.** Use the generated screenshots from
   `learning-product.md` etc. as the visual target: attach the image to the prompt and say
   "match this layout; the interaction spec below is authoritative where they disagree."

---

## Canonical folder layout (state this whenever Lovable puts a file in the wrong place)

```
src/
  app/            router, providers, layouts (AppShell, MarketingShell)
  components/
    ui/           shadcn primitives (generated, do not restyle by hand)
    common/       Button wrappers, StatCard, Chip, EmptyState, Skeleton…
    viz/          visualization renderers (ArrayView, TreeView, GraphView, GridView, TableView)
    player/       PlaybackBar, StepScrubber, SpeedControl, StepCounter
  engine/         PURE algorithm step generators + types (no React, no DOM)
    algorithms/   bfs.ts, dfs.ts, dijkstra.ts, quicksort.ts, mergeSort.ts, binarySearch.ts…
  stores/         zustand stores (playerStore, progressStore, prefsStore)
  data/           static content: algorithms.ts, lessons.ts, paths.ts, problems.ts, cards.ts
  hooks/
  lib/            utils, formatters, spaced-repetition, xp math
  pages/          one folder per route, matching the 43 + 9 pages in architecture.md
  styles/
```

---

## Route map (from `architecture.md`) — build in this order

| Group | Routes |
|---|---|
| Marketing | `/` `/visualizer` `/paths` `/pricing` `/about` `/contact` `/blog` `/blog/:slug` `/campus` |
| Auth | `/signup` `/login` `/forgot-password` `/reset-password` `/verify-email` |
| Onboarding | `/onboarding/goals` `/onboarding/assessment` `/onboarding/result` |
| Core app | `/app` `/explore` `/algorithms/:slug` `/lessons/:slug` `/practice` `/practice/:slug` `/practice/:slug/results` `/paths/:slug` `/review` `/search` |
| Gamification | `/mastery` `/quests` `/leaderboard` `/achievements` `/streak` |
| Account | `/u/:handle` `/progress` `/settings` `/billing` `/notifications` |
| Support | `/help` `/help/:slug` `/status` `/privacy` `/terms` |
| Roadmap | `/roadmap/new` `/roadmap/:id` `/roadmap/:id/day/:n` |
| Admin | `/admin/login` `/admin` `/admin/students` `/admin/students/:id` `/admin/content` `/admin/billing` `/admin/analytics` `/admin/settings` `/admin/profile` |
