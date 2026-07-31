# Batch 04 — The Visualizer: renderers + synced 3-pane workspace

**Goal:** the flagship screen. Because batch 03 exists, every renderer here is a *pure function
of `step.frame`* — dumb, testable, and reusable by every one of the 12+ algorithms.

**Prerequisites:** batch 03 green. `/dev/engine` must already scrub correctly.

**Hard rule for this whole batch:** renderers receive a frame as a prop. They do not import the
store, do not call the engine, do not own timers, and do not know which algorithm is running.

---

## Prompt 4.1 — Playback controls

[PASTE SHARED CONTEXT]

```
Build `src/components/player/` wired to the existing `src/stores/playerStore.ts`. Do not modify
the store or the engine.

- `PlaybackBar.tsx` — one row, bg-card, border-hairline, rounded-lg, sticky at the bottom of the
  visualizer column: [First] [PrevMilestone] [Prev] [Play/Pause (primary, 44px)] [Next]
  [NextMilestone] [Last] · SpeedControl · StepCounter · loop toggle · reset. Icons from lucide,
  each with an aria-label and a Tooltip showing its keyboard shortcut.
- `StepScrubber.tsx` — an accessible range slider over 0…steps.length-1. Track shows phase
  segments as coloured bands (from usePhaseSegments) and milestone tick marks. Dragging seeks
  live. Hovering shows a tooltip with that step's narration (truncated to 80 chars). Keyboard:
  arrows step, PageUp/Down jump 10. role="slider" with aria-valuetext = the narration.
- `SpeedControl.tsx` — segmented mono control 0.25× 0.5× 1× 1.5× 2× 4×.
- `StepCounter.tsx` — mono "step 14 / 87" plus the phase name as a Chip.
- `CounterStrip.tsx` — animated mono counters from step.counters (comparisons, swaps, visits…),
  each with a tiny label; numbers tween with framer-motion but snap instantly under
  reduced-motion.

Mount `usePlayerKeys()` and `useAutoplay()` once, inside the workspace — never inside a renderer.
```

---

## Prompt 4.2 — Renderers

[PASTE SHARED CONTEXT]

```
Build `src/components/viz/`. Each renderer is a pure presentational component:
`(props: { frame: XFrame; className?: string }) => JSX`. Import frame types from
`src/engine/types.ts` — do not redefine them. Colours come ONLY from the --viz-* tokens.

- `ArrayView.tsx` — responsive SVG. Two modes chosen automatically: bars when all values are
  numeric and length ≥ 12, otherwise labelled cells. Cell fill = state token. Pointers render as
  labelled arrows below the cell with framer-motion `layout` so they glide when the index changes.
  `ranges` render as a bracket + label above. `swapPair` animates a crossing arc; use
  framer-motion layoutId keyed by value so bars physically move rather than recolour.
- `TreeView.tsx` — SVG using node x/y from the frame (already normalised 0-100). Circles sized
  36px, label centred in mono, optional badge in a small pill top-right. Edges as straight lines
  with state colours. Auto-fits via viewBox; never scrolls horizontally on mobile.
- `GraphView.tsx` — same as TreeView plus: arrowheads when directed, weight labels on a small
  white rounded rect at the edge midpoint, `dist` shown under each node in mono
  (∞ when null), and edge state tree/rejected/active colouring.
- `GridView.tsx` — CSS-grid of divs (not SVG) so 30×30 stays fast; cell states via tokens;
  `path` drawn as a teal overlay line using absolute positioning; aspect-ratio preserved.
- `TableView.tsx` — DP-style matrix: sticky row/col labels in mono, cell states, and `active`
  cells scale 1.06 with a ring. Horizontally scrollable with a fade edge indicator.
- `AuxPanels.tsx` — renders `step.aux`: 'stack' as a vertical stack that pushes/pops with
  framer-motion (top item marked), 'queue' as a horizontal list with front/back labels,
  'keyvalue' as a two-column mono table with highlighted rows, 'log' as a scroll-locked list
  auto-scrolled to the last line.
- `FrameView.tsx` — a switch on `frame.kind` that dispatches to the right renderer.

All renderers: `transition={{ duration: 0.35, ease: [0.22,1,0.36,1] }}`, zero animation under
prefers-reduced-motion, and an <svg role="img"> with an aria-label describing the current state
in words. No component here may import a store, the engine registry, or react-router.
```

---

## Prompt 4.3 — The workspace shell

[PASTE SHARED CONTEXT]

```
Build `/algorithms/:slug` (`src/pages/AlgorithmDetail/`) — the flagship screen. Compose only
existing pieces: playerStore, FrameView, AuxPanels, PlaybackBar, StepScrubber, CounterStrip.

Header: breadcrumb Explore / Category / Name · h1 name · DifficultyBadge · category Chip ·
ComplexityTag row (best/avg/worst/space) · estMinutes + xp · actions: "Start lesson"
(→ /lessons/:slug), "Practice" (→ /practice/:slug), bookmark toggle, share button
(copies the URL including input + step).

Body on lg+ is a 3-pane grid, `grid-cols-[minmax(0,1fr)_380px]` with the visual on the left:
- LEFT: FrameView in a bg-card panel with a min-height so it never jumps between steps,
  AuxPanels below it, then CounterStrip, StepScrubber and PlaybackBar pinned at the bottom.
- RIGHT (tabbed, mono tab labels): 
  · Code — language switcher (JS/TS/Py, persisted via prefsStore), line numbers, the current
    codeLine highlighted with bg-tint + a teal left bar and auto-scrolled into view (centred,
    smooth unless reduced-motion), copy button. Light theme — never a dark editor.
  · Explain — the current step's narration in t-h3, `detail` below it, and the previous two
    narrations greyed above so the user has context. Updates on every step.
  · Input — the module's InputField list rendered as real controls, preset buttons, "Run"
    (calls load(slug, values)), "Randomize", inline validation error in an error-tint box.
  · About — summary, real-world uses, common mistakes, prerequisites as links to other
    algorithms, and "when NOT to use this".

Under lg: stack vertically — visual first, then a sticky PlaybackBar above the tab strip.

On mount: load(slug) with the module's first preset. If the slug has no engine module yet, show
an EmptyState "Visualization coming soon" plus the About tab content — do NOT crash.
Deep links: read ?input= (base64 of rawInputs) and ?step= and restore them; update the URL
(replaceState, debounced) as the user changes input or seeks. This link is your growth loop.
```

**Accept when:** you can open `/algorithms/bfs`, press Space, watch the graph, the queue, the
code line and the sentence all move together, then drag the scrubber backwards and everything
rewinds exactly.

---

## Prompt 4.4 — Public `/visualizer` playground

[PASTE SHARED CONTEXT]

```
Build `/visualizer` for logged-out visitors, reusing the exact components from
/algorithms/:slug — do not duplicate them.

Left rail (240px): algorithm picker grouped by category, showing only slugs with an engine
module; search field to filter it. Main: the same workspace. 
Add a compare mode: a "Compare" toggle that splits the main area into two independent players
(two store instances via a `createPlayerStore()` factory — refactor the store to a factory and
keep the existing default instance working) running two algorithms on the SAME input, with a
shared scrubber option and a summary line "quicksort: 41 comparisons · bubble sort: 132".
Free-tier gate: after 3 different algorithms in a session, show a soft, dismissible inline card
"Create a free account to unlock all 12 + save progress" — never a hard modal wall.
```

---

## Prompt 4.5 — Swap the hero teaser for the real thing

[PASTE SHARED CONTEXT]

```
Replace the internals of `src/components/marketing/HeroDemo.tsx` with the real engine: create a
scoped player instance via createPlayerStore(), load 'bubble-sort' with a fixed 9-element input,
autoplay at 1.5×, loop, and render the actual ArrayView + a mini code pane + the narration line.
Keep the outer panel styling byte-identical. Still pause off-screen and on tab blur; still render
a single static frame under prefers-reduced-motion. Delete the hardcoded frame array.
Do not modify any file outside this component.
```

---

## Acceptance checklist — Batch 04

- [ ] All 12 engine algorithms render without a renderer crash (walk them via `/visualizer`).
- [ ] Visual, code line, narration and counters are identical after scrubbing backwards to step 0.
- [ ] Code pane auto-scroll keeps the active line visible in a 400px-tall pane.
- [ ] `/algorithms/dijkstra?step=12` opens on step 12 with the distance table correct.
- [ ] Panel height does not jump between steps (no layout thrash).
- [ ] Keyboard-only operation works end to end; focus never gets trapped.
- [ ] Reduced-motion: everything still usable, nothing animates.
- [ ] No renderer imports a store, the registry, or react-router.
- [ ] 30×30 grid stays above ~50fps while playing.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Renderers read the store directly | `Make every component in src/components/viz purely presentational: frame comes in as a prop. Remove all store imports.` |
| Layout jumps each step | `Give the visualization panel a fixed min-height and reserve space for pointers/labels so content cannot reflow between steps.` |
| Code pane scroll fights the user | `Only auto-scroll when the active line is outside the visible area, and cancel auto-scroll for 2s after a manual scroll.` |
| Bars recolour instead of moving | `Use framer-motion layoutId keyed by the value's identity so swapped elements animate along a path.` |
| Compare mode shares one store | `Refactor playerStore into a createPlayerStore() factory and give each player its own instance via React context.` |
| Mobile SVG overflows | `Use viewBox + preserveAspectRatio and remove fixed pixel widths. Must fit 375px.` |
