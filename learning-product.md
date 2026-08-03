# Algora — Section 4: Learning Product (14 screens)

Image-generation prompts + build contract for the logged-in core product.

**Pipeline this document serves** (three passes, in this order):

| Pass | You produce | This doc gives you |
|---|---|---|
| 1 | A prompt | §2 — 14 self-contained prompts |
| 2 | A static image | §2 + §0 paste blocks (visual reference only) |
| 3 | A static website | §3 SVG construction · §4 SVG animation · §5 image→code rules |

Companions: `content.md` (curriculum architecture) · `concept-page-spec.md` (stage order + page anatomy) · `taxnomy-and-transfer.md` (two-axis model) · `content-research.md` (learning-science basis) · `research.md` (engine, tokens, a11y) · `roadmap-builder.md` (§8 roadmap screens).

Evidence tags carried from the source docs: `[RESEARCH]` published education research · `[DERIVED]` logical consequence of our design · `[ESTIMATE]` judgement, must be validated with learner data. `[SPEC → x]` = this requirement is quoted from doc `x`; do not "improve" it locally.

---

# 0. What changed in this rewrite, and why

The previous version of this file described a **linear course product**: 42 lessons, 6 modules, a 29% progress ring, a sidebar of topics, autoplay playback, and a "Mark as complete" button. Every one of those is explicitly ruled out by the newer specs. This is the full delta — each row is a defect that was shipping.

| # | Old file said | Authority says the opposite | Source |
|---|---|---|---|
| 1 | "Lesson 12 of 42", `29%` progress ring | "Progress dots show the **stage, not a percentage**. No '87% complete' — percentages imply the concept can be finished" | `concept-page-spec` §2.1 |
| 2 | Sidebar topic list + 6-module accordion, finished top-to-bottom | "**No sidebar of topics** during a concept. A visible topic list invites 'let me finish all arrays first,' which is the behaviour we are removing" | `concept-page-spec` §2.1, §3.5 |
| 3 | Flat Explore grid: BFS, DFS, Dijkstra, Quicksort, Union-Find, Heap as siblings | Nouns and verbs as siblings **is the bug**. Sidebar grouped under **Machinery / Structures / Techniques** so "nouns and verbs are never siblings" | `taxonomy` §1, §5 |
| 4 | Difficulty chip + `O(n)` complexity printed on the visualizer | "Complexity is **not** printed as a badge. It is discovered in the operations lab and asked in Rail E" | `concept-page-spec` §2.2 |
| 5 | "42 lessons · 6 modules · ~7 weeks" | No "calendar promise (master DSA in 12 weeks) — we have no completion data to justify one" | `concept-page-spec` §3.5, `content` §Standing-rule |
| 6 | Playback bar with autoplay, timeline scrub, speed slider | "**Student-driven stepping, not autoplay.** Autoplay animation is passive" + **predict-before-reveal gates** at 2–3 steps | `concept-page-spec` §2.2 |
| 7 | "Mark as complete" ghost button | "**No concept closes.** Finishing a module moves a concept from *Focus* to *Return*, never to *Done*" | `content` §2 |
| 8 | Review card tagged "Graphs · BFS" | Return items are **unlabeled** — showing the tag *is* giving the answer | `content` §2, `taxonomy` §5 |
| 9 | Mastery = XP / Level / streak | Mastery = **10-dimension vector**; only *Integrated* counts, needing 3 Compose passes × 3 different partners × ≥3 weeks | `content` §7 |
| 10 | Border `#E4E9E7` (conflicted with `roadmap-builder`'s `#E6EBE9`) | **C-1: adopt `#E4E9E7`**, single token, no exceptions | `research` §9.3 |
| 11 | Nav: `Dashboard, Explore, My Path, Practice, Review, Compete, Achievements` | **C-2 canonical nav** adds `Roadmap`; one array, one file | `research` §9.3, D-2 |
| 12 | 9 screens | The 7-stage concept flow, the session braid, Discriminate, the hint ladder and the concept map had **no screen at all** | `concept-page-spec` §1, §2.5; `taxonomy` §6 |

**Time-wise roadmap — the resolved position.** `content.md` bans calendar *promises*; `roadmap-builder.md` specs a 90-day plan with day chips. These are compatible and the resolution is deliberate `[DERIVED]`:

> **Time is a plan. Mastery is the truth.** Days, phases and a daily minute budget are shown, because a student needs to know what to sit down and do (§27, §17). A **per-concept percentage, a "concept complete" state, or an estimated mastery date is never shown** (`concept-page-spec` §3.5). "Day 12 of 90" describes the *plan's* position in time. It never claims a concept is 13% learned.

---

# 0.1 PASTE BLOCK A — visual system (paste verbatim into every prompt)

> VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; card surfaces pure white #FFFFFF; 1px hairline borders #E4E9E7; pale-teal wash #E7F5F1 for selected chips, tint strips and callouts; #EEF2F0 for empty/locked/disabled fills. Text near-black ink #0E1513 for headings and primary text, muted slate #5B6763 for secondary text, labels and captions. ONE accent: teal #0E9C86, with #14B8A6 only as its hover/highlight step — used for primary buttons, active and selected states, focus rings, progress, links, and the logo glyph. Typography: Instrument Sans for headings and UI; JetBrains Mono for all code, numbers, day counts, stats, chips and field labels. Corners 12–16px on cards, 8–10px on buttons and inputs. Contrast comes from borders and spacing, not shadow — at most a very soft low-opacity shadow. Generous whitespace, high contrast, WCAG-AA, legible 14px+ body text, visible pale-teal focus states. Render ultra-high-fidelity 4k, pixel-crisp, aligned grids, real-looking student data and copy.
>
> NEVER: dark backgrounds, black panels, dark code editors, purple or violet, gradients, glows, decorative blobs or orbs, abstract filler shapes, stock photos of people, emojis, neon syntax colors, heavy drop shadows, device frames, browser chrome, mockup shadows, annotations, or lorem ipsum.

# 0.2 PASTE BLOCK B — app shell (paste verbatim into every prompt)

> APP SHELL (persistent and identical on every screen):
> LEFT SIDEBAR — 240px, white, 1px right border #E4E9E7. Top: "algora" wordmark in ink with a small teal two-node graph glyph. Vertical nav, 20px teal line icons + Instrument Sans labels, in exactly this order: Dashboard, Explore, My Path, Roadmap, Practice, Review, Compete, Achievements. The current screen's item is ACTIVE — teal label, #E7F5F1 wash pill, 3px teal left indicator bar. Bottom: a teal flame streak ICON (never an emoji) with a JetBrains Mono day count, and a compact user chip — initials avatar circle "AR", ink name "Arjun R.", JetBrains Mono "Lvl 12", and a slim teal XP bar.
> TOP BAR — 64px, white, 1px bottom border. Left: screen title or breadcrumb in ink. Center: slim search field, JetBrains Mono placeholder "Search structures, techniques…". Right: JetBrains Mono XP total "2,150 XP", a teal level ring, a notification bell with a small teal dot, and the avatar.
> CONTENT AREA — paper #F7F9F8, 32px padding, clear content grid, to the right of the sidebar and below the top bar.

`[SPEC → research §9.3 C-1/C-2/C-3]` The nav order above resolves conflict C-2. The border is C-1's `#E4E9E7`. The wash is C-3's `#E7F5F1`. Do not reintroduce `#E6EBE9`.

# 0.3 PASTE BLOCK C — the ban list for learning screens

Paste into every **concept-stage** prompt (§2 screens 19–24) and every practice/review screen (25, 26, 28):

> PEDAGOGICAL BANS (these are product rules, not style preferences): NO percentage complete anywhere; NO "concept complete", "Mastered" or "Done" state; NO checkbox topic list that can be finished top to bottom; NO complexity badge such as "O(n)" printed as a chip on the canvas; NO calendar or completion promise; NO autoplay-first playback (stepping is student-driven); NO pattern/technique label visible on any unlabeled problem, Return card, or Discriminate pair; NO two equally-weighted primary buttons — exactly one primary action, bottom-right; NO topic sidebar inside a concept stage.

---

# 1. The 14 screens

| # | Screen | Route (`taxonomy` §5) | Spec authority | Canvas |
|---|---|---|---|---|
| 17 | Dashboard — today's braid | `/` | `concept-page-spec` §2.5, `content` §2 | — |
| 18 | Explore — two-axis library | `/explore` | `taxonomy` §2, §5 | — |
| 19 | Concept stage 1 — **Hook** | `/technique/sliding-window#hook` | `concept-page-spec` §1, §2.3 | — |
| 20 | Concept stage 2 — **Play** | `…#play` | `concept-page-spec` §2.3 | **viz** |
| 21 | Concept stage 3 — **Name** | `…#name` | `concept-page-spec` §2.3 | — |
| 22 | Concept stage 4 — **Three views** ★ | `…#three-views` | `concept-page-spec` §2.2 | **viz** |
| 23 | Concept stage 5 — **Build** | `…#build` | `concept-page-spec` §2.3, §2.4 | — |
| 24 | Concept stage 6 — **Confuse** | `…#discriminate` | `concept-page-spec` §2.3, `content` §2 | — |
| 25 | Practice — unlabeled problem | `/problem/:slug` | `taxonomy` §5, `concept-page-spec` §2.4 | — |
| 26 | Solve debrief — Rail E | `/problem/:slug/debrief` | `content` §2 (Rail E), §7 | — |
| 27 | Roadmap board | `/roadmap` | `roadmap-builder` P42 + hybrid ruling | **board** |
| 28 | Return queue — unlabeled | `/review` | `content` §2, §7 | — |
| 29 | Concept map — bipartite | `/map` | `taxonomy` §6, §7 | **map** |
| 30 | Search — two-axis results | `/search` | `taxonomy` §5 | — |

★ = flagship. `research` §21 Phase 1: screen 22 is built **first**; "everything else is packaging."

The three canvases you asked for, and what each is *for*:

| Canvas | Screens | Job | Render |
|---|---|---|---|
| **Visualization canvas** | 20, 22 | One frame of execution, drawn from `Frame.state` | SVG, §3.2–3.4 |
| **Roadmap board canvas** | 27 | Pan/zoom phase board over plan-time | SVG + HTML overlay, §3.6 |
| **Concept map canvas** | 29 | Bipartite verbs↔nouns, lit edges = cells actually solved | SVG, §3.5 |

---

# 2. The prompts

Each prompt below is prefixed by this line. Paste **BLOCK A**, then **BLOCK B**, then the prompt body. Add **BLOCK C** where the table above marks a concept/practice screen.

> Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot, aspect ratio 16:9 at 1440x900, rendered as a real shipping product UI — NOT an illustration, NOT a collage, NOT a mockup on a device. One full desktop viewport including the app shell, nothing cropped, nothing cut off. PRODUCT: "algora" — students master algorithms through synchronized visualization, code, and plain-English explanation. Tagline: "See the algorithm think."

---

## PROMPT — 17. Dashboard: today's braid

MAIN CONTENT — the screen answers exactly one question: *what am I doing today?*

- Greeting: ink headline "Welcome back, Arjun." (the period as a small teal square). Slate subline "Today's session mixes four things — that mix is the point."
- **TODAY'S SESSION card** (white, full width, the hero — this replaces any "continue lesson" card). Four slot rows, each a distinct row with a 1px divider between, each showing a small teal line icon, a JetBrains Mono slot name, the item, and a right-aligned mono share:
  1. `FOCUS` — ink "Sliding window, variable size", teal chip "new", mono "~40%"
  2. `RETURN` — ink "2 items", slate "last seen 9 days ago", mono "~20%" — **the items are NOT named or tagged**, shown as two blank-faced mono placeholders "item 1", "item 2"
  3. `DISCRIMINATE` — ink "1 contrast pair", mono "~20%"
  4. `COMPOSE` — ink "1 problem needing this plus something older", mono "~20%"
  The FOCUS row is the current one — #E7F5F1 wash and a 3px teal left bar. Each row has a small teal drag handle on the left showing rows are reorderable; the RETURN and COMPOSE rows show a tiny slate lock icon with a mono caption "can't be removed".
  Footer of the card: slate italic caption "This session touches 4 concepts across 3 rails." and ONE primary teal button "Start session →" bottom-right.
- A row of THREE compact white stat cards, JetBrains Mono labels: "Streak · 23d" (teal flame line icon + an M–S week row of small teal checks and one #EEF2F0 empty square), "Today · 42m / 1h 30m" (slim teal bar), "Rails touched today · 2 of 3" (three small pills, two teal one slate).
- Lower two-column body:
  - LEFT (wider) — **"Concepts in play"** white card. 5 rows, each: ink concept name, a JetBrains Mono **state word** from this exact set — `Introduced`, `Applied`, `Discriminated`, `Retained`, `Integrated` — and a 5-segment stepper showing which state it has reached (reached segments teal, unreached #EEF2F0). Rows: "Hash map · Retained", "Sliding window, fixed · Discriminated", "Two pointers · Applied", "Binary search · Retained", "Prefix sum · Introduced". One row carries a small slate "overdue" chip with a teal circular-arrow icon and mono caption "returns today". **No percentages, no progress rings, no 'Mastered' badge.**
  - RIGHT (narrower) — **"Where your gaps are"** card: a small teal-line bipartite sketch, verbs left / nouns right, ~4 lit teal edges and ~3 faint #EEF2F0 edges, with a slate one-liner "You've only run sliding window on arrays." and a teal link "Open concept map →".
- Bottom strip card (#E7F5F1 wash, never dark): ink "Compose slot unlocks a new partner today", mono "sliding window + hash map", and a teal ghost link "Why this pairing →".

IMPORTANT: one cohesive light desktop app screen. The visual hierarchy must make the four-slot session card unmistakably the primary object.

---

## PROMPT — 18. Explore: the two-axis library

MAIN CONTENT — this is a library of **nouns, verbs and machinery**, never a flat grid of algorithm names.

- Header: ink headline "Explore" + slate subline "Nouns hold data. Verbs move through it. Machinery makes verbs possible."
- A SECONDARY LEFT RAIL inside the content area (white card, ~220px, separate from the app sidebar) with THREE mono section headers, generously separated so the groups read as different *kinds* of thing:
  - `MACHINERY` — Invariants, Call stack & recursion, Recurrence & cost, Amortised cost, Index arithmetic `[lo, hi)`, State design
  - `STRUCTURES` — Array, String, Hash map, Hash set, Stack, Queue, Deque, Linked list, Heap, Tree, BST, Trie, Graph, Union-find, Matrix, Interval set, Bitmask
  - `TECHNIQUES` — Two pointers, Sliding window, Prefix sum, Binary search on index, Binary search on answer, Monotonic stack, Hash counting, Recursion / divide & conquer, Backtracking, BFS, DFS, Topological order, Greedy exchange, Memoisation, Tabulation, Heap selection
  "Sliding window" is selected — teal label on an #E7F5F1 wash pill.
- MAIN PANEL — a **matrix**, not a card grid. This is the key visual: a table whose ROWS are techniques (verbs) and COLUMNS are structures (nouns), with mono axis labels — rows "sliding window", "two pointers", "prefix sum", "binary search", "monotonic stack"; columns "array", "string", "hash map", "deque", "grid", "tree". Cells:
  - a **solved cell** = small solid teal rounded square with a white check
  - an **available cell** = white square, 1px border, teal ring
  - a **not-a-real-problem cell** = flat #EEF2F0 square with a tiny slate dash and no border emphasis
  Above the matrix a slate caption: "17 structures × 20 techniques — but only about 60 cells are real problems." Roughly a third of cells are #EEF2F0, so the sparseness is visible at a glance.
- A RIGHT DETAIL card for the selected verb (white): ink "Sliding window", a JetBrains Mono `Technique` kind-chip, the invariant sentence in ink on an #E7F5F1 callout with a 3px teal left edge — "the window always satisfies the condition; the right edge expands, the left edge repairs" — then a mono "substrates" list of exactly five rows with one-line slate justifications: "int array, fixed — simplest invariant" (teal check), "int array, variable — invariant becomes a condition" (teal check), "string + hash map — bookkeeping becomes a frequency map" (teal ring, mono "current"), "0/1 array + flip budget — condition becomes a resource" (hollow), "array + monotonic deque — window must answer 'max inside me'" (hollow). Bottom: a slate line "Taught once. Everything else is a labelled visit." and ONE teal button "Open concept →".
- NO difficulty chips, NO complexity badges, NO "Mastered" tags, NO pagination row.

IMPORTANT: a viewer must be able to tell, without reading, that rows and columns are two different *kinds* of thing.

---

## PROMPT — 19. Concept stage 1: Hook

Include BLOCK C.

CONCEPT SHELL (identical on screens 19–24, this is its definition):
- Top bar of the content area (white card, full width): left a teal "← Back" ghost; center ink "Concept: Sliding window" with a JetBrains Mono `Rail: Technique` chip beneath; right a STAGE INDICATOR — six dots, mono caption "Stage 1 of 6", dot 1 solid teal, dots 2–6 hollow #EEF2F0. **Six dots, never a percentage, never a bar.**
- Bottom bar of the content area (white, full width, 1px top border): left an invariant reminder line — on this stage it reads, in slate italic, "(no name yet)"; right exactly ONE primary teal button.
- **No topic sidebar inside the concept.** The area between the two bars is the stage body and nothing else.

STAGE BODY — a single centered white card, max ~720px, everything else empty paper. The student is being made to *fail* with old tools:
- Ink headline "Longest substring with no repeats."
- A JetBrains Mono input strip showing a string of ~14 letters on a paper-tinted background, and a mono "n = 100,000" chip.
- A pre-filled, read-only mono code block of a **nested double loop** — six lines, light theme, slate line numbers, no syntax neon, with a small mono caption "the only tool you have right now".
- A LIVE COST READOUT, the emotional center of the screen: a large JetBrains Mono elapsed timer "8.42s" in ink beside a mono "comparisons 4,999,950,000" and a slim bar that has visibly overrun its track — the overrun portion in slate #5B6763, not red, with a mono label "over budget".
- A slate one-line prompt: "That's the wall. What would let you stop re-scanning what you already scanned?" and a small ink single-line free-text input with a pale-teal focus ring.
- Bottom bar primary button: teal "I feel the cost →".

IMPORTANT: the words "sliding window" and any technique name appear NOWHERE on this screen. No code solution, no hint, no concept name. The screen's only job is a visible, uncomfortable failure.

---

## PROMPT — 20. Concept stage 2: Play (visualization canvas, no code)

Include BLOCK C. Use the CONCEPT SHELL from screen 19, with dots 1 filled, 2 solid teal current, 3–6 hollow, mono "Stage 2 of 6"; invariant line still slate italic "(no name yet)".

STAGE BODY — a full-width white canvas card with minimal chrome. There is **no code pane anywhere on this screen**.
- A horizontal strip of ~14 letter cells, JetBrains Mono capitals, each cell a 48px white rounded square with a 1px border, evenly spaced.
- A WINDOW TINT: a translucent #E7F5F1 rounded rectangle covering cells 4–8, with a 2px teal left edge handle and a 2px teal right edge handle, each drawn as a rounded vertical bar with a small teal grab-dot pattern — they must read as **draggable**. Mono labels "lo" under the left handle and "hi" under the right.
- Cells inside the tint show their letter in ink; cells outside are slate and slightly muted. One cell inside the tint is outlined in teal with a small mono callout "this letter appears twice inside the window".
- A **PREDICT GATE** as the primary interaction — a white card centered below the strip, 1px teal border: ink question "The right edge moves in one step. What must the left edge do?" and three answer pills in a row with mono labels "stay", "move right", "jump to the duplicate" — none selected, all white with 1px borders. Mono caption below: "prediction 2 of 2 — answer to continue".
- A small mono readout row: "window length 5", "distinct letters 4".
- Bottom bar primary: teal "Continue →", rendered clearly DISABLED (slate text on #EEF2F0) with a mono caption "answer the prediction first".

IMPORTANT: no concept name, no code, no complexity, no autoplay controls — dragging and predicting are the only affordances. The prediction gate must be visibly blocking progress.

---

## PROMPT — 21. Concept stage 3: Name

Include BLOCK C. CONCEPT SHELL with dots 1–2 filled, 3 solid teal current, mono "Stage 3 of 6".

STAGE BODY — deliberately the quietest screen in the entire product. One centered white card, max ~640px, enormous surrounding whitespace. It must feel like a held breath, not a documentation page.
- A small JetBrains Mono kind-chip `TECHNIQUE`.
- The name, large in Instrument Sans ink: "Sliding window".
- ONE sentence, the invariant, set larger than body text on an #E7F5F1 callout with a 3px teal left edge: "The window always satisfies the condition; the right edge expands, the left edge repairs."
- Slate caption: "This is the one sentence you must never lose. It will sit at the bottom of every screen from here on."
- A RESTATE INPUT: ink label "Say it back in your own words", a two-line text area with a pale-teal focus ring, and a mono character counter "0 / 140".
- Bottom bar: the invariant line now appears for the first time in slate mono at the bottom-left, and the primary teal button reads "Continue →".

IMPORTANT: NO wall of theory text, NO bullet list of properties, NO code, NO complexity, NO diagram. Exactly one name and one sentence. Whitespace is the design.

---

## PROMPT — 22. Concept stage 4: Three views ★ FLAGSHIP

Include BLOCK C. CONCEPT SHELL with dots 1–3 filled, 4 solid teal current, mono "Stage 4 of 6"; the invariant line is present in the bottom bar.

This is the most polished screen in the product — the differentiator. Render it richest.

STAGE BODY — a three-region synchronized panel, all three regions showing THE SAME single step:
- TOP-LEFT (largest) **VISUALIZATION** white card: the letter strip from stage 2, now with a #E7F5F1 window tint spanning cells 3–7, teal `L` and `R` pointer markers as small teal triangles beneath their cells with mono labels, the newly-entered cell at the right edge outlined 2px teal, and the duplicate cell inside the window carrying a teal ring. Two mono AUX CALLOUTS floated at the card's top-right as small white chips with 1px borders: "counts: {a:1, b:2, c:1}" and "best: 4".
- TOP-RIGHT **CODE** white card, light theme only: JetBrains Mono Python, slate line numbers, restrained syntax color (teal keywords, ink identifiers, slate comments, never neon). ~11 lines of a real variable-size sliding window. **Line 6 — the `while` that shrinks from the left — is highlighted with a full-width #E7F5F1 row and a 3px teal left edge.** In the gutter to the right of the highlighted line, small mono live values: `lo=3  hi=7  dup='b'`. Header row: a mono "Python ▾" pill and a mono "Reset" ghost link.
- BOTTOM, spanning full width, **PLAIN ENGLISH** card (#FFFFFF with an #E7F5F1 left edge): one ink sentence at comfortable reading size — "The right edge moved in, so the window now contains a duplicate — shrink from the left until the condition holds again." with the words "shrink from the left" in teal. A mono caption "step 7 of 19".
- BOTTOM CONTROL ROW inside the panel: step-first / step-back / step-forward / step-last controls as four equal ghost icon buttons — **there is no large play triangle and no autoplay emphasis**; step-forward is the only teal-filled control. A mono step readout "step 7 / 19". A discrete row of 19 small keyframe ticks, three of which are teal and slightly taller with tiny mono "?" marks and a slate caption "predict gates". A speed control is present but visibly de-emphasised — small, slate, mono "speed 1.0x".
- A small mono legend in the visualization card: "L left edge", "R right edge", "tint = window", each with its shape/icon as well as its color.
- Bottom bar: invariant line at left in slate mono; ONE primary teal "Continue →".

IMPORTANT: the three regions must be unmistakably IN SYNC — the same step reflected in the strip, in highlighted line 6, and in the sentence. A viewer must be able to verify the sync by reading. Stepping is student-driven; autoplay is not the emphasis. NO complexity badge, NO difficulty chip, NO "mark complete" button.

---

## PROMPT — 23. Concept stage 5: Build (Parsons + hint ladder)

Include BLOCK C. CONCEPT SHELL with dots 1–4 filled, 5 solid teal current, mono "Stage 5 of 6"; invariant line present.

STAGE BODY — a split workspace:
- LEFT (~38%) **TASK** white card: ink "Write the shrink step", a slate task statement, a small mono example I/O block on paper tint, and the **HINT LADDER** — exactly three rungs as stacked rows, each a white row with 1px border:
  1. mono `CONCEPTUAL` — ink "Which invariant is being broken?" — state: teal "used", with a small teal check
  2. mono `STRUCTURAL` — ink "Subgoal labels for each step" — state: white, teal ghost "Open" link
  3. mono `NEAR-SOLUTION` — ink "Loop skeleton with the key line blank" — state: white, teal ghost "Open" link
  Below the ladder, a slate caption in italic: "Hints cost mastery signal, not points." **There is no "reveal answer" button anywhere.**
- RIGHT (~62%) **EDITOR** white card, light theme: a mono tab row "Parsons · Faded · Write" with **Parsons active in teal**. Body shows a PARSONS TRAY — six draggable mono code lines as white rounded rows with 1px borders and small teal grip dots, presented shuffled, two of them already dropped into an indented assembly area on the right that shows dashed #E4E9E7 drop targets and mono indent guides. One dropped line sits at the wrong indent and carries a slate (not red) 1px left edge with a mono caption "indent doesn't match the loop body".
- Below the editor: a "Tests" strip, three rows with mono I/O and status chips — one teal "passed" check, one slate "not run", one slate "pending".
- Bottom bar: invariant line left; a ghost outline "Run" and ONE primary teal "Check →" at bottom-right.

IMPORTANT: the full solution is NEVER visible. Parsons (reorder) is the active mode, not free coding. Failure is shown in slate with a diagnostic sentence, never in red and never as a score.

---

## PROMPT — 24. Concept stage 6: Confuse (Discriminate)

Include BLOCK C. CONCEPT SHELL with dots 1–5 filled, 6 solid teal current, mono "Stage 6 of 6". **CRITICAL: the invariant line in the bottom bar is REPLACED on this stage by slate italic "labels hidden — decide for yourself", and the concept title in the top bar reads "Concept: —" with the name withheld.**

STAGE BODY — two problems side by side, perfectly symmetrical so neither looks like the "right" one:
- LEFT white card "Problem A": ink title "Longest run of letters with nothing repeated", a slate statement, a small mono example block.
- RIGHT white card "Problem B": ink title "Two values in a sorted list that add to a target", a slate statement, a small mono example block.
- Both cards carry an identical JetBrains Mono chip row with the movement row **withheld**: `Container: [ string ]` on the left and `Container: [ array, sorted ]` on the right, then a row reading `Movement: [ hidden until you commit ]` in slate on #EEF2F0. **No technique name appears on either card.**
- CENTER-BOTTOM, spanning both, a white decision card with a 1px teal border: ink "Which approach, and what is the tell?" Two answer pill groups, each a row of four mono unlabeled-but-descriptive options — "expand then repair one edge", "walk both ends inward", "precompute running totals", "sort first, then scan" — one group per problem, none selected. Below them a required ink text area labelled "What is the tell?" with mono placeholder "name the property that decides it" and a mono counter "0 / 140".
- Bottom bar: ONE primary teal "Commit answer →".

IMPORTANT: the phrase "sliding window", the phrase "two pointers", and every other technique name must appear NOWHERE on this screen — not in a chip, breadcrumb, title, tooltip or sidebar. The two problems must look deliberately similar. This screen's entire value is destroyed if a label leaks.

---

## PROMPT — 25. Practice: unlabeled problem

Include BLOCK C. Top bar breadcrumb: ink "Practice / unlabeled set / item 3" — **no topic in the breadcrumb**. Sidebar "Practice" ACTIVE. Add a JetBrains Mono timer chip "12:04" in the top bar.

MAIN CONTENT — split two-pane workspace:
- LEFT PANE white problem card: ink title "Longest substring without repeating characters", a slate statement, a mono example block on paper tint ("Input: \"abcabcbb\" → Output: 3"), a "Constraints" list in slate. The CHIP ROWS are the important detail — two rows, always two, never one:
  `Container: [ string ] [ hash map ]` — filled white chips with 1px borders
  `Movement: [ commit to an approach to reveal ]` — a slate chip on #EEF2F0 with a small teal eye-off line icon
  Beneath, an APPROACH COMMIT control: mono label "commit first" and four mono option pills, none selected. A small tab row "Description · Hints (3) · Tests" with Description active in teal — **no "Solutions" tab**.
- RIGHT PANE white code editor card, LIGHT theme only (white background, slate line numbers, teal keywords, ink identifiers, slate comments — never a dark IDE, never neon): a mono "Python ▾" pill and mono "Reset" link, a function stub plus four written lines, the current line on an #E7F5F1 row. Below it a "Tests" sub-panel with three rows: two teal "passed" checks, one slate "not run". Footer: ghost outline "Run" on the left, ONE primary teal "Submit" on the right, and a small mono caption "3 hint rungs available" — **no XP reward chip on this screen**.

IMPORTANT: the technique label is hidden behind the commit control, because showing it would be showing the answer. Light editor only.

---

## PROMPT — 26. Solve debrief: Rail E, not a score

Sidebar "Practice" ACTIVE. Breadcrumb "Practice / item 3 / debrief". Include BLOCK C.

MAIN CONTENT — a centered white card, ~860px, on paper. Calm and analytical, NOT a celebration screen.
- Header row: a flat teal check in an #E7F5F1 circle, ink headline "All tests passed." (period as a small teal square) and a slate subline "Now the part that actually moves mastery."
- **DIMENSIONS MOVED** — the primary block. Ink section label, then rows for the 10-dimension vector, each with a mono dimension name, a 5-segment stepper, and a mono evidence caption. Show: `Selection` (moved, teal, caption "chose correctly with the label hidden"), `Implementation` (moved, teal), `Tracing` (unchanged, slate), `Complexity` (mono "asked below"), `Edge cases` (unchanged, slate, caption "you never tested the empty string"). Unmoved dimensions render in #EEF2F0. **No overall score, no percentage, no grade.**
- **RAIL E PROMPTS** — two white sub-cards side by side, each a real question the student must answer, not a readout:
  1. ink "What is the time cost, and why?" with four mono option pills and a small ink "because…" input. A slate caption "you have not been told the complexity — this is where it is discovered".
  2. ink "This requirement just changed: the alphabet is now unbounded. What breaks?" with a two-line ink text area.
- **STATE CHANGE** strip (#E7F5F1 wash): mono "sliding window, variable · Applied → Discriminated" with a 5-segment stepper showing 3 of 5 reached, and a slate sentence: "Two more Compose passes with different partner concepts, over at least three weeks, before this reaches Integrated." A small teal circular-arrow icon with mono "returns in ~2 days".
- **WHAT'S NEXT** row, two white suggestion cards — "Compose: this + hash map" and "Return: 2 unlabeled items" (the second names no topic) — each with a small teal line icon and a ghost "Start →".
- Footer: ghost "Back to problem", ghost "Compare approaches", ONE primary teal "Next item →".

IMPORTANT: NO "beats 88% of submissions", NO runtime leaderboard, NO XP fireworks, NO confetti, NO "Mastered" badge, NO complexity printed as a badge — complexity is ASKED, not displayed. Subtle and premium, never loud.

---

## PROMPT — 27. Roadmap board canvas

Sidebar "Roadmap" ACTIVE. Top bar title: ink "Your 90-day plan".

MAIN CONTENT — a **pan/zoom board**, not a vertical list of cards. It must read as a canvas: a subtle 1px #EEF2F0 dot-grid background across the content area, small zoom controls (mono "−  100%  +" and a "fit" icon) floated bottom-right, and a thin horizontal minimap strip along the very bottom showing the whole 90 days with a teal viewport rectangle over the current region.

- A horizontal **TIME AXIS** pinned at the top of the board: mono day ticks every 5 days from "Day 1" to "Day 90", with a solid teal vertical "today" line at Day 12 carrying a small mono flag "Day 12".
- FOUR **PHASE LANES** as wide white rounded cards laid left-to-right along the axis, each sized to its day range so duration is spatial:
  1. `Foundations` Days 1–20 — teal phase-number chip, mono "Days 1–20", topic rows: Array, String, Hash map, Two pointers. Progress bar mostly teal.
  2. `Core structures` Days 21–45 — in progress, partial teal bar, and a teal "You are here" marker pinned to the today line.
  3. `Algorithms` Days 46–72 — slate, ahead.
  4. `Interview mode` Days 73–90 — slate, ahead.
  Inside each lane, 3–4 compact topic rows: a status dot (teal check = passed, teal ring = current, hollow #EEF2F0 = ahead), an ink topic name, a JetBrains Mono item count "items 8 / 12", and a small right chevron.
- **BRAID THREADS** — the detail that makes this Algora and not a Gantt chart: thin teal curved connector lines arcing BACKWARD from later lanes to earlier topics, showing that old concepts are re-touched. ~5 arcs, 1px, teal at low opacity, with two of them carrying tiny mono labels "return" and "compose". A slate legend below the board: "Curves are returns and compositions — nothing is finished when its lane ends."
- RIGHT SUMMARY RAIL (white cards, floated over the board, not part of it):
  - **Today card**: mono "Day 12", ink "Sliding window, variable size", three items with mono time estimates, mono "1h 30m planned · 42m done" with a slim teal bar, ONE primary teal "Start today's session".
  - **Plan card**: mono metrics — "Plan · 90 days", "Pace · on track" with a small teal check, "Sessions kept · 12 of 14", "Time/day · 1h 30m". Below them, in slate italic, the required disclaimer: "This is a plan, not a promise. Concept mastery is earned by evidence, not by the calendar."
  - **Overdue card**: mono "3 concepts overdue for return", a teal circular-arrow icon, ghost "Fold into today →".
- Header controls: ghost "Edit plan", ghost "Export".

IMPORTANT: the board must show plan-time (days, phases, "Day 12 of 90") but must NOT show a per-concept percentage, a "13% mastered" figure, or an estimated mastery date. A plan-completion figure is acceptable ONLY if it is explicitly labelled as sessions kept, never as learning.

---

## PROMPT — 28. Return queue: unlabeled

Sidebar "Review" ACTIVE. Top bar title ink "Return". Include BLOCK C.

MAIN CONTENT — a focused single-column layout on paper.
- Top strip: mono "item 3 of 12" with a slim teal bar, a mono "~8 min left", and a teal chip "due today · 12".
- A large centered **RETURN CARD** (white, ~720px, 1px border, with two faint stacked card edges peeking behind it to read as a deck):
  - **Where a topic tag would normally sit, there is instead a slate chip on #EEF2F0 reading mono "unlabeled" with a small teal eye-off icon.** This is the most important element on the screen.
  - Ink prompt: "You need the length of the longest stretch of this string with no repeated character. Which manoeuvre, and what stays true the whole time?"
  - A small embedded mono strip of ~10 letter cells as a visual, with no window tint and no pointers — no hint is given.
  - TWO required inputs: a row of four mono approach pills (none selected) and a single-line ink input labelled "the thing that stays true".
- Below the card, an ANSWER STATE shown as the revealed variant: an #E7F5F1 answer box with ink "Sliding window — the window always satisfies the condition; the right edge expands, the left edge repairs.", a slate one-line explanation, and a mono caption "you last saw this 9 days ago".
- SELF-GRADE row: four pill buttons with mono labels "again", "hard", "good", "easy" — "good" solid teal, the rest light outline pills — each with a small mono next-interval caption beneath ("<1m", "10m", "3d", "9d").
- A right-aligned ghost "Skip" link and a mono caption "skipping keeps it due".

IMPORTANT: the topic is hidden BEFORE the answer and revealed only after. A tag above the question would be the answer — that is the single failure this screen exists to prevent. No XP chip.

---

## PROMPT — 29. Concept map canvas: bipartite

Sidebar "My Path" ACTIVE (Mastery is a child of My Path). Top bar title ink "Concept map".

MAIN CONTENT — a large pan/zoom **bipartite graph canvas** filling the content area, on a subtle 1px #EEF2F0 dot grid, with mono zoom controls "−  100%  +" bottom-right.
- TWO explicit columns with mono axis headers at the top: `TECHNIQUES (verbs)` on the left, `STRUCTURES (nouns)` on the right. The two-column separation must be immediately obvious — this is the whole point.
- LEFT column: ~8 verb nodes as white rounded pill nodes with 1px borders and ink labels — "sliding window", "two pointers", "prefix sum", "binary search", "monotonic stack", "BFS", "DFS", "backtracking".
- RIGHT column: ~8 noun nodes, same pill treatment — "array", "string", "hash map", "deque", "grid", "tree", "graph", "heap".
- EDGES between the columns, and their state is the content:
  - **lit edge** = 2px solid teal, meaning the student has actually solved that cell
  - **available edge** = 1px #E4E9E7 solid
  - **never-attempted edge** = 1px #E4E9E7 dashed, low opacity
  "Sliding window" is selected: its node has a teal border and #E7F5F1 fill, and its edges are emphasised — a lit teal edge to "array", and clearly DASHED faint edges to "string", "hash map" and "deque".
- A CALLOUT anchored near the selected node (white card, 1px teal border, small pointer): ink "Sliding window is only lit on one container." then slate "A verb that applies to one noun is a trick, not a skill." and a mono line `transfer gap · 22 pts` with a slate caption "target under 15" and a teal ghost "Practise it on a string →".
- A small MACHINERY BAND across the bottom of the canvas, visually separated by a 1px divider so it reads as a different layer: mono `MACHINERY` and five small flat #E7F5F1 chips — "invariants", "call stack & recursion", "recurrence & cost", "amortised cost", "index arithmetic" — each with thin teal lines rising to several verb nodes above. Slate caption: "Machinery is not a topic you finish. It is what the verbs are made of."
- A LEGEND card (white, floated top-right): three rows, each with its line style drawn plus a text label — "solid teal · solved", "grey · available", "dashed · never tried" — plus a mono counter "lit cells 14 of ~60".

IMPORTANT: colour must never be the only signal — solid/dashed line style carries the same information. The verbs-left / nouns-right split must be unmistakable at a glance. No percentages.

---

## PROMPT — 30. Search: two-axis results

Sidebar with no item active. TOP BAR search field prominently FOCUSED with a pale-teal focus ring, containing the query "sliding window".

MAIN CONTENT:
- Header: ink "Results for “sliding window”" (matched term subtly teal) with a slate "24 results".
- A FILTER CHIP ROW of mono **kind** filters that match the taxonomy, not generic content types: "All (24)", "Machinery (2)", "Structures (5)", "Techniques (3)", "Compositions (4)", "Problems (10)" — "All" selected in teal.
- Two-column body:
  - LEFT (narrow white filter rail): a "Kind" checkbox group with counts; a "Container" group (array, string, hash map, deque, grid); a "State" group using the real state words — Introduced / Applied / Discriminated / Retained / Integrated. A couple checked in teal. **No difficulty group, no "Mastered" option.**
  - RIGHT (wide results list): GROUPED sections with small mono headers `TECHNIQUE`, `TRANSFER EPISODES`, `COMPOSITIONS`, `PROBLEMS`. Each result is a white row card with a small teal kind icon, an ink title with the matched substring in teal, a one-line slate snippet, and a mono meta row. Critically, each problem result carries the **two chip rows** — `Container:` filled chips and `Movement:` as a slate #EEF2F0 chip reading "hidden in practice mode". Include: the canonical "Sliding window" technique; transfer episodes "string substrate", "flip-budget substrate", "monotonic-deque substrate"; compositions "LRU cache", "sliding window maximum"; and 4 problems. One row shows the mono route beneath it in slate — `/technique/sliding-window/string-substrate` — to make the URL model visible.
- A centered ghost "Load more".

IMPORTANT: results are grouped by KIND from the taxonomy (machinery / structure / technique / composition / problem), never by a flat "algorithms and lessons" split. Movement labels stay hidden on problem rows.

---

# 3. How to build the SVG (pass 3)

`[SPEC → research D-4, §18.1]` **SVG first**, up to ~150 elements — accessible, inspectable, and styleable by token. Move to Canvas 2D only where a measurement proves you must. Do not start with Canvas: you lose accessibility and token-driven styling for a performance problem you may not have.

## 3.1 The one rule that makes all three canvases cheap

The canvas is a **pure function of one `Frame`**. Never a mutable scene graph, never an animation timeline you advance imperatively.

```
render(frame: Frame) -> SVG
```

`[SPEC → research §11.1]` The engine's contract already gives you everything the canvas needs:

```ts
type VizStatus =
  | 'idle' | 'current' | 'visited' | 'frontier'
  | 'compared' | 'swapped' | 'final' | 'excluded'

interface VizNode { id: string; label: string; status: VizStatus; x: number; y: number }
interface VizEdge { from: string; to: string; status: VizStatus; weight?: number }
interface VizCell { id: string; value: number | string | null; status: VizStatus }
```

Consequences to respect, because they are what make screens 20 and 22 possible at all:

1. `VizNode` already carries `x` and `y`. Layout is the algorithm module's job, **not** the renderer's. The renderer maps model coords → viewBox units and nothing more.
2. Status is **semantic**. Components map `VizStatus` → a CSS class. `[SPEC → research §9.3]` Zero hex literals outside `styles.css`.
3. Because a frame is fully determined, reduced-motion support is free: render the frame with no transition. `[SPEC → research §18.2, R-8]`

## 3.2 Coordinate system and viewBox

Author in a fixed design space and let `viewBox` do all scaling. Never compute pixel sizes from `window.innerWidth`.

```
<svg viewBox="0 0 640 360" preserveAspectRatio="xMidYMid meet" class="viz">
```

- One design unit = one CSS px **at the reference size**, so the spacing scale stays legible while you author.
- Width/height come from CSS (`width: 100%; height: auto`), never from attributes. Responsive for free.
- `preserveAspectRatio="xMidYMid meet"` for graphs and trees. For the letter strip on screens 20/22, use `xMinYMid meet` so the strip stays left-anchored as it grows.

**Hairlines that survive scaling.** A 1px border drawn in a scaled `viewBox` becomes 1.4px or 0.7px and the whole design reads muddy. Fix it on every stroked element:

```
vector-effect="non-scaling-stroke"
```

## 3.3 Array / strip / grid geometry (screens 20, 22, 28)

Constant spacing, derived positions — never hand-placed coordinates.

```
CELL = 48        // cell edge
GAP  = 8         // gap between cells
PITCH = CELL + GAP            // 56 — the only number that matters
x(i)  = PAD + i * PITCH
W     = PAD * 2 + n * PITCH - GAP    // subtract the trailing gap
```

- Cell rect: `x=x(i) y=yTop width=CELL height=CELL rx=8`.
- Cell label: `x = x(i) + CELL/2`, `y = yTop + CELL/2`, with `text-anchor="middle" dominant-baseline="central"`. Those two attributes together are what actually centres text in SVG — do not fake it with a `dy` offset, it breaks across fonts.
- **Window tint** spanning `lo..hi` inclusive: `x = x(lo)`, `width = (hi - lo + 1) * PITCH - GAP`. Draw it *behind* the cells, first in document order (SVG has no z-index).
- **Pointer marker** under cell `i`: a triangle centred on `x(i) + CELL/2`, via `<path d="M cx-6 y  L cx+6 y  L cx y-8 Z">`.
- Grid (2-D): `x(c) = PAD + c * PITCH`, `y(r) = PAD + r * PITCH`. Same pitch both axes keeps cells square.

## 3.4 Graph and tree geometry (screens 22, 29)

**Edges must be trimmed to the node boundary,** or arrowheads vanish under the circles and weight labels collide with node fills. This is the single most common bug in hand-rolled algorithm visualizers.

```
dx = x2 - x1;  dy = y2 - y1
len = Math.hypot(dx, dy) || 1        // guard: coincident nodes
ux = dx / len;  uy = dy / len        // unit vector along the edge

// trim both ends by the node radius (+ head length at the target)
ax = x1 + ux * R
ay = y1 + uy * R
bx = x2 - ux * (R + HEAD)
by = y2 - uy * (R + HEAD)
```

**Curved edge** (needed when both `a→b` and `b→a` exist, otherwise they overlap exactly). Offset a quadratic control point along the perpendicular:

```
mx = (ax + bx) / 2;  my = (ay + by) / 2
px = -uy;  py = ux                   // perpendicular unit vector
K  = 24 * dir                        // dir = +1 / -1 per direction
d  = `M ${ax} ${ay} Q ${mx + px*K} ${my + py*K} ${bx} ${by}`
```

**Weight label** sits at the curve's midpoint pushed off the line, on an opaque backing rect so the edge does not strike through the digits:

```
lx = mx + px * (K/2 + 10);  ly = my + py * (K/2 + 10)
```

**Tree layout**, if a module hasn't supplied coordinates: `x` from in-order traversal index, `y` from depth.

```
x(node) = PAD + inorderIndex(node) * PITCH_X
y(node) = PAD + depth(node) * PITCH_Y      // PITCH_Y ≈ 72
```

This guarantees no two nodes share an `x` and no subtree crosses another — enough for the ≤ 150-element budget, and far simpler than Reingold–Tilford.

**Bipartite layout** (screen 29) is the easy case — fix `x`, distribute `y`:

```
xVerb = 120;  xNoun = 520
y(i, count) = PAD + i * ((H - 2*PAD) / Math.max(count - 1, 1))
```

## 3.5 Concept-map specifics (screen 29)

- Edge state maps to **both** stroke and dash, never colour alone `[SPEC → research §18.2]`:
  `solved` → `stroke: var(--teal); stroke-width: 2` · `available` → `stroke: var(--border); stroke-width: 1` · `untried` → same + `stroke-dasharray: 4 4; opacity: .5`.
- Draw order: edges group first, then nodes, then labels. Nodes must occlude edge ends.
- Hit targets: a 1px line is unclickable. Add a transparent `stroke-width: 12` sibling path as the pointer target, with `pointer-events: stroke` on it and `pointer-events: none` on the visible path.
- Selecting a verb dims the rest: put `data-selected="sliding-window"` on the root `<svg>` and let CSS do the dimming. No per-element JS updates.

## 3.6 Roadmap board specifics (screen 27)

- Map day → x with a single linear scale: `x(day) = PAD + (day - 1) * DAY_W`. A phase lane spanning days `a..b` is `x = x(a)`, `width = (b - a + 1) * DAY_W`. Duration becomes spatial automatically.
- Pan/zoom by mutating **only the `viewBox`** — never a CSS transform on the SVG, which would blur text and scale your hairlines.
- The braid arcs are backward-pointing quadratics: from a later lane's left edge to an earlier topic row, control point pushed *below* the lanes so arcs don't cross lane bodies.
- Put lane text in **HTML absolutely positioned over** the SVG rather than in `<text>`. SVG text will not wrap or ellipsize, and lane labels need both.

## 3.7 Accessibility of the canvas

`[SPEC → research §18.2]` "The explanation pane is the accessible narration of the canvas."

So the correct wiring is counter-intuitive and worth stating plainly:

```html
<svg aria-hidden="true" focusable="false"> … </svg>

<p id="explain" aria-live="polite" aria-atomic="true">
  The right edge moved in, so the window now contains a duplicate — shrink from the left.
</p>
```

- Mark the SVG `aria-hidden`. A screen reader crawling 150 `<circle>` elements produces noise, not understanding. The sentence *is* the accessible interface.
- `aria-live="polite"` on the explanation, so each step is announced. This is what makes the flagship screen usable rather than merely compliant.
- Every status needs an icon, shape, or text as well as colour — `current` gets a fill *and* a ring, `final` gets a check glyph. `[SPEC → research §17.6]`
- Keyboard: arrows step, `Home`/`End` jump to first/last frame; controls carry real accessible names.

---

# 4. SVG animation — highlighting the right way

## 4.1 The governing constraint

Frames are **discrete**. Animation therefore has exactly one legitimate job: *make the change between two frames legible*. It must never become the mechanism of playback.

`[SPEC → concept-page-spec §2.2]` Student-driven stepping, not autoplay — engagement is what produces the learning gain, and animation that plays on its own makes the student a spectator. `[SPEC → research §13]` Drive any timed advance with `requestAnimationFrame` + an accumulator, never `setInterval`, which drifts and misbehaves in background tabs.

## 4.2 Animate only compositable properties

Transitioning SVG geometry attributes (`x`, `cx`, `width`, `d`) forces layout and paint every frame and janks immediately. Transition `transform` and `opacity` only.

```css
/* window tint slides — transform, not x */
.viz-window {
  transform: translateX(calc(var(--lo) * var(--pitch) * 1px));
  transition: transform 180ms cubic-bezier(.2, .6, .2, 1);
}
```

Feed positions in as CSS custom properties from the frame, and let CSS interpolate:

```tsx
<rect className="viz-window"
      style={{ '--lo': frame.lo, '--pitch': 56 } as React.CSSProperties} />
```

The renderer stays a pure function of the frame; the tween is CSS's problem.

## 4.3 Traversal highlight: draw-on with `pathLength`

To show an edge being traversed, normalise the path length so you never call `getTotalLength()`:

```html
<path class="viz-edge is-traversing" pathLength="1" d="…" />
```

```css
.viz-edge.is-traversing {
  stroke-dasharray: 1;
  stroke-dashoffset: 1;
  animation: draw 260ms ease-out forwards;
}
@keyframes draw { to { stroke-dashoffset: 0; } }
```

`pathLength="1"` remaps the path's own coordinate system so `1` means "the whole path", whatever its real length. One rule works for a straight edge and a curve alike.

## 4.4 Pulse a node without moving it

```css
.viz-node[data-status="current"] .halo {
  transform-box: fill-box;      /* required — else transform-origin is the SVG root */
  transform-origin: center;
  animation: halo 420ms ease-out;
}
@keyframes halo {
  from { transform: scale(1);   opacity: .45; }
  to   { transform: scale(1.9); opacity: 0;   }
}
```

`transform-box: fill-box` is the non-obvious part. Without it, `transform-origin: center` resolves against the whole SVG viewport and the halo flies off across the canvas.

## 4.5 Interpolating a custom property (a real gotcha)

CSS custom properties are strings and do **not** interpolate by default — the transition in §4.2 will snap rather than glide unless the property is registered with a type:

```css
@property --lo {
  syntax: '<number>';
  inherits: false;
  initial-value: 0;
}
```

## 4.6 Don't let React restart your animations

Keying list items by array index remounts elements when the collection reorders, which restarts every animation and produces flicker.

```tsx
{frame.state.edges.map(e => (
  <Edge key={`${e.from}->${e.to}`} {...e} />     // stable identity
))}
```

Same for cells and nodes: key by `id`, never by index.

## 4.7 Hover parity (`concept-page-spec` §2.2 requirement 4)

"Hovering a code variable highlights it in the visualization, and vice versa." Implement with a shared token attribute plus one CSS rule — no state plumbing, no re-render:

```html
<span class="tok" data-token="lo">lo</span>          <!-- code pane -->
<g class="viz-pointer" data-token="lo"> … </g>       <!-- canvas -->
```

```css
.pane:has([data-token="lo"]:hover) [data-token="lo"] {
  outline: 2px solid var(--teal);
  outline-offset: 2px;
}
```

For the general case set `data-hl="lo"` on a common ancestor on hover and match `[data-hl="lo"] [data-token="lo"]`. One attribute write, zero React renders.

## 4.8 Predict-gate motion

At a gate the Next control is blocked `[SPEC → concept-page-spec §2.2]`. The motion must communicate *blocked*, not *broken*:

- Do **not** shake, flash red, or bounce. Failure is diagnostic in this product, never punitive (`content` §7 routes by error type, not score).
- Reveal the consequence *after* the answer commits, using the §4.3 draw-on so the student sees their prediction play out.
- Keep the gate's own transition ≤ 200ms; the reveal may run to ~400ms because it carries information.

## 4.9 Reduced motion — a promise four specs make

`[SPEC → research §18.2, §17.6, R-8]` "No autoplay, no tweening, instant frame swaps, stepping still fully available."

```css
@media (prefers-reduced-motion: reduce) {
  .viz *,
  .viz-window,
  .viz-edge,
  .viz-node .halo {
    animation: none !important;
    transition: none !important;
  }
}
```

And in code, not only in CSS — because CSS cannot stop a rAF loop:

```ts
const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches
if (reduced) autoplay = false     // stepping remains fully available
```

Test it. `research` R-8 lists "reduced-motion mode ships broken" as a live risk whose mitigation is that the frame model makes correct behaviour nearly free — the only way to waste that is to not check.

## 4.10 Duration budget

| What | Duration | Why |
|---|---|---|
| Status colour change | 120ms | Just enough to catch the eye |
| Pointer / window move | 180ms | Tracks a discrete step without lagging the student |
| Edge draw-on | 260ms | Direction must be readable |
| Halo pulse | 420ms, once | Never loops — a looping pulse becomes wallpaper |
| Predict-gate reveal | ≤ 400ms | Carries information, so it may be slower |
| Anything decorative | 0ms | Delete it |

Rule: if a student stepping quickly can outrun an animation, the animation is too slow. Stepping must never feel gated by motion.

---

# 5. Static image → static site: what carries over and what does not

The generated images from pass 2 are a **composition and hierarchy reference**. They are not a source of truth. Specifically:

| Carry over from the image | Never take from the image |
|---|---|
| Layout, proportion, visual hierarchy | Hex values — use the tokens in `styles.css` `[SPEC → research §9.3: zero hex outside styles.css]` |
| Spacing rhythm, card grouping | Copy text — image models misspell and invent; author copy in content files |
| Which element is dominant | Any node/edge coordinates — those come from `Frame`, §3.1 |
| Chip and control placement | Code inside code panes — it comes from `AlgorithmModule.source` |
| Icon *positions* | Icon shapes — use the project icon set at 16/20/24px |

Two hard rules:

1. **The canvas is never an image.** Screens 20, 22, 27 and 29 render from data. Tracing an AI-generated graph into SVG paths produces geometry that cannot animate, cannot be stepped, and cannot be made accessible.
2. **Build four shells, not fourteen pages.** `[SPEC → research R-3]` 14 hand-built screens will drift, and the C-2 sidebar conflict will ship twice. The shells: app shell (§0.2), concept shell (screen 19's definition, reused by 19–24), workspace shell (25, 26), canvas shell (20, 22, 27, 29).

## Build order

`[SPEC → research §21 Phase 1, concept-page-spec §5]` Do not build these in page-number order.

| Step | Build | Done when |
|---|---|---|
| 1 | `engine/types.ts` + the three-view panel (screen 22) with synced stepping and predict gates | Scrub to step 7 and the canvas, the line-6 highlight, and the sentence all agree — and adding a 4th algorithm needs one file and no UI change |
| 2 | Concept shell + stages 1, 2, 3, 5, 6 (screens 19, 20, 21, 23, 24) | Six stage dots, one primary action, invariant line correct per stage, no label leak on 24 |
| 3 | Item schema + 21 items for **two contrasting** concepts | Discriminate and Compose are real, not mocked |
| 4 | Session builder with the ≥ 3-concept / ≥ 2-rail assertion, then screen 17 | A monochrome session cannot be generated |
| 5 | Mastery event log + decay, then screens 26 and 29 | Overdue concepts re-enter Return automatically |
| 6 | Roadmap board (27), Return queue (28), Explore (18), Search (30) | Two chip rows everywhere; Movement hidden in practice mode |

`concept-page-spec` §5: do **not** broaden to 30 concepts before steps 1–5 are validated on two.

---

# 6. Acceptance checklist

Run this against every screen before calling it done. Each line is a quotation from a spec, not a preference.

- [ ] No percentage anywhere on a concept, and no per-concept "complete" state.
- [ ] Progress inside a concept is **six stage dots**.
- [ ] No topic sidebar inside a concept stage.
- [ ] Exactly one primary action per screen, bottom-right.
- [ ] The invariant line is visible on every stage from 3 onward — and deliberately withheld on stage 6.
- [ ] No technique label on screens 24, 25, 28, or on any problem row in 18/30 practice mode.
- [ ] Complexity is asked (screen 26), never printed as a badge.
- [ ] Every problem shows **two** chip rows — Container and Movement — never one.
- [ ] Explore groups under Machinery / Structures / Techniques; nouns and verbs are never siblings.
- [ ] Stepping is student-driven; autoplay is de-emphasised and off under reduced motion.
- [ ] Every `VizStatus` carries an icon/shape/text as well as colour.
- [ ] The explanation pane is an `aria-live` region and the SVG is `aria-hidden`.
- [ ] Zero hex literals outside `styles.css`; border is `#E4E9E7`, wash is `#E7F5F1`.
- [ ] Sidebar nav is the C-2 canonical eight items, from one array in one file.
- [ ] The roadmap shows plan-time, and states in copy that the plan is not a promise.
- [ ] No emoji — the streak flame is an icon `[SPEC → research C-5]`.

---

# 7. Still unresolved, and blocking

`[SPEC → research D-1]` **The stack decision is still open and it blocks Phase 0.** The repo is Next.js 16; the stated target is TanStack Start on Vite. There is no application code to migrate, so switching costs ~nothing today and grows with every screen written. Fourteen screens built before that call is risk R-5 arriving on schedule. Decide before building screen 22.

Open items inherited from `concept-page-spec` §6 that these screens must keep configurable, not hardcode: per-stage timings, the ~8-items-per-day cap, Return interval spacing, whether *Integrated* needs 3 Compose partners or 2, and whether stage 5 is completable on mobile at an acceptable rate. Every `[ESTIMATE]` above belongs in a config file so it can be changed by data rather than by opinion.
