# Concept Spec — Learning Order, Page Anatomy, and Problem Counts

This document answers three questions in plain terms:

1. **In what order does a student learn one concept?** → Section 1
2. **What does the page look like at each step?** → Section 2
3. **How many problems per concept, and how are they spread out?** → Section 3

Companion to `content.md` (curriculum architecture) and `content-research.md` (learning-science basis).

Evidence tags used here: `[RESEARCH]` = supported by published education research · `[DERIVED]` = logical consequence of our design · `[ESTIMATE]` = our judgement, must be validated with real learner data.

---

# 1. The order a student learns ONE concept

## The one-line rule

> **Feel the problem → play with the structure → name it → see three views → build it → be confused on purpose → prove it later with other concepts.**

The critical part is the last step. A concept is **not finished on the day it is taught.** It finishes weeks later, inside problems that also need other concepts.

## The 7 stages

| # | Stage | Student is doing | Time `[ESTIMATE]` | Pass condition |
|---|---|---|---|---|
| 1 | **Hook** | Solving a small task with only their old tools, and hitting the wall | 2 min | Feels the cost/limit |
| 2 | **Play** | Dragging/stepping the structure with no name and no code | 5 min | Predicts the next state correctly twice |
| 3 | **Name** | Reading the name + one-sentence invariant | 1 min | Restates invariant |
| 4 | **Three views** | Stepping visualization + code + English together | 8 min | Traces unseen input correctly |
| 5 | **Build** | Parsons → faded example → full write | 15 min | Writes it once, unassisted |
| 6 | **Confuse** | Contrast pair vs nearest neighbour, labels hidden | 6 min | Picks correct approach and says why |
| 7 | **Prove (over weeks)** | Return / Discriminate / Compose slots in later sessions | months | 3 Compose passes with 3 different partner concepts |

Stages 1–6 are one sitting, roughly 35–40 minutes `[ESTIMATE]`. Stage 7 is scheduled by the system, never by the student.

## Why this exact order

| Order decision | Reason |
|---|---|
| Problem before solution | Learners retain a tool better when they first felt the need for it `[RESEARCH]` |
| Play before naming | Builds the mental model before vocabulary load; avoids "knows the word, not the idea" |
| Visual + code + words in lockstep | Active engagement with visualization beats passive watching `[RESEARCH]` |
| Parsons before free coding | Removes syntax load so attention goes to structure `[RESEARCH]` |
| Faded guidance | Full example → partial → blank is stronger than jumping to blank `[RESEARCH]` |
| Contrast immediately after building | Selection skill only trains when two options look similar `[DERIVED]` |
| Labels hidden from stage 6 onward | Real interviews never say "this is a sliding window" `[DERIVED]` |
| Mastery only at stage 7 | Stops the student from grinding one topic to "100%" `[DERIVED]` |

---

# 2. How the page should be built

## 2.1 Global shell (same on every stage)

```
┌──────────────────────────────────────────────────────────┐
│ TOP BAR                                                  │
│  ← Back    Concept: Sliding Window    Stage 4 of 6  ●●●○○○│
│            Rail: Technique                                │
├──────────────────────────────────────────────────────────┤
│                                                          │
│                    STAGE BODY                            │
│              (changes per stage, see below)               │
│                                                          │
├──────────────────────────────────────────────────────────┤
│ BOTTOM BAR                                               │
│  Invariant reminder (1 line)          [ Continue → ]     │
└──────────────────────────────────────────────────────────┘
```

Rules for the shell:

- **One primary action only**, bottom-right. Never two equal buttons.
- **Progress dots show the stage, not a percentage.** No "87% complete" — percentages imply the concept can be finished, which contradicts stage 7 `[DERIVED]`.
- The invariant line is always visible after stage 3. It is the single sentence the student must never lose.
- No sidebar of topics during a concept. A visible topic list invites "let me finish all arrays first," which is the behaviour we are removing `[DERIVED]`.

## 2.2 The signature layout: the three-view panel (stage 4)

This is the product. It must be the most polished screen.

Desktop (≥1024px):

```
┌─────────────────────────┬──────────────────────────┐
│  VISUALIZATION          │  CODE                    │
│  array cells, L/R       │  line 4 highlighted      │
│  pointers, window tint  │  current vars in gutter  │
│                         │                          │
├─────────────────────────┴──────────────────────────┤
│  PLAIN ENGLISH                                      │
│  "The right edge moved in, so the window now        │
│   contains a duplicate — shrink from the left."     │
├─────────────────────────────────────────────────────┤
│  ⏮  ◀  ▶  ⏭    step 7 / 19    speed ○──●──○         │
└─────────────────────────────────────────────────────┘
```

Mobile (<768px): stack in this order — visualization, English, code. English sits second because on a small screen the sentence is what carries the meaning `[DERIVED]`.

Hard requirements for this panel:

1. **One step = one change in all three panes.** If code advances a line, the visualization moves and the sentence rewrites. A desync here destroys the whole thesis.
2. **Student-driven stepping, not autoplay.** Autoplay animation is passive; engagement is what produces the learning gain `[RESEARCH]`.
3. **Predict-before-reveal gates.** At 2–3 chosen steps, block the Next button and ask "what happens next?" This converts watching into retrieval practice `[RESEARCH]`.
4. **Hover parity.** Hovering a code variable highlights it in the visualization, and vice versa.
5. Complexity is **not** printed as a badge. It is discovered in the operations lab and asked in Rail E `[DERIVED]`.

## 2.3 Stage-by-stage body layout

| Stage | Layout | Must have | Must NOT have |
|---|---|---|---|
| 1 Hook | Single centered card, small input, live counter | Visible failure (too slow / too much memory) | Concept name, code |
| 2 Play | Full-width canvas, drag handles, minimal chrome | "Predict next state" prompt | Any code pane |
| 3 Name | One quiet screen: name + invariant sentence | Restate-in-your-words input | A wall of theory text |
| 4 Three views | The panel above | Step control, predict gates | Autoplay-only |
| 5 Build | Split: left = task, right = editor / Parsons tray | Hint ladder (3 rungs), run + tests | Visible full solution |
| 6 Confuse | Two problems side by side, no labels | "Which approach, and why?" + short justification box | The word "sliding window" anywhere on screen |

## 2.4 The hint ladder (used in stage 5 and every later problem)

Three rungs only, and each costs something in the mastery signal, not in points:

1. **Conceptual** — "which invariant is being broken?"
2. **Structural** — subgoal labels for the solution's steps.
3. **Near-solution** — the loop skeleton with the key line blank.

There is never a "reveal answer" button before an attempt exists `[DERIVED]`.

## 2.5 Session page (what the student sees between concepts)

After the Focus concept, the session continues into other concepts. The screen shows the **braid**, so variety is visible:

```
Today's session
 ● Focus        Sliding Window            new
 ○ Return       Hash Map           last seen 9 days ago
 ○ Discriminate Two Pointers vs Sliding Window
 ○ Compose      Sliding Window + Hash Map
```

The student cannot delete a Return or Compose slot. They can reorder them `[DERIVED]` — autonomy over sequence, not over whether retention happens.

---

# 3. How many problems per concept

## 3.1 The honest answer

There is no researched magic number, and any product claiming one is guessing. Our count is **derived from what the schedule must be able to fill**, not from a frequency study `[DERIVED]`. It is a *floor*, and it is spread across months.

## 3.2 Per core concept: 21 items minimum

| Item type | Count | Used in | Why this count |
|---|---:|---|---|
| Trace / predict-the-state | 3 | Stage 4 + cheap Returns | need fresh inputs on each Return |
| Parsons / reorder | 2 | Stage 5 | one guided, one unaided |
| Faded worked example | 2 | Stage 5 | partial, then blank |
| Canonical application | 2 | Stage 5 end | one in-lesson, one held back |
| Contrast partner | 2 | Stage 6 | a pair is impossible with one |
| Transfer variant (different surface story) | 3 | Compose + unlabeled Return | 3 partners ⇒ 3 variants |
| Broken solution to repair | 2 | Rail E | debugging is a tested dimension |
| Generated-code review | 1 | Rail E | AI-era verification skill |
| Complexity / trade-off prompt | 2 | Rail E | before and after a requirement change |
| Requirement-change follow-up | 2 | interview realism | the "now make it streaming" turn |
| **Total** | **21** | | |

Tier adjustments `[ESTIMATE]`:

| Tier | Items | Example |
|---|---:|---|
| Core | 21 | hash map, BFS, sliding window, binary search |
| Extended | 12 | tries, union-find, monotonic stack |
| Specialist | 6 | segment tree, advanced DP shapes |

## 3.3 How many the student actually *solves* — and when

This is the part that answers "one concept to how many problems."

| Phase | When | Items from this concept | Labels shown? |
|---|---|---:|---|
| Learning day | day 0 | 6–8 | yes, from stage 3 |
| First return | ~day 2 | 1 | no |
| Second return | ~day 9 | 1–2 | no |
| Discriminate | week 2–3 | 1 pair | no |
| Compose #1 | week 2–4 | 1 | no |
| Compose #2 | week 4–7 | 1 | no |
| Compose #3 | week 6–10 | 1 | no |
| Decay re-entry | whenever overdue | 1 | no |

**≈ 8 items on the learning day, ≈ 7 more spread over 6–10 weeks.** `[ESTIMATE]` on the intervals; the *shape* — few now, more later, spaced — is `[RESEARCH]`-backed by spacing and retrieval-practice findings, where reported benefits commonly fall around d ≈ 0.5–0.85 and grow at longer delays.

## 3.4 The structural rule that stops single-concept grinding

Three enforcement points, in code, not in copy:

1. **Session assertion** — every generated session must contain **≥ 3 distinct concepts** and **≥ 2 rails**, or it is regenerated.
2. **Daily cap per concept** — after ~8 items of one concept in a day, further items of that concept are refused; the student is offered Return/Compose on others `[ESTIMATE]` on the number, hard on the principle.
3. **Mastery is unreachable alone** — a concept reaches *Integrated* only after **3 Compose passes with 3 different partner concepts, over ≥ 3 weeks**. No amount of same-concept practice can produce it.

So the answer to "how many problems for one concept" is deliberately not a number the student can farm in one day. It is ~8 today, and the rest is earned in the company of other concepts.

## 3.5 What the student never sees

- A per-concept percentage or "concept complete" state.
- A topic list with checkboxes that can be finished top to bottom.
- A pattern label on any problem after stage 6.
- A calendar promise ("master DSA in 12 weeks") — we have no completion data to justify one.

---

# 4. Worked example: Sliding Window (variable size)

| Stage | Concrete content |
|---|---|
| 1 Hook | "Longest substring with no repeats." Give them only nested loops. Show the timer blow up at n = 10⁵. |
| 2 Play | Two draggable edges over a strip of letters. A tint marks the window. Ask: "what must be true inside the tint?" |
| 3 Name | Sliding window. **Invariant: the window always satisfies the condition; the right edge expands, the left edge repairs.** |
| 4 Three views | Step 7: right edge takes a duplicate `b`. Code highlights the `while` line. English: "condition broken — shrink from the left until it holds again." |
| 5 Build | Parsons with the expand/shrink lines shuffled → faded version with the shrink loop blank → full write. |
| 6 Confuse | Paired with a sorted-array two-pointer problem, both unlabeled. "Which one, and what is the tell?" Tell: *contiguity requirement* vs *sorted order*. |
| 7 Prove | Compose with hash map (character counts), then with queue/monotonic deque (window maximum), then with prefix sums (fixed-window average). Three different partners ⇒ Integrated. |

Rail E items attached: complexity before/after "what if the alphabet is unbounded?"; a broken version whose left pointer advances unconditionally; a generated solution that is correct but O(n²) due to a rebuilt set each step.

---

# 5. Build order for the team

| Step | Deliverable | Why first |
|---|---|---|
| 1 | Three-view panel with synced stepping + predict gates | It is the differentiator; everything else is packaging |
| 2 | Item schema + 21 items for **two** contrasting concepts | Two concepts is the minimum that makes Discriminate and Compose real |
| 3 | Session builder with the ≥ 3-concept assertion | The anti-grinding guarantee must exist before content scales |
| 4 | Mastery event log + decay | Without decay the mastery display is a lie |
| 5 | Hint ladder + error-type routing | Turns failure into a next action instead of a score |

Do **not** broaden to 30 concepts before steps 1–5 are validated on two.

---

# 6. Open items (must be measured, not assumed)

1. Real per-stage timings — the 35–40 minute figure is an estimate.
2. The 8-items-per-day cap — tune against fatigue and success-band data.
3. Return interval spacing — start from standard spacing schedules, then fit to observed forgetting.
4. Whether 3 Compose partners is the right Integrated bar, or whether 2 suffices.
5. Whether mobile students can complete stage 5 at acceptable rates, or need a Parsons-only mobile path.

Every number above tagged `[ESTIMATE]` should live in a config file so it can be changed by data rather than by opinion.
