# Algora — Learning Product Design Research

**Status:** research only. No image prompts, no screens, no code in this document.
**Purpose:** work out *why* the current design reads as complicated and boring, what the evidence says a learning surface should actually do, and what design grammar follows from that. Design comes after this is agreed.

**Method:** every claim below is either (a) traced to a line in this repo, or (b) traced to published findings from the algorithm-visualization and multimedia-learning literature. Where something is my judgement call rather than evidence, it is marked **[JUDGEMENT]**.

---

## 1. The diagnosis — six named mechanisms

Not "it looks bad." Six specific, separable causes. Fixing the paint won't fix any of them.

### 1.1 Every screen is the same screen — structurally, not just stylistically

Measured across the existing prompt files:

| Repeated element | Occurrences |
|---|---|
| `persistent LEFT SIDEBAR` (240px, 7–8 nav items) | 13 prompts |
| `ink headline` + slate subline header block | 19 prompts |
| `pale-teal tint` strip / surface | 21 prompts |
| `row of THREE white stat cards` | every gamification screen |
| "one large dominant white card" as the body | ~all app screens |

Every app screen resolves to the identical skeleton: **sidebar → top bar → headline+subline → three stat cards → one big white card → pale-teal strip at the bottom.** Five gamification screens, one template. Fourteen learning screens, one template.

This is the single largest cause of the boredom, and it is a *layout rhythm* problem, not a colour problem. When each screen has the same silhouette, the eye learns the silhouette after two screens and stops looking. Nothing is ever *bigger* than anything else across screens; there is no crescendo, no full-bleed moment, no quiet moment. It reads as an admin console that happens to contain algorithms.

### 1.2 The interesting thing is the smallest thing on screen

Current concept screen nests the actual algorithm three containers deep: page background → white card → visualizer sub-card. In `onboarding.md` prompt 15 the tree that the entire question is *about* is a "small WHITE visualizer sub-card" in the left half of a centred wizard card — so the object of study occupies roughly an eighth of the viewport, while chrome (sidebar, top bar, stepper, footer, stat cards) occupies the majority.

The product's whole promise is *"See the algorithm think."* The algorithm is currently a thumbnail.

### 1.3 The tri-pane splits attention three ways at once

`concept-page-spec` mandates viz + code + prose simultaneously. This runs directly into two established effects:

- **Split-attention effect** — when learners must mentally integrate separate sources that are unintelligible in isolation, load rises; the fix is physical and temporal integration, not adjacency.
- **Redundancy effect** — presenting the *same* information in two channels at once (prose narrating exactly what the animation shows) overloads rather than reinforces; learning is often better with the redundant channel removed.
- **Coherence principle** — removing unneeded visual/verbal material improves learning.

Three synchronised panes saying the same thing is the textbook redundancy case. It *feels* generous and is actually taxing — which is exactly the "complicated" complaint. **[JUDGEMENT]** The panes should be sequenced or fused, not tiled.

### 1.4 Passive viewing is the default, and passive viewing does not work

This is the most important finding in the field and it invalidates the current core loop:

> Hundhausen, Douglas & Stasko (2002), meta-study of 24 experiments: the effectiveness of algorithm visualization is determined **more by how students use it than by what they see**. Merely watching an animation showed **no consistent learning advantage** over conventional materials. Value appears when students construct inputs, make predictions, answer questions, or build their own visualizations.

Naps et al.'s **engagement taxonomy** grades interaction: *No viewing → Viewing → Responding → Changing → Constructing → Presenting*. The current design lives almost entirely at **Viewing**, with a playback bar, a timeline scrub and a speed slider — controls for *watching more comfortably*.

A beautiful animation with a scrub bar is a screensaver with extra steps. It is boring because the learner has nothing to do.

### 1.5 Motivation is bolted on from outside, which is an admission the core isn't interesting

`gamification.md` supplies XP, levels, streaks, leagues, promotion/demotion zones, 60 badges, quests, a rewards shop. This is a large machine whose only job is to make someone return to a loop that isn't compelling on its own.

The evidence is genuinely mixed, and I won't overstate it: rewards framed as *informational* (telling you something true about your competence) can sustain motivation. But rewards that feel *controlling* trigger the **overjustification effect** — reducing interest in a task that was intrinsically interesting — and longitudinal gamification studies commonly find badges and leaderboards producing *declining* motivation, empowerment and satisfaction over time. Leagues with demotion zones are the controlling kind.

There is also a direct contradiction with the newer specs — see §7.

### 1.6 Everything is pre-labelled, so nothing can ever be discovered

Curiosity is, per Loewenstein's **information-gap theory**, a cognitively induced deprivation: it spikes when a gap is made *salient* and collapses once filled. Surprise that resolves a **prediction failure** measurably boosts memory.

The current design systematically forecloses every gap before it opens:
- the technique is named in the breadcrumb, the sidebar, the title, and a difficulty chip
- complexity is printed as a badge before you've felt a single operation
- the "correct" answer path is visible as a highlighted node

If the screen tells you it's BFS, tells you it's O(V+E), and tells you it's Medium, there is no gap left. Nothing to wonder about, nothing to be wrong about. **That is the definition of boring** — and it's why the fix is pedagogical structure, not visual polish. `concept-page-spec` already half-recognises this with predict-before-reveal gates, but the surrounding chrome leaks every answer.

---

## 2. What the evidence says to build instead

Distilled to five load-bearing rules:

| # | Rule | Grounding |
|---|---|---|
| R1 | The learner must **act at every step**; viewing is never the terminal state | Hundhausen meta-study; Naps taxonomy |
| R2 | Push each interaction **up the taxonomy** — prefer Changing/Constructing over Responding, Responding over Viewing | Naps et al. |
| R3 | **Open a gap before giving the answer.** Prediction, then reveal, then explain the miss | Loewenstein; prediction-failure/surprise memory findings |
| R4 | **One channel at a time.** Fuse or sequence viz/code/prose; never narrate the animation in parallel | split-attention, redundancy, coherence |
| R5 | Progress signals must be **informational, not controlling** — say something true about capability, never rank or threaten | overjustification / gamification longitudinal findings |

---

## 3. The core reframe

**Current mental model:** a course made of screens, each screen containing a visualization, wrapped in a dashboard, motivated by points.

**Proposed mental model** **[JUDGEMENT]**: a sequence of **situations the learner cannot resolve without building the idea.** The visualization is not the content — it is the *evidence surface* the learner interrogates while resolving the situation. The screen's job is to pose, withhold, respond, and only then name.

Consequences:
- The dominant object on screen is the thing under study, at **full bleed** — not a sub-card.
- Chrome is **suppressed during a concept** (already required by `concept-page-spec`: no topic sidebar) and returns between concepts.
- Prose does not narrate; it **interrupts** — one short line at the moment of surprise.
- Naming is a **reward**, delivered after the learner has already felt the pattern.

---

## 4. Techniques vs Structures — the question you actually asked

This is where the current design makes its deepest error, and it's the biggest single lever on both "complicated" and "boring."

`taxnomy-and-transfer.md` establishes the two axes — **Structures** (nouns: array, heap, graph, DSU) and **Techniques** (verbs: two pointers, binary search, DFS, DP). The current design gives **both the identical tri-pane treatment.** That is a category error, because they are not the same kind of thing and are not learned the same way.

### 4.1 A structure is a thing in *space*

Its identity is its **invariant** ("the parent is always ≤ its children") plus its **cost profile** (what's cheap, what's ruinous). You understand a structure by *doing things to it and being billed for them.*

Design grammar that follows:
- **Persistent object.** The structure stays on screen, centred, large, stable. It does not replay; it *accumulates state*.
- **An operations bench, not a play button.** The learner issues operations (`insert 7`, `pop`, `union(3,8)`). This sits at Naps **Changing** — the level with evidence behind it.
- **Cost is felt, then summarised.** Each operation visibly costs work; a running tally accrues. Complexity is *derived from the learner's own tally at the end*, never printed as a badge up front. `concept-page-spec` already demands this — "discovered in the operations lab."
- **The invariant is a visible, breakable promise.** Let the learner attempt an illegal move; the structure resists and shows *why*. Breaking is the lesson.
- **Time is not the axis** — so no timeline, no scrub bar, no speed slider on a structure screen.

### 4.2 A technique is a motion through *time*

Its identity is the **decision rule at each step** ("if sum is too small, move the left pointer") plus its **precondition** ("requires sorted"). You understand a technique by *predicting its next move and being wrong.*

Design grammar that follows:
- **The trace is the artefact.** The path taken is drawn and *persists* — a visible history you can read backwards, not an animation that erases itself.
- **Stepping is a decision, not a transport control.** The primary control is not "next"; it is *"which move would you make?"* — the learner commits, then the true move is revealed. Naps **Responding**, plus R3's gap.
- **Failure is a first-class view.** Run the technique on input that violates its precondition and let it produce a wrong answer. The precondition becomes memorable because the learner watched it matter.
- **Space is not the axis** — a technique screen shouldn't fetishise the container it walks over; render the container plainly and spend the pixels on the decision.

### 4.3 Why this fixes the boredom

Different kinds of knowledge get **visibly different screens.** Structure screens feel like a workshop bench: stable object, tools, an accruing bill. Technique screens feel like a duel: a decision, a commitment, a reveal, a trace left behind. Sameness dies here — not because we varied the colours, but because the two are genuinely different activities.

It also fixes the taxonomy bug already flagged in the repo: nouns and verbs stop being siblings in a flat grid, because they no longer even share a layout.

### 4.4 And the pairing is the third thing

Neither axis alone is competence. `taxnomy-and-transfer` §6's bipartite map exists because the real skill is **choosing a pairing** — "binary search *over* a sorted array", "DFS *over* a graph". That deserves its own surface: a matrix/graph of verb × noun where a cell lights only when the learner has actually shipped that pairing. It is simultaneously the anti-confusion and anti-grinding device, and it's the honest answer to "what have I got?" — replacing XP entirely (R5).

---

## 5. Layout and art direction — fixing "boring" without changing the palette

The palette is fine and stays: paper `#F7F9F8`, white cards, ink `#0E1513`, slate `#5B6763`, one teal `#0E9C86`, hairline `#E4E9E7` (C-1), Instrument Sans + JetBrains Mono. **Boring is not coming from the colours. It is coming from uniform rhythm and timid scale.** Four changes:

1. **Scale contrast.** Give each screen one unmistakably dominant element occupying ≥55% of the viewport, and let everything else be genuinely small. Today everything is mid-sized, which is the visual equivalent of a monotone.
2. **Kill the stat-card reflex.** Three equal stat cards is the laziest available layout and it appears on nearly every screen. Numbers that matter should be *typographically* large and bare on paper; numbers that don't matter should be one mono line, not a card.
3. **Vary the container.** Rotate deliberately between: full-bleed canvas (no card at all), single centred column, split 60/40, and bare-paper editorial. **[JUDGEMENT]** A canvas that bleeds to the viewport edge is the highest-impact single change available — it makes the algorithm the environment rather than a widget.
4. **Teal carries one job per screen.** Right now teal marks active nav, progress, buttons, links, earned badges, streaks, ranks and the logo — simultaneously. When the accent is everywhere it signals nothing. During a concept, teal should mean **"the thing currently under the spotlight"** and almost nothing else.

**Motion.** Per `research` §18.2, animation is a highlighting tool, not decoration; everything respects `prefers-reduced-motion`. Motion should mark *state change and causality* — the operation you just paid for, the pointer that just moved — never ambient drift.

---

## 6. Time-wise roadmap — carried forward from the agreed position

Position already agreed: **time is a plan, mastery is the truth.** The roadmap may show day/week structure and a daily time budget; it must never show a per-concept percentage or promise a mastery date. Design implication: the roadmap is a **board of sessions**, and a session's card states *what you'll do*, not *what fraction you'll complete.*

The honest signal of progress is §4.4's pairing map — cells lit, gaps visible — because it says something *true* (R5), and unlike XP it cannot be farmed.

---

## 7. Unresolved contradictions in the repo — these must be settled before design

`gamification.md` and `onboarding.md` are still the **v1 model** and are now in direct conflict with `content.md` / `concept-page-spec.md`. Design cannot proceed while both are authoritative:

| Conflict | v1 files | Newer specs |
|---|---|---|
| Progress display | "Dijkstra 60%", collection "40%", `Est. completion · 7 weeks` | "no percentages — percentages imply a concept can be finished"; no calendar promises |
| Motivation | XP, levels, leagues, promotion/**demotion** zones, 60 badges, rewards shop | mastery as a 10-dimension vector; informational only |
| Completion | "Mastered · 18", badge "Earned Jun 12" | "**no concept closes**"; Focus → Return |
| Structure of Explore | flat sibling grid of BFS/DFS/Quicksort/Heap | must group under Machinery / Structures / Techniques |
| Complexity | printed as a badge | discovered in the operations lab |
| Core loop | playback bar, scrub, speed slider | student-driven stepping, predict-before-reveal |

Also still open from the previous pass: **`research` D-1 (Next.js 16 vs TanStack Start)** — unchanged, and it blocks any build work.

---

## 8. What I recommend, in one paragraph

Keep the palette and the type. Throw away the uniform dashboard skeleton. Split the design language in two — **structures get a workshop bench in space; techniques get a duel in time** — and add a third surface, the **verb × noun pairing map**, which replaces XP as the progress story. Make the object of study full-bleed and dominant. Convert every playback control into a decision the learner has to commit to before the truth is revealed. Delete leagues, demotion, quests and the rewards shop. Then, and only then, generate images.

---

## 9. Decisions I need from you before designing

1. **Gamification:** delete XP/leagues/badges/quests outright, keep a reduced informational subset (e.g. the pairing map + a gentle return cadence), or keep v1 as-is?
2. **Tri-pane:** fuse into one integrated canvas, sequence the three channels across stages, or keep three panes?
3. **Onboarding:** rewrite to drop "Est. completion · 7 weeks" and the % path, or leave it?
4. **Scope of the design pass:** re-design the concept/learning surfaces only, or the whole app including onboarding, gamification and account?
