# Batch 07 — Practice: editor, sandboxed runner, results

**Goal:** the student writes code, runs it against real tests, and — the part nobody else does —
gets their *own* execution visualized next to the canonical one.

**Prerequisites:** batches 03, 04, 05.

**Security rule, non-negotiable:** user code never runs on the main thread and never touches
`eval` in app scope. Everything happens in a Web Worker with a hard timeout. Say this in every
prompt in this batch.

---

## Prompt 7.1 — `/practice` list

[PASTE SHARED CONTEXT]

```
Build `/practice` (`src/pages/Practice/`) over src/data/problems.ts + progressStore.problems.

Header stats: solved count, acceptance rate, current solving streak, total attempts — all from
progressStore.
Toolbar: search, difficulty filter, category filter, status filter (All / Unsolved / Attempted /
Solved), "linked algorithm" filter, and a "random unsolved" button. URL-synced.
A responsive table (cards under md): status icon, title, DifficultyBadge, linked algorithm chip
(links to /algorithms/:slug), tags, xp, attempts count, best runtime in mono, and a "Solve" CTA
→ /practice/:slug.
Above the table: a "Recommended for you" row of 3 problems chosen from the user's weakest
categories where the prerequisite algorithm is already watched.
EmptyState for filtered-out results. Solved rows get a subtle accent-tint left border.
```

---

## Prompt 7.2 — Sandboxed runner (do this before the editor UI)

[PASTE SHARED CONTEXT]

```
Build the execution sandbox. No UI in this prompt.

`public/runner.worker.js` (a classic Web Worker, not a module, so it works in all targets):
- Receives { code, tests, entryName, timeLimitMs }.
- Wraps the user's JS in a function constructed inside the worker only, captures console output
  into an array (max 200 lines, 2000 chars each), and calls entryName(...test.input) per test.
- Deep-compares the result to test.expected (order-insensitive only when expected is marked as a
  set — support an `unordered: true` flag on the test).
- Measures per-test duration with performance.now().
- Posts back { results: [{ id, pass, actual, expected, error, ms, logs }], totalMs }.
- Catches syntax errors, thrown errors and stack overflows and reports them as a single
  compile/runtime failure with the message and a cleaned stack (strip worker internals).

`src/lib/runner.ts` — a typed `runTests(code, tests, entryName)` that:
- spawns a fresh worker per run, terminates it after use,
- enforces a 4000ms wall-clock timeout per run (terminate + return a timeout result — this is
  what catches infinite loops),
- serialises concurrent runs (one at a time),
- returns a discriminated union: { kind:'ok', results } | { kind:'compile-error', message } |
  { kind:'timeout' } | { kind:'runtime-error', message, stack }.

Python support: do NOT add Pyodide in this batch. If the selected language is 'py', show
"Python running is coming soon — switch to JS/TS to run tests" and keep the editor fully usable.
TypeScript: strip types with a tiny regex-free approach is unreliable — instead run TS by
transpiling with `sucrase` (add the dependency) inside the worker before execution.

Add vitest coverage for runner.ts using a mocked worker: passing case, failing assertion,
syntax error, and timeout.
```

---

## Prompt 7.3 — Problem workspace

[PASTE SHARED CONTEXT]

```
Build `/practice/:slug` (`src/pages/Problem/`). Two resizable panes on lg+ (shadcn Resizable,
persist the split in prefsStore); stacked tabs under lg.

LEFT — tabs: Description / Hints / Solution / Submissions.
- Description: title, DifficultyBadge, statement blocks, constraints as a mono list, examples in
  bg-tint cards with input/output/explanation, and a "Visualize the approach" link to
  /algorithms/:slug that opens in the split-right pane instead of navigating when possible.
- Hints: progressive reveal — each hint is behind a "Reveal hint 2" button, with a note that
  hints cost no XP but are tracked.
- Solution: locked until the user has either solved it or made 3 attempts (explain the rule
  inline, offer "unlock anyway" which marks the attempt as assisted). Shows the approach, the
  complexity, and the reference code with a copy button.
- Submissions: history from progressStore.problems[slug] — timestamp, verdict, runtime, language,
  and "load this code back into the editor".

RIGHT — the editor:
- CodeMirror 6 (@uiw/react-codemirror) with the javascript/python language packs, a LIGHT theme
  built from our tokens (background #FFFFFF, gutter #F7F9F8, selection tint, teal cursor —
  absolutely no dark theme), line numbers, bracket matching, auto-indent, and Cmd/Ctrl-Enter to run.
- Toolbar: language switcher (persists per problem, seeded from starterCode), Reset to starter
  (with confirm), Copy, Format (prettier-lite via a simple indent pass is fine), font-size
  stepper, and a Run (secondary) + Submit (primary) pair.
- Below: a console panel with tabs Testcases / Output. Testcases lists the visible tests with
  pass/fail chips after a run; the failing one auto-expands showing expected vs actual, diffed
  and monospaced. Hidden tests show only pass/fail counts.
- Autosave the code draft to progressStore.problems[slug].lastCode on every change, debounced 700ms.
- Running state: button spinner, disabled inputs, "Running 3/8 tests" mono line, and a Stop
  button that terminates the worker.

Run = visible tests only. Submit = all tests; on all-pass call markSolved + awardXp, then
navigate to /practice/:slug/results. On failure, stay put and focus the first failing test.
User code must only ever execute in the worker from src/lib/runner.ts.
```

---

## Prompt 7.4 — Results screen

[PASTE SHARED CONTEXT]

```
Build `/practice/:slug/results` (`src/pages/ProblemResults/`).

Accepted state: a large accent check with a restrained scale-in, "Accepted" in t-h1, XP earned
(XpToast style inline), runtime in mono with a percentile bar vs a plausible distribution, the
tests-passed count, attempts taken, and time spent.
Then the payoff section — "How your solution ran": if the problem's linked algorithm has an
engine module, render the canonical FrameView player beside a summary of the user's counters
(comparisons/swaps captured by instrumenting the reference run, not the user's code) and a
one-line verdict such as "Your approach matched the optimal O(n log n) pattern."
Then: complexity self-check (two selects: what do you think your time/space complexity is → shows
the correct answer with an explanation), an "Add to review" button that injects that algorithm's
cards, related problems (3), and CTAs: "Next problem" primary, "Back to practice" ghost.

Failed state (reached via a query flag): a calm, non-punitive panel — which test failed, the
diff, the most relevant hint offered, "try again" primary, and "see a related lesson" secondary.
Never use red as the dominant colour here; use warning tint.

Guard: if there is no submission in progressStore for this slug, redirect to /practice/:slug.
```

---

## Acceptance checklist — Batch 07

- [ ] `while(true){}` in the editor does NOT freeze the page; it times out in ~4s and reports it.
- [ ] A syntax error shows a friendly compile error, not a white screen.
- [ ] `eval(` and `new Function(` appear only inside `public/runner.worker.js`.
- [ ] The editor is light-themed and matches the tokens; no dark surface anywhere.
- [ ] Code draft survives a reload and a language switch keeps per-language drafts separate.
- [ ] Submit → results → back → Submissions tab shows the run.
- [ ] Solution stays locked until 3 attempts or a solve; "unlock anyway" is tracked.
- [ ] Worker is terminated after every run (check the browser task manager for leaks).
- [ ] runner.ts vitest suite passes all four cases.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Code runs on the main thread | `All user code execution must go through the Web Worker in src/lib/runner.ts. Remove every eval/new Function from src/.` |
| Page hangs on infinite loops | `Enforce a 4000ms timeout that terminates the worker and returns { kind:'timeout' }.` |
| Editor renders dark | `Build the CodeMirror theme from our CSS tokens with a white background. Delete the oneDark import.` |
| Deep equality false negatives | `Use a structural deep-compare that handles nested arrays, objects, NaN and -0, plus the unordered flag on tests.` |
| Draft loss on language switch | `Store lastCode per language as Record<'js'|'ts'|'py', string> and restore per language.` |
| Workers accumulate | `Terminate the worker in a finally block and on component unmount.` |
