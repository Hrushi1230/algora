# Algora — DSA Content Build Order (2026 interview reality)

What to build, in what order, and why. This is the companion to `INTERACTIVE-PLAN.md`
(how to build) and `GROWTH.md` (who it's for).

---

## 1. The shift you must design around

DSA interviews in 2026 are **not** what the textbooks teach.

| Dead / dying | What replaced it |
|---|---|
| "Implement an AVL rotation" | "Recognise this is a sliding window" |
| Memorising 300 problems | Recognising ~15 **patterns** |
| Writing code from scratch | Explaining *why* this approach, and the tradeoff |
| Obscure algorithms (KMP, Floyd–Warshall) | Grid/graph BFS, heaps, intervals, binary-search-on-answer |
| Single-answer puzzles | Multi-part, follow-up-driven ("now make it O(1) space") |

Three forces caused this:

1. **The AI floor.** An LLM writes the code instantly, so interviewers now grade *reasoning
   out loud* and *pattern naming*. This is Algora's exact home turf — a visualizer teaches
   recognition, which is the thing still being tested.
2. **Standardised lists.** Blind 75 / NeetCode 150 / Grind 169 are now the de-facto
   syllabus. Almost every student arrives with one of these lists open. Map your content to
   that taxonomy or you are invisible to them.
3. **Pattern-first hiring.** Companies rotate questions but not patterns. ~15 patterns cover
   ~90% of asked questions.

**Design consequence:** Algora's unit of content is a **pattern**, not an algorithm.
`sliding-window` is a page. `Longest Substring Without Repeating Characters` is an
*instance* inside it.

---

## 2. Two scores, never one

The single biggest content mistake would be ranking topics by one number. Two audiences want
opposite things:

- **I = Interview value** (1–5): how often it decides a real job outcome.
- **T = Traffic value** (1–5): search demand + how badly it needs a *moving* picture.

They diverge hard. Bubble sort is worthless in interviews (I=1) and one of the most-searched
CS terms alive (T=5). Intervals are the reverse (I=5, T=2). You need both kinds:
**high-T topics are the front door, high-I topics are the reason to pay.**

- **V = Visual payoff** (1–5): how impressive the animation is. Drives sharing.
- **R = Renderer** it needs (the real cost driver — see §3).

---

## 3. The ordering rule: batch by RENDERER, not by topic

This is the part most roadmaps get wrong, and it's a 3× cost difference.

A new **renderer** (array-bars, grid, node-link graph, tree, DP table, linked list) is
days of work: layout, transitions, labels, responsive, a11y. A new **algorithm** on an
*existing* renderer is a few hours — it's just a new `Step[]` producer.

So the build order below is grouped so each wave **unlocks one renderer and then drains it
completely** before moving on. Never build "BFS, then quicksort, then DP" — that's three
renderers for three algorithms. Build all 11 array algorithms while the array renderer is
warm in your head.

```
Wave 0  array-bars  → 6 algos   (proof of concept)
Wave 1  array-bars  → +8 algos  (0 new renderers, the money patterns)
Wave 2  grid        → 6 algos
Wave 3  node-link   → 7 algos
Wave 4  tree        → 9 algos
Wave 5  dp-table    → 7 algos
Wave 6  linked-list → 5 algos
Wave 7  mixed/aux   → 8 algos
```

---

## 4. The build order

### Wave 0 — Proof (6 algos, renderer: `array-bars`)

Ship these with batches 3–4. They exist to prove the engine and to seed SEO. Chosen because
they are the *most searched* things in all of DSA **and** the easiest to animate.

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 1 | `bubble-sort` | Sorting | 1 | 5 | 4 |
| 2 | `insertion-sort` | Sorting | 1 | 4 | 4 |
| 3 | `selection-sort` | Sorting | 1 | 4 | 4 |
| 4 | `merge-sort` | Divide & conquer | 3 | 5 | 5 |
| 5 | `quicksort` | Divide & conquer | 3 | 5 | 5 |
| 6 | `binary-search` | Binary search | 5 | 5 | 3 |

> Why start with algorithms that don't matter for interviews? Because `bubble-sort` and
> `binary-search` are the highest-volume DSA searches on earth. Wave 0 buys you *traffic*
> while Wave 1 buys you *revenue*. Also: sorting is the only family where the animation is
> self-explanatory with zero prose, so it validates the engine fastest.

### Wave 1 — The money patterns (8 algos, renderer: `array-bars` reused, 0 new)

Highest interview value per hour of work in the entire product. Nothing new to render.

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 7 | `two-pointers` | Two pointers | 5 | 4 | 4 |
| 8 | `sliding-window-fixed` | Sliding window | 5 | 4 | 5 |
| 9 | `sliding-window-dynamic` | Sliding window | 5 | 3 | 5 |
| 10 | `prefix-sum` | Prefix sum | 4 | 3 | 4 |
| 11 | `kadane` | Greedy / DP | 4 | 3 | 4 |
| 12 | `binary-search-on-answer` | Binary search | 5 | 2 | 3 |
| 13 | `monotonic-stack` | Stack | 4 | 2 | 5 |
| 14 | `merge-intervals` | Intervals | 5 | 3 | 4 |

> `binary-search-on-answer` ("minimise the maximum…") and `monotonic-stack` are the two
> patterns that most separate people who pass from people who fail today, and almost nobody
> teaches them visually. This is your strongest differentiation wedge in the whole catalogue.

### Wave 1B — Strings (8 algos, renderer: `array-cells` — a *mode*, not a new renderer)

A string is a character array. `ArrayView` (batch 4) already auto-switches to labelled cells for
non-numeric values, so this entire wave costs **zero new renderers** — the cheapest 8 algorithms
in the whole plan, and among the highest in both interview and search value. This is the best
value-per-hour block in the catalogue after Wave 1.

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| S1 | `valid-palindrome` | Two pointers | 5 | 5 | 5 |
| S2 | `reverse-string` | Two pointers | 4 | 5 | 5 |
| S3 | `valid-anagram` | Frequency count | 5 | 5 | 4 |
| S4 | `group-anagrams` | Hashing | 5 | 4 | 4 |
| S5 | `longest-substring-no-repeat` | Sliding window | 5 | 5 | 5 |
| S6 | `longest-repeating-char-replacement` | Sliding window | 5 | 3 | 5 |
| S7 | `minimum-window-substring` | Sliding window | 5 | 4 | 5 |
| S8 | `longest-palindromic-substring` | Expand around centre | 4 | 5 | 5 |

Notes that matter for the build:

- **S1/S2 are the single best onboarding animation in the product.** Two pointers walking inward
  over `r-a-c-e-c-a-r` is understandable in three seconds with no prose, in any language. Consider
  using S1 rather than a sort as the landing-page hero demo.
- **S5–S7 reuse Wave 1's sliding-window step producer** with a char frequency map. Build them
  immediately after `sliding-window-dynamic` while that code is still warm — the window
  visual is identical, only the "is the window valid?" predicate changes.
- These need one small aux panel: a **character frequency map** (`aux: 'keyvalue'`, already
  specified in batch 4). No new component.
- S8 is the exception: expand-around-centre needs two pointers moving *outward* from each centre.
  Cheap, but visually distinct — and it's a very high-traffic term.

> Strings were missing from the first draft of this list. That was a mistake: string manipulation
> is one of the top-3 most common interview categories and carries huge search volume
> (`valid palindrome`, `anagram`). Because they ride the array renderer, they should ship in the
> MVP, not later.

### Wave 2 — Grid (6 algos, renderer: `grid`)

The single most-asked *shape* in modern interviews, and the most screenshot-able.

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 15 | `grid-bfs` | BFS | 5 | 4 | 5 |
| 16 | `grid-dfs` | DFS | 5 | 4 | 5 |
| 17 | `number-of-islands` | Flood fill | 5 | 4 | 5 |
| 18 | `flood-fill` | Flood fill | 4 | 4 | 5 |
| 19 | `multi-source-bfs` | BFS | 4 | 2 | 5 |
| 20 | `a-star` | Pathfinding | 2 | 5 | 5 |

> `a-star` has low interview value but enormous traffic and the best animation in the entire
> product. Build it as a growth asset — it's the one most likely to get shared on social.

### Wave 3 — Graphs (7 algos, renderer: `node-link`)

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 21 | `graph-bfs` | BFS | 5 | 5 | 5 |
| 22 | `graph-dfs` | DFS | 5 | 5 | 5 |
| 23 | `topological-sort` | Topo sort | 5 | 3 | 5 |
| 24 | `union-find` | DSU | 4 | 3 | 4 |
| 25 | `dijkstra` | Shortest path | 4 | 5 | 5 |
| 26 | `cycle-detection` | DFS colouring | 4 | 2 | 4 |
| 27 | `course-schedule` | Topo sort | 5 | 3 | 4 |

### Wave 4 — Trees & heaps (9 algos, renderer: `tree`)

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 28 | `tree-dfs-preorder` | Tree DFS | 5 | 5 | 4 |
| 29 | `tree-dfs-inorder` | Tree DFS | 5 | 5 | 4 |
| 30 | `tree-dfs-postorder` | Tree DFS | 4 | 4 | 4 |
| 31 | `level-order-traversal` | Tree BFS | 5 | 4 | 5 |
| 32 | `bst-insert-search` | BST | 4 | 5 | 4 |
| 33 | `lowest-common-ancestor` | Tree DFS | 5 | 3 | 4 |
| 34 | `heapify` | Heap | 4 | 4 | 5 |
| 35 | `top-k-elements` | Heap | 5 | 3 | 4 |
| 36 | `trie-insert-search` | Trie | 3 | 3 | 5 |

> Heap gets a **dual view** (tree + backing array, synchronised). That single feature is
> worth more than five extra algorithms — the array↔tree correspondence is the #1 thing
> students never understand from a book.

### Wave 5 — Dynamic programming (7 algos, renderer: `dp-table`)

DP is where students quit. A filling table with a highlighted recurrence is the highest-value
visualization you can build, so don't rush it — but don't build it before you have retention
(batches 6–8), because DP learners need the review loop.

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 37 | `fibonacci-memo` | 1-D DP | 3 | 5 | 4 |
| 38 | `climbing-stairs` | 1-D DP | 4 | 4 | 4 |
| 39 | `house-robber` | 1-D DP | 4 | 3 | 4 |
| 40 | `coin-change` | 1-D DP | 5 | 4 | 5 |
| 41 | `knapsack-01` | 2-D DP | 4 | 5 | 5 |
| 42 | `longest-common-subsequence` | 2-D DP | 5 | 4 | 5 |
| 43 | `edit-distance` | 2-D DP | 4 | 4 | 5 |

### Wave 6 — Linked lists (5 algos, renderer: `linked-list`)

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 44 | `reverse-linked-list` | Pointers | 5 | 5 | 5 |
| 45 | `fast-slow-pointers` | Cycle detect | 5 | 4 | 5 |
| 46 | `merge-two-lists` | Merge | 4 | 3 | 4 |
| 47 | `remove-nth-node` | Two pointers | 4 | 3 | 4 |
| 48 | `lru-cache` | Design | 4 | 4 | 5 |

### Wave 7 — Completion & long tail (8 algos, mixed/aux renderers)

| # | Slug | Pattern | I | T | V |
|---|---|---|---|---|---|
| 49 | `hashmap-internals` | Hashing | 3 | 5 | 5 |
| 50 | `subsets` | Backtracking | 4 | 3 | 5 |
| 51 | `permutations` | Backtracking | 4 | 4 | 5 |
| 52 | `n-queens` | Backtracking | 3 | 5 | 5 |
| 53 | `word-search` | Backtracking | 4 | 3 | 5 |
| 54 | `bit-manipulation-basics` | Bits | 3 | 4 | 3 |
| 55 | `stack-queue-basics` | Structures | 3 | 5 | 3 |
| 56 | `counting-sort` | Non-comparison | 2 | 4 | 4 |

Backtracking needs a **recursion-tree** renderer — treat it as one new renderer serving five
algorithms, which is why it lands last rather than never.

---

## 5. Deliberately NOT building (and why)

Say no on the record, or scope creep will eat you.

| Skipped | Reason |
|---|---|
| AVL / red-black rotations | Near-zero interview value. High build cost. University-only. |
| KMP / Rabin–Karp | Fascinating, essentially never asked. Phase 3 at best. |
| Bellman–Ford / Floyd–Warshall | Rarely asked; Dijkstra already covers the concept. |
| Segment tree / Fenwick | Competitive programming, not interviews. |
| Radix / bucket / shell sort | Traffic exists but sorting is already over-served by Wave 0. |
| Max-flow, matching | Wrong audience entirely. |

If a skipped topic keeps appearing in your search-console queries, promote it — let data
overrule this table.

---

## 6. Free vs Pro split

Directly from `GROWTH.md`: gate **progress**, never **understanding**.

- **Free & indexed (all 56):** the visualizer, custom input, playback, code, explanation.
- **Pro:** saved progress, the spaced-repetition review queue, the adaptive path, the
  in-browser practice runner, mastery analytics, teacher/cohort tools.

Never put a login in front of an animation. Every one of the 56 pages is a door.

---

## 7. Suggested pace

| Wave | Algos | New renderers | Ship alongside |
|---|---|---|---|
| 0 | 6 | 1 | batches 3–4 |
| 1 | 8 | 0 | batch 5 |
| 2 | 6 | 1 | batch 11 (growth) |
| 3 | 7 | 1 | batch 6 |
| 4 | 9 | 1 | batches 7–8 |
| 5 | 7 | 1 | batch 9 |
| 6 | 5 | 1 | batch 10 |
| 7 | 8 | 2 | post-launch |
| | **56** | **8** | |

**Minimum viable catalogue is Wave 0 + 1 + 2 = 20 algorithms and 2 renderers.** That is
enough to launch publicly, rank, and charge. Don't wait for 56.
