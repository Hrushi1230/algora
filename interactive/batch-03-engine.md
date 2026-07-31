# Batch 03 ★ — The Step Engine (this is the company)

**Goal:** a headless, pure-TypeScript library that runs an algorithm once and returns an
immutable list of `Step`s. Zero React. Zero DOM. Zero `setTimeout`. Every visual, code
highlight, narration line and counter in the product later derives from `steps[i]`.

**Prerequisites:** batch 01 (types + tokens), batch 02 optional.

**Why this ordering matters:** if you let an AI build "an animated visualizer" it will animate
with timers and per-algorithm bespoke code. You then cannot scrub backwards, cannot sync code
highlighting, cannot generate quizzes, and every new algorithm is a from-scratch rewrite. Spend
a full session here.

---

## Prompt 3.1 — Types and contract

[PASTE SHARED CONTEXT]

```
Create `src/engine/types.ts` — the permanent contract of the whole product. No implementation.

Frames describe what to draw; a Step bundles a frame with teaching metadata.

export type ArrayFrame = { kind:'array'; values:(number|string)[];
  states: Record<number, CellState>;            // index -> state
  pointers: Array<{ name:string; index:number; color?:'accent'|'warning'|'error' }>;
  ranges: Array<{ from:number; to:number; label?:string; tone?:'tint'|'warning' }>;
  swapPair?: [number, number]; }

export type TreeFrame = { kind:'tree';
  nodes: Array<{ id:string; label:string|number; x:number; y:number; state:CellState;
                 badge?:string }>;
  edges: Array<{ from:string; to:string; state:EdgeState; label?:string }>; }

export type GraphFrame = { kind:'graph'; directed:boolean; weighted:boolean;
  nodes: Array<{ id:string; label:string; x:number; y:number; state:CellState;
                 dist?:number|null; badge?:string }>;
  edges: Array<{ from:string; to:string; weight?:number; state:EdgeState }>; }

export type GridFrame = { kind:'grid'; rows:number; cols:number;
  cells: Array<{ r:number; c:number; state:CellState; label?:string|number }>;
  path?: Array<[number,number]>; }

export type TableFrame = { kind:'table'; title?:string;
  rowLabels:(string|number)[]; colLabels:(string|number)[];
  cells: Array<{ r:number; c:number; value:string|number|null; state:CellState }>; }

export type AuxPanel =
  | { kind:'stack'; label:string; items:Array<{id:string;label:string;state?:CellState}> }
  | { kind:'queue'; label:string; items:Array<{id:string;label:string;state?:CellState}> }
  | { kind:'keyvalue'; label:string; rows:Array<{k:string;v:string;highlight?:boolean}> }
  | { kind:'log'; label:string; lines:string[] };

export type CellState = 'idle'|'active'|'visited'|'frontier'|'found'|'excluded'|'compare'|'sorted';
export type EdgeState = 'idle'|'active'|'tree'|'rejected';

export type Frame = ArrayFrame|TreeFrame|GraphFrame|GridFrame|TableFrame;

export type Step = {
  i: number;                     // index in the step list, filled by the builder
  frame: Frame;
  aux?: AuxPanel[];              // stack / queue / dist table / log beside the main view
  codeLine: number;              // 1-based line in the algorithm's pseudocode
  narration: string;             // ONE plain-English sentence, present tense
  detail?: string;               // optional deeper 1-2 sentences
  phase: string;                 // e.g. 'partition', 'relax-edges' — used for the timeline
  counters: Record<string, number>;  // comparisons, swaps, visits, pushes...
  isMilestone?: boolean;         // scrubber tick marks + quiz anchor points
};

export type AlgorithmRun = {
  slug:string; steps: Step[]; pseudocode: string[];
  codeByLang: Record<'js'|'ts'|'py', string[]>;   // lines aligned to the SAME codeLine numbers
  inputSummary: string; result: string;           // human-readable outcome
  totalCounters: Record<string, number>;
};

export type InputField =
  | { name:string; label:string; kind:'numbers'; default:string; help?:string; max?:number }
  | { name:string; label:string; kind:'number'; default:number; min:number; max:number }
  | { name:string; label:string; kind:'text'; default:string }
  | { name:string; label:string; kind:'select'; default:string; options:string[] }
  | { name:string; label:string; kind:'graph'; default:string; help?:string }
  | { name:string; label:string; kind:'grid'; default:string; help?:string };

export type AlgorithmModule = {
  slug:string;
  inputs: InputField[];
  validate(raw:Record<string,string>): { ok:true; parsed:Record<string,unknown> }
                                     | { ok:false; error:string };
  run(parsed:Record<string,unknown>): AlgorithmRun;
  presets: Array<{ label:string; values:Record<string,string> }>;
};

Also create `src/engine/builder.ts` exporting a `StepBuilder` class used by every algorithm:
  new StepBuilder(pseudocode, codeByLang)
  .emit({ frame, aux?, codeLine, narration, detail?, phase, isMilestone? })  // clones counters
  .bump('comparisons', 1)  // mutates the running counter, applied to subsequent steps
  .finish(inputSummary, result): AlgorithmRun
The builder must DEEP-CLONE every frame on emit so no step can be mutated later, assign `i`
automatically, and carry counters forward cumulatively.

Pure TypeScript only. No React import anywhere in src/engine.
```

---

## Prompt 3.2 — First three algorithms (prove the contract)

[PASTE SHARED CONTEXT]

```
Implement three AlgorithmModules using ONLY the existing StepBuilder and types from
`src/engine/types.ts`. Do not modify types.ts.

1. `src/engine/algorithms/binarySearch.ts` — inputs: sorted numbers list + target.
   Auto-sort input and say so in inputSummary. Steps must show: lo/hi/mid pointers, the
   excluded half greying out each iteration, `found` or the exhausted range at the end.
   Counters: comparisons, iterations. Milestone on every mid computation.
2. `src/engine/algorithms/bubbleSort.ts` — inputs: numbers list.
   Show compare pair, swapPair when swapping, and the growing `sorted` suffix.
   Counters: comparisons, swaps, passes.
3. `src/engine/algorithms/bfs.ts` — inputs: graph as an edge-list text field
   ("A-B, A-C, B-D" and optionally "A-B:4" weights) + start node.
   Include a layered auto-layout so nodes get sensible x/y in a 0-100 coordinate space
   (put it in `src/engine/layout.ts` — BFS-layer layout plus a simple force-free circular
   fallback; reuse later for DFS/Dijkstra). Aux panels: the queue, and a visit-order log.
   Node states: frontier when enqueued, active when dequeued, visited when done.
   Counters: enqueues, dequeues, edgesExamined.

For each module:
- `pseudocode` is 8-16 numbered lines of clean pseudocode.
- `codeByLang` gives real, runnable JS, TS and Python whose line numbers correspond to the SAME
  codeLine values (pad with blank lines if needed so alignment holds).
- Narration is ONE present-tense sentence per step, written for a confused 20-year-old, e.g.
  "Middle value 12 is smaller than 30, so everything to the left can be thrown away."
- `presets`: 3 per algorithm, including one adversarial/worst case.
- `validate` rejects empty input, non-numeric tokens, arrays longer than 40, unknown start node,
  and returns a human-readable error string.

Register them in `src/engine/registry.ts`: `getModule(slug)`, `hasModule(slug)`,
`listModules()`. Registry keys must match the slugs in `src/data/algorithms.ts`.
```

---

## Prompt 3.3 — Player store

[PASTE SHARED CONTEXT]

```
Create `src/stores/playerStore.ts` (zustand). This is the only place playback lives.

State: slug | null, run: AlgorithmRun | null, index: number, isPlaying: boolean,
speed: 0.25|0.5|1|1.5|2|4, loop: boolean, error: string | null, rawInputs: Record<string,string>.

Actions: load(slug, rawInputs?) (calls registry + module.validate + module.run, resets index,
sets error on invalid input), play, pause, toggle, next, prev, seek(i), first, last,
setSpeed, toggleLoop, reset, stepToNextMilestone, stepToPrevMilestone, stepToNextPhase.

Derived selectors exported as hooks: useCurrentStep(), useProgressPercent(), useCounters(),
useCodeLine(), useCanStepForward/Back(), usePhaseSegments() (contiguous phase ranges for the
timeline bar).

Playback loop: a `useAutoplay()` hook in `src/hooks/useAutoplay.ts` driven by
requestAnimationFrame with accumulated time (base 900ms per step ÷ speed) — NOT setInterval.
It must pause on tab blur, stop at the last step (or wrap when loop), and advance zero steps
when `prefers-reduced-motion` is set unless the user explicitly pressed play.

Keyboard hook `src/hooks/usePlayerKeys.ts`: Space play/pause, ArrowRight/Left step,
Shift+Arrow milestone jump, Home/End first/last, 1-4 speed, R reset. Must ignore events when
focus is inside an input, textarea, or contenteditable.

No visual components in this prompt.
```

---

## Prompt 3.4 — Engine self-test page (throwaway, keep it forever)

[PASTE SHARED CONTEXT]

```
Add a dev-only route `/dev/engine` (not linked from any nav) that proves the engine works with
the ugliest possible UI: a slug dropdown, the raw input fields from module.inputs, a Run button,
Prev/Next/Play buttons, "step i of n", and a <pre> dump of JSON.stringify(currentStep, null, 2)
plus the current counters and narration.

Also add `src/engine/__tests__/engine.test.ts` (vitest) asserting:
- binarySearch on [1..15] target 13 finds it and every step's codeLine is within pseudocode range
- bubbleSort output frame values are sorted ascending and swaps counter > 0
- bfs visit order from A on "A-B,A-C,B-D,C-D" is A,B,C,D
- for all three: steps.length > 3, every step has non-empty narration, counters never decrease,
  and mutating steps[0].frame does not affect steps[1] (deep-clone guarantee)
```

**Accept when:** `/dev/engine` lets you scrub all three algorithms and the JSON changes
coherently at every step. This page stays in the repo as your regression harness.

---

## Prompt 3.5 — Nine more algorithms (same pattern, no new concepts)

[PASTE SHARED CONTEXT]

```
Do NOT modify src/engine/types.ts, builder.ts, registry.ts structure, or playerStore.ts — they
are final. Add nine modules following the exact pattern of the existing three, then register them:

1. insertionSort, 2. selectionSort  (array frames, sorted-prefix highlighting)
3. mergeSort   — table frame or array frame with `ranges` showing sub-arrays merging;
                 aux 'log' panel of merges; phase names 'split' / 'merge'
4. quicksort   — pivot as a pointer, partition ranges, phases 'choose-pivot'/'partition'/'recurse'
5. heapSort    — TreeFrame for the heap PLUS the backing array frame in an aux keyvalue panel
6. dfs         — graph frame, aux 'stack' panel, edge states tree/rejected, phases enter/backtrack
7. dijkstra    — graph frame with `dist` on each node, aux keyvalue distance table + priority
                 queue panel, edge relaxation highlighted, phase 'relax-edges'
8. topologicalSort — graph frame with in-degree badges, aux queue, phase 'peel'
9. slidingWindow   — array frame with a moving `ranges` window, aux keyvalue of window sum/max

Each needs: 8-16 pseudocode lines, aligned js/ts/py code, one-sentence narration per step,
3 presets including a worst case, strict validate(), and accurate counters.
Add one vitest per algorithm asserting a known-correct result.
```

---

## Acceptance checklist — Batch 03

- [ ] `src/engine/**` contains no `import React`, no `setTimeout`, no `window`.
- [ ] 12 modules registered; `listModules()` slugs all exist in `src/data/algorithms.ts`.
- [ ] Every step: `codeLine` ≥ 1 and ≤ pseudocode length; `narration` non-empty.
- [ ] Scrubbing to step 0 after reaching the end gives byte-identical frame JSON.
- [ ] `codeByLang` line counts are aligned across js/ts/py for the same codeLine.
- [ ] All vitest tests pass.
- [ ] Invalid input shows a friendly error instead of a crash.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Animation "works" but can't go backwards | `Steps must be precomputed and immutable. Remove all timer-driven mutation from the algorithm modules; the store may only change the index.` |
| Frames share object references | `Deep-clone the frame inside StepBuilder.emit so mutating one step cannot affect another. Add a test proving it.` |
| Code highlight is off by one | `codeByLang lines must be 1-based and index-aligned with pseudocode. Pad shorter languages with blank lines so the same codeLine points at the equivalent statement.` |
| Narration reads like a log | `Rewrite every narration string as one plain-English present-tense sentence a beginner would understand. No variable dumps, no "i++".` |
| It adds React to the engine | `src/engine must be framework-free. Move any hook or component out to src/components or src/hooks.` |
