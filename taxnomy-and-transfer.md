# Taxonomy & Transfer — Why Overlap Is Correct, and How To Stop It Confusing Students

Answers one question: sliding window lives on both arrays **and** strings; recursion powers sorting, trees, backtracking **and** DP — does that overlap confuse students, or is it the best design?

**Short answer: the overlap is correct and unavoidable. It is not the source of confusion. The source of confusion is putting nouns and verbs in the same flat list.**

Companion to `content.md`, `concept-page-spec.md`, `content-research.md`.

Tags: `[RESEARCH]` published education research · `[DERIVED]` logical consequence of our design · `[ESTIMATE]` our judgement, must be validated with learner data.

---

# 1. Where the confusion actually comes from

Every popular list mixes two incompatible kinds of thing in one sidebar:

| Category in a typical list | What kind of thing is it? |
|---|---|
| Arrays & Hashing | a **container** (noun) |
| Two Pointers | a **movement** (verb) |
| Sliding Window | a **movement** (verb) |
| Stack | a **container** (noun) |
| Binary Search | a **movement** (verb) |
| Linked List | a **container** (noun) |
| Trees | a **container** (noun) |
| Backtracking | a **movement** (verb) |
| Graphs | a **container** (noun) |
| 1-D DP / 2-D DP | a **movement** (verb) |
| Greedy | a **movement** (verb) |
| Intervals | a **data shape** (noun-ish) |

A student reading that sidebar reasonably concludes these are 12 parallel, mutually exclusive buckets. Then reality breaks the model:

- Sliding window appears on arrays *and* strings → "so is it an array topic or a string topic?"
- Longest Substring Without Repeating Characters needs string + hash map + sliding window → "which bucket was this?"
- Merge sort, tree DFS, subsets, and memoised DP all use recursion → "I finished recursion already, why is it back?"

**The bug is the taxonomy, not the overlap.** Verbs are *supposed* to apply to many nouns. That is what makes them worth learning. `[DERIVED]`

---

# 2. The fix: three layers, two axes

## 2.1 Layer 0 — Machinery (taught once, referenced forever)

Not topics. The physics everything else runs on.

| Machinery concept | Where it later reappears |
|---|---|
| Invariant (a statement true at every step) | sliding window, two pointers, binary search, heaps, DP |
| Call stack & recursion | sorting, tree traversal, backtracking, DP, graph DFS |
| Recurrence → tree of calls → cost | divide & conquer, DP, backtracking |
| Amortised cost | dynamic array, hash map, monotonic stack |
| Index arithmetic & half-open ranges `[lo, hi)` | every array/string technique, binary search |
| State = the minimum you must remember | DP, BFS layers, backtracking, greedy |

**Recursion belongs here, not in a topic list.** `[DERIVED]` Recursion is not a subject a student "completes" — it is the engine later subjects are built from. So it gets one canonical home with a call-stack visualization, and every later use links back to it with an explicit banner: *"This is recursion again — the stack is doing X here."*

## 2.2 Layer 1 & 2 — the two axes

- **Axis N (Structures / nouns):** array, string, hash map, hash set, stack, queue, deque, linked list, heap, tree, BST, trie, graph, union-find, matrix, interval set, bitmask.
- **Axis V (Techniques / verbs):** two pointers, sliding window, prefix sum, binary search on index, binary search on answer, fast/slow pointers, sorting-then-scanning, monotonic stack/deque, hash counting, recursion/divide & conquer, backtracking, BFS, DFS, topological order, greedy exchange, memoisation, tabulation, bit tricks, heap selection, in-place reversal.

**A problem is a cell, not a category.** `Container × Movement`.

| Problem | Structure (N) | Technique (V) |
|---|---|---|
| Maximum Sum Subarray of Size K | array of ints | sliding window (fixed) |
| Longest Substring Without Repeating Characters | string + hash map | sliding window (variable) |
| Minimum Window Substring | string + 2 hash maps | sliding window (variable + need-count) |
| Max Consecutive Ones III | array of 0/1 | sliding window (variable + budget) |
| Sliding Window Maximum | array + deque | sliding window + monotonic deque |

All five are **one technique**. Only the container and the "what makes the window valid" change.

## 2.3 Layer 3 — Compositions

Named multi-concept skills that are genuinely their own thing: *k-th largest via heap*, *cycle detection in a graph*, *LRU cache (hash map + doubly linked list)*, *word search on a grid (DFS + backtracking)*, *course schedule (graph + topo sort)*.

---

# 3. The rule that removes the confusion

> **One canonical home per concept. Everywhere else is an explicitly labelled visit, never a re-teach.**

Concretely: `[DERIVED]`

1. **Sliding window is taught once**, on the most concrete substrate: an array of integers with a fixed window. Numbers are easier to hold than characters, and fixed is easier than variable.
2. Strings, budgets, need-counts, and deques then arrive as **transfer episodes** inside that same concept, each opening with the same banner:

   > **Same technique, new container.** The invariant hasn't changed: *everything between `lo` and `hi` satisfies the window condition.* Only "what makes it valid" changed — last time it was window size, this time it's no repeated characters.

3. **Never** create a separate "Sliding Window on Strings" concept. That is what teaches students the two things are different. There is one concept with 4–5 substrates.
4. Every transfer episode must state the invariant **in the same words** as the original. Constant deep structure + varying surface features is precisely what produces transfer; identical surface features produce surface-bound learning that fails on a new container. `[RESEARCH]`

## Why this is strictly better than a flat list

| Flat mixed list | Two-axis model |
|---|---|
| "Sliding window" and "strings" look like rival buckets | Sliding window is a verb; string is a noun it acts on |
| Recursion appears "finished", then keeps returning unexplained | Recursion is Layer 0 machinery, expected to return |
| ~150 problems feel like ~150 special cases | ~17 nouns × ~20 verbs, of which only ~60 cells are real problems `[ESTIMATE]` |
| Learner memorises "string problems use sliding window" | Learner learns *when the invariant applies*, container-independent |
| Practising one container only → fails on the other | Deliberate multi-container practice per technique |

---

# 4. Avoiding the opposite failure: combinatorial explosion

17 nouns × 20 verbs = 340 cells. Do **not** author 340 pages.

Rules: `[DERIVED]`

- A **cell becomes a transfer episode** only if it changes the invariant, the bookkeeping, or the complexity. `sliding window × string` qualifies (needs a frequency map). `sliding window × list-of-floats` does not (identical logic).
- Cap: **3–5 substrates per technique** `[ESTIMATE]`. More is repetition, not transfer.
- Each substrate must be justified in one line in the authoring file, or it gets cut in review.

### Worked example — the whole Sliding Window concept

| Slot | Substrate | Why it earns its place |
|---|---|---|
| Canonical teach | int array, fixed size | simplest possible invariant |
| Transfer 1 | int array, variable size | invariant becomes a condition, not a length |
| Transfer 2 | string + hash map | bookkeeping becomes a frequency map |
| Transfer 3 | 0/1 array with a flip budget | condition becomes a resource constraint |
| Transfer 4 (advanced) | array + monotonic deque | window must also answer "max inside me" |
| Discriminate | vs two pointers, vs prefix sum | nearest neighbours that look identical |

One concept. Six pages. Zero duplicate teaching.

### Worked example — Recursion (Layer 0)

| Slot | Where it appears | Banner shown |
|---|---|---|
| Canonical teach | pure call-stack visualization, factorial → array sum | "this is the machine" |
| Instance | merge sort / quick sort | "recursion splits the input" |
| Instance | tree DFS | "the structure is already recursive" |
| Instance | subsets / permutations | "recursion + undo = backtracking" |
| Instance | memoised DP | "recursion + a cache = DP" |
| Contrast | iterative equivalents | "same work, explicit stack" |

Students stop asking "why is recursion back?" because the page states upfront that it will be back, and lists where. `[DERIVED]`

### DP is a verb too

"1-D DP" and "2-D DP" are not two topics — they are the same verb over different **state shapes**. The teachable skill is *state design*: what is the minimum you must remember, and what does one dimension of the table mean? Substrates: 1-D over an array index, 2-D over two sequences (string pair), 2-D over a grid, state + capacity (knapsack). Same verb, four containers. `[DERIVED]`

---

# 5. Product surface: naming, URLs, navigation

To make the two axes visible rather than something the student has to infer: `[DERIVED]`

```
/machinery/recursion              ← Layer 0, canonical
/machinery/invariants
/structure/array                  ← Layer 1, container
/structure/hash-map
/technique/sliding-window         ← Layer 2, canonical teach
/technique/sliding-window/string-substrate     ← transfer episode
/composition/lru-cache            ← Layer 3
/problem/longest-substring-no-repeat           ← tagged: [string, hash-map] × [sliding-window]
```

Every problem page shows two chip rows, never one:

```
Container:  [ string ]  [ hash map ]
Movement:   [ sliding window ]
Machinery:  [ invariant ]
```

Sidebar is grouped under three headers — **Machinery**, **Structures**, **Techniques** — so nouns and verbs are never siblings.

Practice and interview modes **hide the Movement row** until the student commits to an approach, otherwise the tag is the answer. `[DERIVED]`

---

# 6. Making sure students actually feel the connection

| Mechanism | What the student sees |
|---|---|
| **Transfer banner** | "Same technique, new container" + the unchanged invariant, verbatim |
| **Invariant diff** | Side-by-side: what stayed identical vs the one line that changed |
| **Reverse question** | "You've seen sliding window on arrays and strings. Name a container where it would *not* work, and why." (answer: unsorted data where validity isn't monotonic) |
| **Selection drill** | 6 unlabeled problems, student only picks the verb + names the invariant — no coding |
| **Machinery callback** | On merge sort: "Recursion, again. Open the call-stack view you learned in Layer 0." |
| **Concept map** | Live bipartite graph: verbs on one side, nouns on the other, lit edges = cells the student has actually solved. Makes gaps visible: "you've only ever run sliding window on arrays." |

That last one is the anti-confusion device *and* the anti-grinding device: the student sees a technique is only truly known when several edges from it are lit.

---

# 7. How this changes the mastery rule

`content.md` requires 3 Compose passes with 3 different partner concepts. Add one axis-aware condition: `[DERIVED]`

> A **technique** cannot reach mastery until it has been passed on **at least 2 different containers**, one of which was not the container it was taught on.

So sliding window mastered only on integer arrays stays "learning", regardless of streak or problem count. This directly prevents the exact failure your question implies — a student who thinks sliding window *is* a string topic.

Measure it: **transfer gap** = accuracy on the taught container − accuracy on an unseen container. Target < 15 points. `[ESTIMATE]` If wider, the transfer episodes are too surface-similar and the invariant framing needs rewriting.

---

# 8. Verdict

| Question | Answer |
|---|---|
| Does sliding window spanning arrays and strings confuse students? | Only if you present containers and techniques as one flat list. |
| Is the overlap a flaw? | No — it is the entire value of a technique. A verb that applies to one noun is a trick, not a skill. |
| Is recursion appearing in sorting, trees, backtracking, and DP a problem? | No, provided recursion is Layer 0 machinery with one canonical home and explicit callbacks, not a topic that gets "completed". |
| So is this the best structure? | Two axes + a machinery layer + one canonical home per concept + explicit transfer episodes. Yes — and it is also fewer pages than the flat model. |

**One line for the team:** *nouns hold data, verbs move through it, machinery makes verbs possible — teach each thing exactly once, and make every reappearance say out loud that it is a reappearance.*
