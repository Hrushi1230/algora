# Algora — Learning Product Design Spec

**Status:** design system + screen architecture. **No image prompts in this document** — prompts come only after this is approved.
**Derives from:** `learning-design-research.md` (diagnosis + rules R1–R5), `concept-page-spec.md` (7 stages), `taxnomy-and-transfer.md` (two axes, bipartite map), `content.md` (braid, mastery states), `research.md` §9 (tokens).

**Decisions locked by the user for this pass:**
1. Gamification → **replaced** by the pairing map. XP, levels, leagues, demotion, 60 badges, quests, rewards shop are deleted.
2. Tri-pane → **sequenced across stages**, one dominant channel at a time.
3. Scope → **learning surfaces first**. Onboarding / account / admin realigned in a later pass.
4. Order → **this spec, then prompts.**

Every rule below carries the reason it exists. A rule with no reason is a rule that gets broken.

---

# Part I — The design language

## 1. What the design has to do

The research produced five rules. They map onto design decisions like this:

| Rule (from research) | Design consequence |
|---|---|
| R1 — learner acts at every step | Every screen has exactly one **committing control**. No screen is only readable. |
| R2 — push up the engagement taxonomy | Controls prefer *Changing* (issue an operation) and *Constructing* (build input) over *Responding*, and never stop at *Viewing*. |
| R3 — open a gap before answering | The answer is **physically absent from the DOM** until commit. Not greyed, not below the fold — absent. |
| R4 — one channel at a time | Layout archetype is chosen per stage; channels sequence rather than tile. |
| R5 — informational, not controlling | Progress = lit cells and named states. Never a rank, never a percentage, never a threat. |

## 2. Tokens — unchanged, plus one honest gap

Palette and type stay exactly as `research.md` §9.1/§9.2. Boredom was never the palette.

| Token | Hex | Use |
|---|---|---|
| `paper` | `#F7F9F8` | Page background |
| `card` | `#FFFFFF` | Elevated surfaces |
| `ink` | `#0E1513` | Headings, primary text |
| `slate` | `#5B6763` | Secondary text, labels |
| `teal` | `#0E9C86` | **The** accent — see §5.4 for its single job |
| `teal-hi` | `#14B8A6` | Hover/highlight step |
| `wash` | `#E7F5F1` | Tints, callouts, selected state |
| `border` | `#E4E9E7` | 1px hairlines — C-1 resolved, no exceptions |
| `empty` | `#EEF2F0` | Unlit / locked / disabled fills |

Type: **Instrument Sans** for headings, UI, body. **JetBrains Mono** for code and *all* numbers, costs, counts, step indices. Radius: cards 12–16px, buttons/inputs 8–10px. Body ≥14px, `leading-relaxed` in reading columns. Contrast comes from hairlines, not shadows.

**One token is genuinely missing, and it is load-bearing for this design.** This whole spec depends on the learner being *wrong on purpose* — broken invariants (§6.4), failed predictions (§7.3), violated preconditions. There is currently no token that can say "this broke." Using `teal` for both "correct/spotlight" and "broken" would destroy the accent's meaning.

**Proposal:** add one functional token, `clay = #C2603F` — a warm terracotta that sits inside the existing warm-neutral palette and never reads as festive or alarming. Total palette remains within budget: 3 neutrals (paper/ink/slate) + 1 accent (teal) + 1 functional (clay).

**This is a decision I need from you, not something I'll assume.** It is listed in §12.

## 3. Layout archetypes — four, deliberately different

The measured cause of the boredom was one skeleton on every screen (sidebar → headline+subline → three stat cards → one big white card → teal strip). That skeleton is retired. Four archetypes replace it, and a stage is **assigned** one:

**Archetype A — Full-bleed canvas.**
No card. The visualization *is* the page, edge to edge, on `paper`. Controls float as a single low bar or a corner cluster. Used when the object of study is the point.
→ Structure bench, technique duel, Play, the pairing map.

**Archetype B — Single quiet column.**
Max ~560px, centred, huge vertical air, no card border at all. One idea, a lot of silence. Used when the screen's job is to be *read once and remembered*.
→ Name, Hook framing.

**Archetype C — Working split.**
60/40 or 50/50. Left = the task or the artefact, right = the tool. Both panes are full-height; neither is a sub-card.
→ Build, Confuse.

**Archetype D — Bare-paper editorial.**
No cards. Content sits directly on `paper`, organised by typographic hierarchy and hairline rules only.
→ Roadmap board, session review.

**Hard rule:** archetypes A and B may not contain a nested visualizer sub-card. That nesting is what shrank the algorithm to an eighth of the viewport.

## 4. The rhythm score — the actual cure for monotony

A session must have a **shape**. If every stage is equally dense the session is a monotone, which is what we have now. Density is therefore *composed* across the seven stages:

| Stage | Archetype | Density | Dominant channel | Feels like |
|---|---|---|---|---|
| 1 Hook | B | low | the failing artefact | quiet unease |
| 2 Play | **A** | **peak visual** | canvas only | loud, hands-on |
| 3 Name | **B** | **minimum** | one sentence | a held breath |
| 4 Three views | **A** fused | **peak information** | canvas, annotated | dense, integrative |
| 5 Build | C | high working | code | focused labour |
| 6 Confuse | C | medium tense | two problems | a decision |
| 7 Return | B | low | one problem | cold recall |

The two peaks (2 and 4) are separated by the emptiest screen in the product (3). That contrast is not decoration — it is what makes the name land, and it is the single biggest anti-boredom device available at the layout level.

**Rule:** every screen has exactly one element occupying **≥55% of the viewport**. If everything is mid-sized, nothing is interesting.

## 5. Four art-direction rules

**5.1 Scale contrast is mandatory.** One dominant element per screen, everything else genuinely small. No more uniformly mid-sized cards.

**5.2 The stat-card reflex is banned.** Three equal white stat cards may not appear on any learning surface. A number that matters is set **large, bare, in mono, directly on paper**. A number that doesn't matter is one mono line at 12–13px. If a number needs a card to look important, it isn't.

**5.3 Rotate the container.** Consecutive screens may not share an archetype unless §4 says so. The card is not the default; `paper` is the default.

**5.4 Teal has exactly one job per screen.** Today teal marks nav, progress, buttons, links, badges, streaks, ranks and the logo simultaneously — so it signals nothing. During a concept, `teal` means **"the element currently under the spotlight"** and nothing else. Navigation active-state drops to `ink`; structural chrome uses `border`/`slate`. (Note: `research.md` §9.1 lists "XP" as a teal use — XP is deleted, so that use disappears with it.)

**5.5 Chrome is suppressed during a concept.** Per `concept-page-spec` §2.1, no topic sidebar during a concept — a visible topic list invites "let me finish all arrays first," the exact behaviour being removed. Nav returns *between* concepts. The stage indicator is dots showing **stage, not percentage**.

---

# Part II — The two grammars

This is the core of the redesign and the direct answer to *"how techniques, structures — what way?"* Giving both the same tri-pane was a category error. They are different kinds of knowledge, so they get visibly different screens.

## 6. Structure grammar — a workshop bench in space

A structure's identity is its **invariant** plus its **cost profile**. You learn it by doing things to it and being billed.

**6.1 Layout — Archetype A.** The structure sits centred and large on bare paper, ~60% of viewport. It is a **persistent object**: it does not replay or reset between actions, it *accumulates* state. Continuity is the whole point — this is one object being worked on over time, not a series of renders.

**6.2 The operations bench replaces the play button.** A single bottom bar of operation controls: `insert ⟨n⟩`, `pop`, `peek`, `union(a,b)`, `find(x)` — whatever the structure affords. Typed or stepped values, learner-chosen. This is Naps **Changing**, the level with evidence behind it. **There is no timeline, no scrub bar, no speed slider on a structure screen** — time is not this thing's axis.

**6.3 Cost is felt, then totalled.** Every operation visibly costs work: the touched nodes flash, and a mono **cost ledger** in the top-right accrues (`comparisons 14 · swaps 3 · nodes touched 21`). The ledger is the largest number on screen after the structure itself.

Complexity is **never printed as a badge**. At the end of the bench the learner is shown their own ledger against input size and asked to name the shape they just produced. Per `concept-page-spec` §2.2: complexity is *discovered in the operations lab*. A badge saying `O(log n)` before the learner has paid a single comparison is the exact "everything is pre-labelled" failure from the research.

**6.4 The invariant is a visible, breakable promise.** One line of mono at the top edge states it (`every parent ≤ both children`). The learner is *invited* to break it — drag a node into an illegal position. The structure resists, the offending relation renders in `clay`, and the invariant line shows which clause failed. **Breaking is the lesson**, so the illegal move must be reachable, not disabled.

**6.5 What a structure screen must NOT have:** a timeline, a speed slider, an autoplay button, a complexity badge, a difficulty chip, a code pane during Play, or the structure rendered inside a sub-card.

## 7. Technique grammar — a duel in time

A technique's identity is its **decision rule** plus its **precondition**. You learn it by predicting its next move and being wrong.

**7.1 Layout — Archetype A, but the pixels go to the decision.** The container the technique walks over is rendered *plainly* — a technique screen must not fetishise its array. The spend goes on the decision point, the trace, and the reveal.

**7.2 The trace is the artefact, and it persists.** Every step the technique takes stays drawn: pointer positions visited, edges walked, cells compared, all accumulating as a readable history in fading `wash`. The current step is the only `teal` element. An animation that erases itself leaves nothing to reason about; a trace can be read backwards.

**7.3 Stepping is a commitment, not transport.** This is the most important interaction in the product. The primary control is **not** "next". It is:

> **"Which move would you make?"** → learner commits (clicks a candidate, or picks *expand right* / *shrink left*) → the true move is revealed → if they missed, one line says *why*.

The true next state is **absent from the DOM until commit** (R3). Predict-before-reveal already exists in `concept-page-spec` §2.2; this makes it the spine rather than a gate. After two correct consecutive predictions the gate relaxes to plain stepping — the learner has demonstrated the rule and further gating becomes friction.

**7.4 Failure is a first-class view, not an error state.** Every technique screen can run the technique on input that **violates its precondition** — binary search on unsorted data, two pointers on unordered input — and let it produce a confidently wrong answer, drawn in `clay`. The precondition becomes memorable because the learner watched it matter. This is a deliberate, reachable mode, not a bug.

**7.5 What a technique screen must NOT have:** autoplay as the default, the technique's name during Play, a difficulty chip, a self-erasing animation, or prose narrating what the canvas is already showing.

## 8. Channel sequencing — how the tri-pane dies

Per the locked decision, viz/code/prose **sequence** rather than tile:

| Stage | Canvas | Code | Prose |
|---|---|---|---|
| 1 Hook | the failing artefact | none | one framing line |
| 2 Play | **everything** | **forbidden** | the predict prompt only |
| 3 Name | none, or one frozen still | none | **name + one invariant sentence** |
| 4 Three views | **dominant** | inline annotation | one interrupt line |
| 5 Build | reference, secondary | **dominant** | task + hint ladder |
| 6 Confuse | two small stills | none | the question |

**Stage 4 is the one place all three legitimately meet** — it is the integration stage. But it is still **not three equal panes.** It is *one canvas with the code as an annotation attached to it*: the executing line renders in a mono strip docked to the canvas region it controls, so the eye never travels between two separately-scanned panes. This is physical integration, the actual documented fix for split-attention — adjacency is not integration.

**Prose never narrates.** It interrupts, once, at the moment of surprise, then leaves. A sentence that describes what the animation already shows is the redundancy effect in action and must be cut.

## 9. The pairing map — what replaces gamification

XP, levels, leagues, promotion/demotion, 60 badges, quests and the rewards shop are **deleted**. This surface replaces all of them, per `taxnomy-and-transfer.md` §6: *"lit edges = cells the student has actually solved."*

**9.1 It must be sparse, not a 340-cell grid.** Axis N has 17 structures, Axis V has 20 techniques. A full matrix is 340 cells and most are meaningless — "bit tricks × graph" is not a pairing anyone should be nudged toward. **Only valid pairings are rendered as cells** (roughly 70–90). Invalid combinations are not empty cells, and not struck-through cells; they are simply *absent*, so the map never implies an obligation that doesn't exist. Filling a grid is farming — the exact behaviour R5 removes.

**9.2 Cell states — four, no percentages:**

| State | Fill | Means |
|---|---|---|
| Unlit | `empty` | never shipped |
| Once | `wash` | solved once — **fragile**, not known |
| Transferred | `teal` | solved on ≥2 different containers |
| Decayed | `wash` + `clay` hairline | was known, past its Return interval |

The `Once` → `Transferred` distinction is the entire pedagogical payload: a technique is only truly known when **several edges from it are lit**. One lit cell must never look like an achievement.

**9.3 Layout — Archetype A or D, pan/zoom.** Techniques down one side, structures across the other. Row density is readable at a glance, so the map's headline finding is legible without reading a single label: *"you've only ever run sliding window on arrays."*

**9.4 It states gaps, never ranks.** The one piece of generated copy is a factual observation of the sparsest row — no comparison to other learners, no "you're behind", no completion figure. Informational, not controlling (R5).

**9.5 Mastery states are named, never numeric.** Per `content.md`: Introduced → Applied → Discriminated → Retained → Integrated, and only *Integrated* counts as mastered. These render as **words in mono**, never as a bar or a percentage. `Integrated` requires ≥3 Compose passes with *different* partners over ≥3 weeks — unreachable by grinding one concept, by construction.

## 10. The roadmap board — time as a plan, mastery as truth

Position already agreed and unchanged: **time is a plan, mastery is the truth.**

**10.1 Archetype D**, a board of **sessions** — not a progress tracker. Phase lanes run horizontally; each card is one sitting and states **what you will do** (`Heap · bench + build`), never what fraction you'll complete.

**10.2 May show:** day/week structure, a daily time budget, today's marker, what's scheduled next.
**10.3 May never show:** a per-concept percentage, an aggregate completion figure, a projected mastery date, or a "you are behind" state. A required line of copy states that dates are a plan and mastery is measured separately.

**10.4 Return items on the board are unlabeled.** Per `content.md` and `taxnomy-and-transfer` §5, a Return card tagged "Graphs · BFS" hands over the answer — the tag *is* the answer. Return cards show the problem only.

## 11. Motion — highlighting, never decoration

Per `research.md` §18.2, animation is a highlighting tool. It may mark exactly three things:

1. **state change** — what just changed as a result of an action
2. **causality** — this pointer moved *because* that condition broke
3. **cost** — the work an operation just billed

Everything else is banned: no ambient drift, no parallax, no entrance animations on static content, no looping idle motion. All motion respects `prefers-reduced-motion`, where transitions resolve to instant state changes with no loss of information. Durations stay short (120–240ms for state, up to ~400ms for a trace draw) — long enough to be seen, never long enough to be waited on. A learner who is stepping must never wait for an animation to finish.

---

# Part III — Consequences

## 12. Open decisions — I need these before prompts

| # | Decision | Why it blocks |
|---|---|---|
| D-a | **Add `clay = #C2603F`?** (§2) | Broken invariants, failed predictions and decay have no colour without it. Whole design depends on being wrong safely. |
| D-b | **Delete or rewrite `gamification.md`?** | It still specifies XP/leagues/badges as authoritative. Both files can't be true. |
| D-c | **`onboarding.md` still promises "Est. completion · 7 weeks" and a % path** | Contradicts §10.3. In scope for the *next* pass — confirm it can be changed then. |
| D-d | **`research.md` D-1: Next.js 16 vs TanStack Start** | Still open from two passes ago. Blocks all build work; cost of switching rises per screen. |

## 13. What gets deleted

So the removal is explicit and reviewable: XP, levels, level-up moments, leagues, promotion/demotion zones, the 60-badge set, badge "Earned" dates, quests, the rewards shop, "Mark as complete", per-concept percentages, "Mastered · N" counts, estimated completion dates, difficulty chips, up-front complexity badges, playback bars, timeline scrubs, speed sliders, the three-stat-card row, and the topic sidebar during a concept.

Streak is **not** in that list — a gentle return cadence survives as *informational*, but it never threatens, never ranks, and never appears during a concept.

## 14. Screen inventory for the design pass

Learning surfaces only, per the locked scope. Prompts get written for these once §12 is settled.

| # | Screen | Archetype | Grammar |
|---|---|---|---|
| 1 | Hook — the wall | B | shared |
| 2 | Play — structure bench | A | §6 |
| 3 | Play — technique duel | A | §7 |
| 4 | Invariant break | A | §6.4 |
| 5 | Cost ledger → complexity reveal | A | §6.3 |
| 6 | Predict-before-reveal, missed | A | §7.3 |
| 7 | Precondition violation | A | §7.4 |
| 8 | Name | B | §8 |
| 9 | Three views, fused | A | §8 |
| 10 | Build — Parsons → faded → write | C | hint ladder |
| 11 | Confuse — unlabeled contrast pair | C | labels hidden |
| 12 | Pairing map | A/D | §9 |
| 13 | Roadmap board | D | §10 |
| 14 | Return item, unlabeled | B | §10.4 |

**Design review test** — a screen passes only if all five hold:
1. One element ≥55% of viewport.
2. Exactly one committing control; the screen is not merely readable.
3. No answer present in the DOM before commit.
4. One dominant channel; no prose narrating the canvas.
5. No percentage, rank, difficulty chip or up-front complexity anywhere.
