# DSA Content Architecture v2 — Braided Curriculum and Evidence-Tagged Content Spec

> **What changed from v1, and why**
>
> Two defects were fixed.
>
> 1. **Guessing presented as research.** v1 stated invented numbers — the 150-anchor allocation, week counts, "15–20 high-frequency patterns" — in the same confident voice as genuinely established learning-science findings. v2 tags every claim with an evidence class and replaces invented numbers with a **measurement method** plus a calibration gate.
> 2. **One-concept-at-a-time progression.** v1 was a ladder: finish arrays, then linked lists, then trees. That produces students who can only solve a problem when told which topic it belongs to — the exact failure mode interviews and real work punish. v2 replaces the ladder with a **braided curriculum** in which a learner is always holding three or more concepts in play at once.

---

## Evidence tagging — read this before trusting any number

Every substantive claim carries one of four tags. Nothing untagged should be quoted externally.

| Tag | Meaning | How to treat it |
|---|---|---|
| `[VERIFIED]` | Confirmed against a primary or well-corroborated public source, listed in Section 16. | Safe to build on and to quote. |
| `[RESEARCH]` | Established finding in learning science, with effect sizes where available. | Safe to build on. Cite the literature, not this document. |
| `[DERIVED]` | A logical consequence of a `[VERIFIED]` or `[RESEARCH]` item, reasoned explicitly here. | Safe to build on. State the reasoning when challenged. |
| `[ESTIMATE]` | Professional judgment with no data behind it yet. Each one names the experiment that would replace it. | **Never quote as a finding.** Must be replaced by measurement before it drives a roadmap or a pitch. |

**Standing rule:** an `[ESTIMATE]` may ship into a prototype. It may not ship into a public promise, an investor deck, or a learner-facing commitment such as "master DSA in 16 weeks."

---

# 1. The core decision: concept-wise or question-wise?

## The answer is neither, in a specific way

Concept-first with question-proven mastery — **but the unit of scheduling is not the concept**. This is the substantive correction to v1.

- **Concepts** are the knowledge graph. They define what exists and what depends on what.
- **Questions** are the evidence. A concept is not learned because a lesson was read; it is learned because it was applied under conditions that could have exposed a gap.
- **Sessions** are the schedulable unit, and a session is always **mixed**. A learner never spends a whole session inside one concept.

### Why not pure concept-wise

`[RESEARCH]` Blocked practice — all of topic A, then all of topic B — reliably produces higher *in-session* performance and weaker *later discrimination*. Interleaved practice, where items from different categories are mixed, improves category discrimination and inductive learning. A meta-analysis of interleaving reports an overall moderate effect of roughly Hedges' g ≈ 0.42, driven by the *discriminative-contrast* mechanism: mixing forces the learner to compare categories and notice what distinguishes them.

`[DERIVED]` Interview and on-the-job problems arrive **unlabeled**. The hard skill is not executing sliding window; it is recognizing that this problem is sliding window and not two pointers. Blocked, concept-wise study systematically fails to train that skill, because the chapter heading gives away the answer.

### Why not pure question-wise

`[RESEARCH]` The same literature reports the boundary condition honestly: **blocking is superior when categories are highly variable internally**, because the learner's first job is to find what the category's members share. Interleaving helps when the challenge is telling similar categories apart; blocking helps when the challenge is seeing a category's underlying commonality.

`[DERIVED]` So the correct schedule is not "interleave everything." It is:

- **Block on introduction.** First exposure to a new concept is concentrated, so the learner can extract the invariant.
- **Interleave on consolidation.** Once the invariant exists, all further practice is mixed with prior concepts and delivered unlabeled.

This one rule is the backbone of everything below.

---

# 2. The braided curriculum

## The failure mode being designed out

A linear roadmap creates four predictable problems. `[DERIVED]`

1. **Label leakage.** The learner solves problems correctly inside a topic and collapses on a mixed set.
2. **Decay behind the cursor.** Arrays finished in week 2 have measurably rotted by week 9, and a linear plan has no mechanism to detect it.
3. **Single-point stalling.** Dynamic programming becomes a wall. Because progress is one-dimensional, hitting the wall stops all progress — the dominant abandonment moment.
4. **Boredom by monotony.** Eleven consecutive tree problems is the same activity eleven times. Novelty, not difficulty, is what collapses first.

## The structure: three rails advanced in parallel

Instead of one sequence, the curriculum runs **three rails simultaneously**, so a stall on one rail never ends a session.

| Rail | Contains | Function |
|---|---|---|
| **Rail S — Structures** | arrays, strings, linked lists, stacks, queues, hash maps, trees, BSTs, heaps, graphs, tries, union-find, range structures | *What data looks like.* "Where does this live, and what does it cost?" |
| **Rail T — Techniques** | two pointers, sliding window, prefix sums, binary search on answer, recursion, backtracking, sorting-as-preprocessing, sweep line, greedy exchange, DP formulation, bit tricks | *How to move through data.* "What is the manoeuvre?" |
| **Rail E — Engineering & analysis** | complexity reasoning, invariants, edge-case enumeration, test design, tracing, debugging, reviewing AI-written code, trade-off articulation | *How to be trusted.* "Is this actually correct, and can you defend it?" |

`[DERIVED]` The rails are not arbitrary. Structures and techniques are genuinely semi-independent: sliding window can be taught on arrays and later reapplied to strings and hash-map-backed windows; binary search generalizes from sorted arrays to answer spaces to BST navigation. Chaining them into one line invents false prerequisites. Rail E runs from day one because it is the rail current hiring signals actually reward — and the rail every competitor bolts on last.

## The session unit: a Braid

Every session has four slots, in this order.

| Slot | Share | Content | Purpose |
|---|---|---|---|
| **1. Focus** | ~40% | One new concept, taught blocked, with synchronized visualization + code + plain-English views | Extract the invariant. Blocking is correct here. `[RESEARCH]` |
| **2. Return** | ~20% | 2–3 items from earlier concepts, scheduled by spacing, **unlabeled** | Retrieval practice against decay. `[RESEARCH]` |
| **3. Discriminate** | ~20% | A contrast pair: two superficially similar problems whose correct approaches differ | Trains the discriminative-contrast mechanism directly. `[RESEARCH]` |
| **4. Compose** | ~20% | One problem requiring the new concept **plus** at least one older concept | Forces integration; stops concepts being stored as isolated islands. |

`[ESTIMATE]` The 40/20/20/20 split is judgment, not data. **Experiment to replace it:** three arms (60/13/13/13, 40/20/20/20, 25/25/25/25) on a matched cohort, measuring delayed unlabeled-transfer score at 14 days. Adopt the winner. Do not publish the split as a recommendation until this runs.

## The rule that answers "students must not sit on one concept"

Three hard constraints, enforced by the scheduler rather than by author discipline. `[DERIVED]`

1. **No session is monochrome.** Every session touches at least three distinct concepts across at least two rails. If the queue cannot satisfy that, the session is regenerated, not shipped.
2. **No concept closes.** Finishing a module moves a concept from *Focus* to *Return*, never to *Done*. Top mastery is reached only after the concept succeeds in at least three **later** Compose problems, spaced across at least three weeks.
3. **A stall never blocks the map.** After two failed gate attempts, the concept stays in Focus rotation at reduced share while a different rail advances in the same session. The learner always leaves with progress. This is the specific defence against the DP abandonment cliff.

## What a braided week looks like

`[ESTIMATE]` — illustrative shape, not a validated schedule.

| Session | Focus (new) | Return (spaced, unlabeled) | Discriminate (contrast pair) | Compose (multi-concept) |
|---|---|---|---|---|
| 1 | Hash map fundamentals (S) | complexity of array ops; two-pointer trace | hash set vs sorting for duplicates | dedupe, then two-pointer scan |
| 2 | Sliding window, fixed size (T) | hash collisions; string indexing | fixed window vs whole-array scan | fixed window over a hash-counted string |
| 3 | Test design for off-by-one (E) | sliding-window invariant recall | correct vs almost-correct window bounds | write failing tests for a given solution |
| 4 | Sliding window, variable size (T) | hash map; array prefix reasoning | variable window vs two pointers | longest substring with constrained counts |
| 5 | Review braid — no new concept | everything above, mixed and unlabeled | three-way contrast set | one integration mission + one AI-code review |

Note what never happens: there is no "hash map day." By session 2 the learner carries three concepts; by session 5 they choose between approaches without being told which applies.

---

# 3. Verified facts about the lists students currently use

This replaces v1's vibes-level competitive analysis with what is actually confirmable — and is explicit about what remains unmeasured.

## Blind 75

- `[VERIFIED]` A static set of 75 problems organized into roughly ten core topics.
- `[VERIFIED]` Approximate distribution: arrays ≈ 9–10, strings ≈ 8–10, trees ≈ 11–14, graphs ≈ 6–8, dynamic programming ≈ 11; the remainder spreads across linked lists, intervals, matrix, heap, and binary manipulation.
- `[VERIFIED]` Its selection thesis is breadth of high-frequency *patterns* rather than volume.
- `[DERIVED]` Two consequences: trees plus DP are roughly a third of the list, and there is no built-in mechanism for spacing, contrast, or unlabeled retrieval. It is a checklist, and checklists get consumed blocked.

## NeetCode 150

- `[VERIFIED]` An ordered roadmap of 18 categories: Arrays & Hashing → Two Pointers → Sliding Window → Stack → Binary Search → Linked List → Trees → Tries → Heap → Backtracking → Graphs → Advanced Graphs → 1-D DP → 2-D DP → Greedy → Intervals → Math & Geometry → Bit Manipulation.
- `[VERIFIED]` Its stated guidance is easiest-to-hardest **within** each category, to reinforce pattern recognition.
- `[DERIVED]` That is textbook blocked practice with the category label permanently visible. It is genuinely good for invariant extraction and structurally unable to train unlabeled selection. That gap is a real product opportunity, not a rhetorical one.

## LeetCode 75

- `[VERIFIED]` An official curated 75-problem plan presented as a 14-week structure.
- `[VERIFIED]` Organized by structure and pattern, with binary tree split explicitly into DFS and BFS sub-groups, BST separate, graphs split into DFS/BFS, and DP split into 1-D and multidimensional; also covers two pointers, sliding window, stack, queue, linked list, heap/priority queue, and backtracking.
- `[DERIVED]` The DFS/BFS split is a real pedagogical signal: the authors treat traversal *strategy* as a first-class concept separate from the *structure*. That independently validates the Rail S / Rail T separation.

## Grind 75, Striver-style sheets, pattern courses, university courses

- `[VERIFIED]` Grind 75 is a configurable generator: the learner sets available weeks and hours and receives a schedule — a real advance over a static list.
- `[ESTIMATE]` Everything else v1 asserted about these — precise counts, per-topic distributions, spaced-repetition behavior, specific weaknesses — was never verified. **Do not cite v1's claims here.**
- **Required work (Section 15, W1):** build the problem-level overlap matrix. Until then the honest statement is: "these lists overlap substantially on a common core and diverge in the tail; we have not yet measured by how much."

## What the comparison licenses us to claim today

`[DERIVED]` Three claims are defensible right now:

1. Every major list is **blocked and labeled**. None systematically trains unlabeled approach selection.
2. Every major list is a **checklist of problems**, not a model of a learner. None represents what the learner currently knows, so none can schedule spacing, contrast, or targeted remediation.
3. None treats **explanation, test design, debugging, or reviewing generated code** as assessed skills, despite that being where hiring signal is moving.

Those three are the product wedge, and none of them requires an invented statistic to be true.

---

# 4. The concept inventory (Rail S / Rail T / Rail E)

Complete A-to-Z coverage. Tier: **C** = core for every learner, **X** = extended, **P** = specialist.

## Rail S — Structures

| Concept | Tier | Built from | Contrasts with | Unlocks |
|---|---|---|---|---|
| Memory, references, mutation | C | — | value semantics | everything |
| Static & dynamic arrays, amortized growth | C | memory | linked list | windows, prefix sums |
| Strings as constrained arrays, immutability | C | arrays | arrays | string techniques |
| 2-D grids and matrices | C | arrays | graphs | grid traversal |
| Singly & doubly linked lists | C | references | arrays | LRU cache, list surgery |
| Stack | C | arrays | queue | DFS, monotonic stack, parsing |
| Queue and deque | C | arrays | stack | BFS, sliding-window max |
| Hash map & set, collisions, load factor | C | arrays | sorted structures | counting, dedup, memoization |
| Binary tree | C | references | linked list | traversals |
| Binary search tree | C | binary tree + ordering | hash map | ordered queries |
| Balanced trees (conceptual) | X | BST | plain BST | why library maps are log n |
| Heap / priority queue | C | arrays + tree shape | sorted array | top-k, scheduling, Dijkstra |
| Graph representations: list, matrix, implicit | C | arrays + maps | trees | all graph work |
| Trie | X | trees + alphabet | hash map | prefix search, autocomplete |
| Disjoint set union | X | arrays + trees | BFS/DFS components | Kruskal, dynamic connectivity |
| Prefix-sum & difference arrays | C | arrays | recomputation | range sums, sweeps |
| Segment tree, Fenwick tree | P | trees + prefix sums | prefix sums | mutable range queries |
| Bitset / bitmask as a set | X | integers | hash set | subset enumeration, bitmask DP |
| LRU/LFU composite structures | X | list + map | either alone | cache design questions |

## Rail T — Techniques

| Concept | Tier | Built from | Contrasts with | Unlocks |
|---|---|---|---|---|
| Iteration and accumulation | C | arrays | — | all scans |
| Two pointers, same & opposite direction | C | arrays, ordering | brute-force pairs | pair sums, partitioning |
| Fast & slow pointers | C | two pointers | index arithmetic | cycle detection, midpoint |
| Sliding window, fixed | C | arrays | full rescan | fixed-length aggregates |
| Sliding window, variable | C | fixed window + invariant | two pointers | longest/shortest constrained |
| Prefix sums & running state | C | arrays | nested loops | subarray sums |
| Sorting as preprocessing | C | ordering | hashing | intervals, greedy, dedup |
| Comparison sorts & stability | C | recursion, arrays | non-comparison sorts | custom orderings |
| Counting / radix / bucket sorts | X | arrays | comparison sorts | linear-time ordering |
| Binary search on a sorted array | C | ordering | linear scan | log-n lookup |
| Binary search on the answer space | C | binary search + monotone predicate | array search | min-max optimization |
| Recursion and the call stack | C | functions | iteration | trees, D&C, DP |
| Divide and conquer | C | recursion | iteration | mergesort, quickselect |
| Backtracking with pruning | C | recursion | brute-force enumeration | permutations, subsets, constraints |
| Tree traversals: pre/in/post/level | C | trees + recursion/queue | linear scans | tree problems |
| Tree DFS returning values upward | C | recursion | traversal for printing | diameter, LCA, validation |
| Graph BFS, unweighted shortest path | C | queue + graph | DFS | levels, min steps |
| Graph DFS, components, cycle detection | C | stack/recursion + graph | BFS | connectivity, ordering |
| Topological sort | C | DFS / indegrees | plain DFS | scheduling, dependencies |
| Dijkstra | X | heap + graph | BFS | weighted shortest path |
| Bellman-Ford, Floyd-Warshall | P | DP over edges | Dijkstra | negative weights, all-pairs |
| MST: Kruskal, Prim | P | DSU / heap | shortest path | network cost |
| Union-find as a technique | X | DSU | traversal | grouping, redundancy detection |
| Sweep line & event ordering | X | sorting + heap | pairwise checks | intervals, meeting rooms |
| Greedy with exchange argument | C | sorting | DP | activity selection, jump games |
| DP: state, transition, base case | C | recursion + memo | greedy | all DP |
| DP families: linear, subsequence, knapsack, grid, interval, tree, bitmask | C→P | DP core | greedy | optimization problems |
| Monotonic stack & queue | X | stack / deque | brute-force scans | next-greater, window max |
| Bit manipulation and masks | X | integers | arithmetic | parity, subsets, XOR tricks |
| String matching: hashing, KMP, Z | P | strings + prefix ideas | naive matching | substring search |
| Randomized: shuffle, reservoir, quickselect | X | probability | deterministic | sampling, selection |
| Number theory: gcd, primes, modular arithmetic | X | arithmetic | brute force | math problems |

## Rail E — Engineering and analysis

| Concept | Tier | Assessed by |
|---|---|---|
| Asymptotic reasoning: big-O/Θ/Ω, amortized, space | C | predicting complexity before running code |
| Invariant identification and maintenance | C | stating the loop invariant in one sentence |
| Edge-case enumeration | C | producing the failing input for a given solution |
| Test design, including adversarial cases | C | writing a test that breaks a plausible solution |
| Manual tracing and state prediction | C | predicting output before execution |
| Debugging a near-correct solution | C | locating the wrong line **and** naming the wrong assumption |
| Reviewing model-generated code | C | accept / reject / repair with a stated reason |
| Trade-off articulation | C | verbal defence of the chosen approach |
| Requirement-change adaptation | C | correct modification when constraints shift |
| Practical concerns: overflow, precision, recursion limits, locale, immutability | X | constraint-aware implementation |
| Working inside unfamiliar code | X | correctly modifying a small existing repo |

`[DERIVED]` Rail E is not a soft add-on. Reviewing and repairing generated code is load-bearing precisely because generated code is now abundant while trust in its accuracy is not. High adoption plus low trust is what makes verification the scarce skill.

---

# 5. Replacing invented allocations with a measurement pipeline

v1's biggest failure was asserting a 150-problem topic allocation as though it were derived from frequency data. It was not. Here is the pipeline that produces a real one.

## Step 1 — Build the frequency dataset

`[VERIFIED]` Public sources exist and can be aggregated:

- Company-tagged problem lists with frequency and recency windows, published as structured datasets in several open GitHub repositories (organized by company, with 30-day / 3-month / 6-month windows).
- Community aggregators that rank problems by frequency and recency across interview-report sources, filterable by company, role, and round.
- Platform-native company tags and official study plans.

`[DERIVED]` Handling rules, because this data is dirty:

1. **Recency weighting.** Weight 30-day and 3-month windows above all-time. Interview fashion moves.
2. **Cohort segmentation.** Internship, new-grad, and senior loops differ. Never merge them into one number.
3. **Self-selection correction.** People post about problems that surprised them. Treat raw counts as biased toward the memorable and cross-check independent sources.
4. **Concept mapping, not problem copying.** The output is a **weight per concept**, not a list of problems to reproduce — better pedagogy and cleaner legally (Section 13).

## Step 2 — Derive weights, then allocate

The formula, stated explicitly so it can be audited:

```
concept_weight = 0.5 × recency_weighted_frequency
               + 0.3 × prerequisite_centrality     // out-degree in the concept DAG
               + 0.2 × transfer_breadth            // # of later concepts that reuse it

anchor_count(concept) = round(total_anchors × normalize(concept_weight))
                        clamped to [min_viable, max_useful] per tier
```

`[DERIVED]` Frequency alone is the wrong objective. Prefix sums are not a frequent *interview topic* but are high-centrality; dropping them starves later concepts. Hence three terms, not one.

## Step 3 — What we may claim about counts today

| Quantity | v1 claim | v2 status |
|---|---|---|
| Total anchor problems | "150" | `[ESTIMATE]` — chosen for comparability with NeetCode 150, not derived. Replace with Step 2 output. |
| Per-topic allocation | full table | **Withdrawn.** Regenerate from Step 2. |
| "15–20 high-frequency patterns" | stated as fact | **Withdrawn.** Inherited folklore. Section 4 is a *coverage inventory*, not a frequency ranking. |
| Assessed items per concept | "100–160 total" | `[ESTIMATE]` — superseded by the item contract below, which is a *design minimum*, not a measurement. |

## Step 4 — The per-concept item contract

`[DERIVED]` from the braid: each concept needs enough items to fill Focus once and Return/Discriminate/Compose repeatedly over months.

| Item role | Min count | Which slot needs it |
|---|---|---|
| Trace / predict-the-state | 3 | Focus, plus cheap Return fuel |
| Parsons / reordering | 2 | structure without syntax load `[RESEARCH]` |
| Faded worked example | 2 | guidance fade `[RESEARCH]` |
| Canonical application | 2 | invariant consolidation |
| Contrast partner | 2 | Discriminate needs a *pair*, so pairs must exist |
| Transfer variant, different surface | 3 | Compose, and unlabeled Return |
| Broken solution to repair | 2 | Rail E |
| Generated-code review item | 1 | Rail E |
| Complexity / trade-off prompt | 2 | Rail E |
| Requirement-change follow-up | 2 | interview realism |

**Floor: 21 items per core concept.** `[DERIVED]` from slot requirements. With ~30 core concepts that implies 600+ items for core coverage alone — which is exactly why Section 14 constrains the MVP to a vertical slice instead of breadth.

---

# 6. How students choose a path — without choosing a single concept

## Diagnostic, not self-report

`[DERIVED]` "Are you a beginner?" is unreliable. A short adaptive diagnostic (~15 minutes) probes all three rails and outputs a **mastery vector**, not a level label:

- **Rail S:** given a task, pick the structure and justify the cost.
- **Rail T:** given an unlabeled problem, name the manoeuvre. Highest-signal probe, and exactly what blocked competitors never test.
- **Rail E:** predict output; spot the bug; state the complexity.

## Paths are entry points and slot mixes, not different content

All paths draw from one library. They differ only in initial rail balance, slot weighting, and gate strictness. `[ESTIMATE]` on every mix — calibrate against real completion and transfer data.

| Path | For | Initial rail balance | Braid emphasis |
|---|---|---|---|
| **Foundations** | not yet a confident programmer | S 50 / T 25 / E 25 | heavy Focus and tracing; Compose kept small |
| **Coursework** | CS student mid-course | S 40 / T 35 / E 25 | correctness reasoning and complexity in Rail E |
| **Interview core** | first real loop coming | S 30 / T 45 / E 25 | Discriminate weighted up; labels hidden early |
| **Sprint** | loop in weeks | S 20 / T 45 / E 35 | Return and Compose dominate; Focus only where the diagnostic found gaps |
| **Depth** | already comfortable | S 25 / T 40 / E 35 | advanced tier, multi-concept Compose, verbal defence |

**No path is a topic list.** Every path is a braid generator. `[DERIVED]` — this is the mechanical guarantee that no learner ends up grinding one concept.

## Time estimates

`[ESTIMATE]`, and deliberately **not shown to learners** in v2. v1's "16–24 weeks" had no completion data behind it.

Replacement policy: display **mastery progress and readiness**, never calendar promises. After 200+ learners complete a path, publish observed medians with ranges. Until then the honest learner-facing line is: "your next session is chosen from what you have and have not yet proven."

---

# 7. Mastery: the vector, the gate, and why nothing ever "closes"

## The mastery vector

Ten independently tracked dimensions per concept. `[DERIVED]` from Rail E plus the braid slots.

| # | Dimension | Evidence that moves it |
|---|---|---|
| 1 | Mental model | correct state prediction on unseen input |
| 2 | Tracing | step-by-step execution accuracy |
| 3 | Selection | correct approach chosen on an **unlabeled** problem |
| 4 | Implementation | working solution within constraints |
| 5 | Complexity | correct time/space, and still correct after a change |
| 6 | Edge cases | enumerates and handles boundaries unprompted |
| 7 | Test design | produces a test that breaks a flawed solution |
| 8 | Debugging | locates the wrong assumption, not just the wrong line |
| 9 | Retention | success on a spaced, unlabeled Return item |
| 10 | Transfer | success on a Compose item combining this with another concept |

`[DERIVED]` Dimensions 3, 9, and 10 are the ones no checklist product can measure, because measuring them requires hiding the label and remembering the learner's history. They are the moat.

## The gate

A concept advances only on evidence, and **advancement is not completion**:

| State | Requirement |
|---|---|
| Introduced | Focus slot completed |
| Applied | canonical application solved |
| Discriminated | contrast pair resolved correctly, labels hidden |
| Retained | ≥ 2 successful spaced Return items, ≥ 7 days apart |
| Integrated | ≥ 3 successful Compose items over ≥ 3 weeks, each with a *different* partner concept |

`[DERIVED]` Only *Integrated* counts as mastered — and Integrated is unreachable by studying one concept in isolation, by construction. This is the structural enforcement of the requirement that students not go after one concept.

## Decay and re-entry

`[RESEARCH]` Retrieval practice and distributed practice both show moderate-to-large benefits, with reported effect sizes commonly in the d ≈ 0.5–0.85 range, and retrieval advantages growing at longer delays. `[DERIVED]` So mastery must decay in the model, or the model lies. A concept unpracticed past its scheduled interval loses *Retained* and re-enters Return rotation automatically.

## Failure diagnosis, not failure scoring

`[DERIVED]` A wrong answer routes by *error type*, never by score:

| Observed error | Failing dimension | Intervention |
|---|---|---|
| Wrong structure chosen | Selection | a contrast pair — not more of the same problem |
| Right approach, broken bounds | Implementation | Parsons + trace on the invariant |
| Correct code, wrong stated complexity | Complexity | cost-annotation drill |
| Passes samples, fails edges | Edge cases | adversarial test-writing task |
| Cannot explain a working solution | Mental model | rebuild from visualization, then re-explain |
| Accepts flawed generated code | Review | graded review set with planted defects |

---

# 8. Anti-boredom design, honestly labeled

`[RESEARCH]` Genuinely supported: retrieval practice, spacing, interleaving, worked examples with faded guidance, subgoal labeling, Parsons problems, immediate targeted feedback, and mastery-based progression all outperform passive study or undifferentiated drilling.

`[DERIVED]` What follows: the braid *is* the anti-boredom mechanism, because each session contains four activity types across three or more concepts. Variety is a byproduct of correct pedagogy, not a decoration bolted on top.

`[ESTIMATE]` Specific tuning rules — v1 stated these as if researched. They are heuristics awaiting validation, and should live in code as tunable parameters, not constants:

- no more than 3 consecutive items of the same interaction type;
- at least one visual and one verbal item per session;
- Focus slot capped around 15 minutes before switching;
- difficulty targeted at roughly a 70–85% success band.

## What is not a boredom fix

`[DERIVED]` Streaks, XP, and leaderboards drive visit frequency, not learning depth, and can crowd out the intrinsic motivation this product depends on. Reward the six real signals — selection, complexity, testing, debugging, explanation, retention — and let streaks be cosmetic.

---

# 9. Module blueprint (the Focus slot)

Twelve components. `[DERIVED]` from worked-example, subgoal-labeling, and faded-guidance research plus the three-view synchronization thesis.

1. **Need hook** — a task the learner's current tools handle badly.
2. **Mental-model lab** — manipulate the structure before naming it.
3. **Naming** — the concept and its one-sentence invariant.
4. **Three-view binding** — visualization, code, and plain English stepped in lockstep.
5. **Subgoal labels** — the solution's steps named as reusable sub-goals.
6. **Operations lab** — cost of each operation, discovered rather than stated.
7. **Contrast card** — the nearest neighbour concept and the tell that separates them.
8. **Parsons construction** — assemble correct code from shuffled lines.
9. **Faded worked examples** — full → partial → blank.
10. **Canonical challenge** — unlabeled from here on.
11. **Rail E block** — complexity prompt, adversarial test, broken-solution repair, generated-code review.
12. **Handoff to the braid** — the concept registers for Return, Discriminate, and Compose scheduling. It is never marked done.

---

# 10. Content data model

Entirely missing from v1, which is why v1 was not buildable. Shapes are illustrative but complete enough to implement against.

```ts
type Rail = "S" | "T" | "E"
type Tier = "core" | "extended" | "specialist"

interface ConceptNode {
  id: string                    // "technique.sliding-window.variable"
  rail: Rail
  tier: Tier
  name: string
  invariant: string             // one sentence, required
  builtFrom: string[]           // prerequisite ids (DAG edges)
  contrastsWith: string[]       // required, min 1 — powers Discriminate
  unlocks: string[]
  weight: {                     // from Section 5, Step 2
    recencyWeightedFrequency: number | null   // null until the dataset exists
    prerequisiteCentrality: number
    transferBreadth: number
    computedAt: string | null
  }
}

type ItemRole =
  | "trace" | "parsons" | "fadedExample" | "canonical" | "contrastPartner"
  | "transfer" | "repairBroken" | "reviewGenerated" | "complexity" | "requirementChange"

interface Item {
  id: string
  role: ItemRole
  primaryConcept: string
  alsoRequires: string[]        // non-empty => eligible for Compose
  labelVisible: boolean         // false in Return / Discriminate / Compose
  difficulty: 1 | 2 | 3 | 4 | 5
  constraints: { inputSize?: string; time?: string; space?: string }
  plantedDefects?: Array<{ line: number; kind: string; revealsDimension: number }>
  hintLadder: string[]          // conceptual -> structural -> near-solution
  provenance: {                 // Section 13 — legal gate
    origin: "original" | "publicDomain" | "referencedByLink"
    externalRef?: string        // link/ID only; never a copied statement
    reviewedBy: string
    reviewedAt: string
  }
}

interface MasteryEvent {        // append-only; the model is derived, never overwritten
  learnerId: string
  itemId: string
  conceptId: string
  dimension: 1|2|3|4|5|6|7|8|9|10
  outcome: "pass" | "fail" | "partial"
  errorType?: string            // keys Section 7's diagnosis table
  labelWasVisible: boolean      // labeled and unlabeled success are not equal evidence
  hintsUsed: number
  latencyMs: number
  sessionSlot: "focus" | "return" | "discriminate" | "compose"
  at: string
}
```

`[DERIVED]` Two non-obvious requirements worth defending: `contrastsWith` is mandatory because Discriminate cannot be scheduled without it, and `labelWasVisible` must be stored per event because a labeled success is weaker evidence than an unlabeled one.

---

# 11. The scheduler

`[DERIVED]` The scheduler *is* the product. Content without it is a checklist.

```
buildSession(learner):
  1. decayMastery(learner)                          // elapsed spacing intervals
  2. focus    = nextConceptWithSatisfiedPrereqs(learner)
                or stalledConcept at reduced share  // a stall never blocks
  3. returns  = dueRetentionItems(learner, limit 3, labelVisible = false)
  4. contrast = contrastPairFor(focus.contrastsWith ∪ recentErrorConcepts)
  5. compose  = item where primaryConcept = focus
                and alsoRequires ∩ learner.appliedConcepts ≠ ∅
  6. assert distinctConcepts(session) >= 3
     assert distinctRails(session)    >= 2
     else regenerate
  7. targetDifficulty(success band)                 // [ESTIMATE] 70–85%, tunable
```

Step 6 is the enforcement point for "no student sits on one concept." It is an assertion in code, not a guideline in a document.

---

# 12. Production cost and authoring pipeline

Also absent from v1.

## Pipeline

1. Define the `ConceptNode`, including the invariant and at least one contrast partner. An invariant that needs more than one sentence fails review.
2. Design the single canonical execution model all three views share.
3. Write the **wrong** solutions first — planted defects define what the module must teach.
4. Author the 21-item floor set (Section 5, Step 4).
5. Build the three synchronized views against the canonical model.
6. Write the hint ladder: conceptual → structural → near-solution. Never syntax-first.
7. Pass four review gates: pedagogy, technical correctness, accessibility, **and legal provenance**.

## Cost model

`[ESTIMATE]` — every figure exists to be replaced.

| Work | Est. hours per core concept |
|---|---|
| Concept definition and invariant | 2–4 |
| Canonical model + three synchronized views | 8–16 |
| 21-item floor set with hints and defects | 12–20 |
| Visualization implementation | 8–20 |
| Four review passes | 4–8 |
| **Total** | **34–68** |

**Calibration gate:** author 3 concepts end to end, measure actual hours, replace this table before any roadmap, budget, or hiring plan uses it. Do not multiply an estimate by 30 and call it a plan.

---

# 13. Intellectual property policy

`[DERIVED]` A commercial product cannot copy problem statements, editorials, or curated lists from other platforms. v1 mentioned this twice in passing, which is not a policy.

Rules, enforced by `Item.provenance` and blocking at review:

1. **Problem statements are original** — our own framing, constraints, and narrative.
2. **Test harnesses and reference solutions are original.**
3. **Public problems are referenced, never reproduced.** Store a link or ID in `externalRef`; the learner practises the underlying concept on our statement.
4. **Curated lists are market signal, not content.** We may state verified facts about them and map them to our concepts; we may not reproduce them.
5. **Frequency datasets derive concept weights only.** Check each source's terms before ingestion, prefer openly licensed datasets, record source and license per ingestion.
6. **Every item carries provenance and a named reviewer.** No provenance, no publish.
7. **Generated-code review items are authored in-house** with intentionally planted defects, so no third-party output is redistributed.

---

# 14. MVP scope: a vertical slice, not a survey

`[DERIVED]` Because the differentiator is the scheduler and the mastery model, the MVP must prove those. Breadth proves nothing a checklist does not already prove.

## Scope

Six concepts spanning all three rails, chosen so that Compose items genuinely exist between them:

| Concept | Rail |
|---|---|
| Arrays and amortized cost | S |
| Hash map and hash set | S |
| Two pointers | T |
| Sliding window, fixed and variable | T |
| Complexity reasoning and invariants | E |
| Test design and debugging near-correct code | E |

## Deliverables

- 6 modules, three-view synchronized.
- ~126 items (21 floor × 6), including 12 contrast partners and ≥ 15 Compose items.
- The scheduler, with all three braid assertions enforced.
- Append-only mastery event log capturing `labelWasVisible`.
- Provenance review gate active from the first item.

## Validation experiments — the actual point of the MVP

| # | Question | Design | Success signal |
|---|---|---|---|
| V1 | Does braiding beat blocking on unlabeled selection? | two arms, same content, blocked vs braided; delayed unlabeled test at 14 days | braided arm higher on dimensions 3 and 10 |
| V2 | Does the 40/20/20/20 split hold? | three-arm split test | winner adopted; split becomes internally verified |
| V3 | Does non-blocking stall handling reduce abandonment? | stall-blocking vs rail-switching | lower drop-off at the first hard gate |
| V4 | Do the tuning heuristics matter? | vary consecutive-item cap and success band | retain only heuristics that move outcomes |
| V5 | Does generated-code review transfer? | pre/post on unseen defective code | measurable improvement |

Only after V1–V5 do the withdrawn numbers in Section 5 get regenerated from real data.

---

# 15. Outstanding work that must precede any public claim

| # | Work | Replaces | Blocking for |
|---|---|---|---|
| **W1** | Problem-level overlap matrix of Blind 75 / NeetCode 150 / LeetCode 75 / Grind 75 / Striver sheets, with true per-topic counts | v1's generic competitor analysis | any competitive claim or positioning copy |
| **W2** | Recency-weighted, cohort-segmented frequency dataset | v1's invented allocation and "high-frequency patterns" | anchor counts, topic weights |
| **W3** | Authoring-cost calibration on 3 real concepts | Section 12 estimates | roadmap, budget, hiring plan |
| **W4** | V1–V5 experiments | Section 2 and 8 estimates | any learning-efficacy claim |
| **W5** | Legal review of frequency-source terms | Section 13 assumptions | data ingestion at scale |

---

# 16. Sources and evidence base

**Verified list and platform facts**

- Blind 75 — set size, ten-topic organization, approximate per-topic distribution (arrays ≈ 9–10, strings ≈ 8–10, trees ≈ 11–14, graphs ≈ 6–8, DP ≈ 11), pattern-breadth thesis, and the commonly recommended arrays/strings → trees/graphs → DP progression.
- NeetCode 150 — the ordered 18-category roadmap and its explicit easiest-to-hardest-within-category guidance.
- LeetCode 75 — official curated 75-problem, 14-week plan; DFS/BFS split for binary tree and graphs; 1-D vs multidimensional DP split; coverage of two pointers, sliding window, stack, queue, linked list, heap/priority queue, backtracking.
- Grind 75 — configurable week/hour schedule generation.
- Frequency data availability — company-tagged open datasets with 30-day/3-month/6-month recency windows, plus community aggregators ranking by frequency and recency with company/role/round filters.

**Learning-science foundations**

- Interleaving vs blocking, including the meta-analytic estimate of roughly Hedges' g ≈ 0.42, the discriminative-contrast mechanism, and the boundary condition favouring blocking for highly variable categories.
- Retrieval practice (testing effect) and distributed practice, with reported effect sizes commonly in the d ≈ 0.5–0.85 range and retrieval advantages increasing at longer retention intervals.
- Worked examples with faded guidance, cognitive-load management, subgoal labeling, Parsons problems, mastery learning, and formative feedback in programming education.

**Hiring and future-skills context**

- Movement of technical assessment toward practical, AI-enabled, and repository-based formats.
- High AI-tool adoption paired with low trust in output accuracy, which elevates verification, debugging, and review skills.
- Analytical thinking ranked among the leading core skills, with AI-related skills among the fastest growing.

**Honest limitation.** Section 3 list facts and the learning-science findings above are corroborated. Everything tagged `[ESTIMATE]` is not. This document's value is the architecture and the measurement plan; its numbers become trustworthy only after W1–W5.

---

# Final recommendation

Build the **braid**, not the ladder.

The concept inventory in Section 4 is table stakes — anyone can list DSA topics. The defensible product is the combination of three things no existing list has: a **mastery model that remembers what the learner has proven**, a **scheduler that refuses to serve a single-concept session**, and **assessment of the AI-era skills** of selection, verification, debugging, and explanation.

Every session should be able to answer one question: *which three or more concepts did I just hold in play at once, and which one did I have to choose between without being told?* If a session cannot answer that, the scheduler built it wrong.
