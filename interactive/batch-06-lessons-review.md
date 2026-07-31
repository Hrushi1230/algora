# Batch 06 — Lessons, quizzes, spaced repetition

**Goal:** convert "that looked cool" into "I still know it in three weeks". This is the batch
that makes Algora a learning product instead of a museum of animations.

**Prerequisites:** batches 03, 04, 05 (needs the engine, the renderers and progressStore).

**The unfair advantage to exploit here:** because every lesson section can point at a
`visualStep`, the prose and the animation are welded together — and quiz questions can be
generated *from the step log itself*.

---

## Prompt 6.1 — Lesson runner

[PASTE SHARED CONTEXT]

```
Build `/lessons/:slug` (`src/pages/Lesson/`) from src/data/lessons.ts. Reuse FrameView,
PlaybackBar and the player store — do not fork them.

Layout on lg+: left 58% = the lesson content column, right 42% = a sticky visual panel showing
the algorithm at the step named by the current section's `visualStep` (seek the player to it,
smoothly, when the section changes). Under lg: the visual pins to the top as a collapsible strip.

Content column: section-by-section, one section visible at a time, with:
- a top progress bar "Section 3 of 6" plus dot navigation you can click to jump back,
- the section heading + prose rendered from the typed block array (no markdown lib),
- inline "Watch this part" button that plays only that section's step range,
- Prev / Next buttons; Next is the primary and is disabled until an inline check is answered
  when the section has one,
- a floating "Ask: why?" affordance that expands a pre-written deeper explanation (from
  `detail`) — never an AI call in this batch.

Reading position and section index persist to progressStore.lessons[slug].sectionIndex so
closing the tab resumes exactly. Award XP per section (small) via awardXp, and call touchStreak()
on the first section completion of the day.

Final section leads into the quiz (prompt 6.2) rather than a dead end.
```

---

## Prompt 6.2 — Quiz engine

[PASTE SHARED CONTEXT]

```
Build `src/components/quiz/` — a reusable quiz runner used by lessons, the assessment, and review.

`QuizRunner.tsx` props: { questions: QuizQuestion[]; onComplete(result) }. Supports all four
kinds from src/data/types.ts:
- 'mcq' — 4 options, single select, radio semantics via buttons with aria-checked
- 'true-false' — two large buttons
- 'order-steps' — drag-to-reorder list (keyboard alternative: up/down buttons on each row —
  mandatory, drag alone is not accessible)
- 'predict-step' — shows the visualization frozen at step N and asks what happens next; renders
  the real FrameView from the engine, with the answer options as small frame thumbnails or text

Behaviour: one question at a time, immediate feedback on submit (correct = accent tint + check,
wrong = error tint + the correct answer + the `explanation` paragraph), a "why?" expander,
no going back after answering, a progress bar, and a final results panel: score ring,
per-question review list, XP earned, "Review the ones you missed" (loads just those into a
second pass), and a primary CTA to the next thing.

Write `src/lib/generateQuiz.ts`: given an AlgorithmRun, generate 3 'predict-step' questions
automatically — pick milestone steps, use the real next frame as the correct option and three
plausible distractors (a frame with the wrong pointer moved, one with the wrong node visited, one
that skips a step). This is a genuine differentiator; make the distractors non-obvious.

On completion, call completeLesson(slug, score) and awardXp.
```

---

## Prompt 6.3 — Spaced repetition scheduler

[PASTE SHARED CONTEXT]

```
Write `src/lib/srs.ts` — a clean SM-2 variant. Pure functions, unit-tested, no store imports.

  type Grade = 0 | 1 | 2 | 3;   // again / hard / good / easy
  gradeCard(card, grade, nowISO): { ease, intervalDays, dueISO, reps, lapses }
  Rules: ease starts 2.5, clamped to [1.3, 2.8]; grade 0 → interval 0 (due again today, lapses+1,
  ease -0.20); grade 1 → interval * 1.2, ease -0.15; grade 2 → interval * ease; grade 3 →
  interval * ease * 1.3, ease +0.05. First two successful reps use fixed 1-day then 3-day
  intervals. Add ±10% deterministic jitter (seeded by cardId) to avoid review pile-ups.
  Also: isDue(card, nowISO), dueCards(cards, nowISO) sorted by most-overdue,
  forecast(cards, days) → per-day due counts for the next 30 days.

Write `src/data/cards.ts` — 60 review cards across the 24 algorithms, typed as
{ id; algorithmSlug; kind:'concept'|'complexity'|'step-predict'|'code-line'; front; back;
  choices?:string[] }. Real, high-quality content:
- 'complexity' cards ask for time/space of a named operation,
- 'concept' cards ask "why does BFS find the shortest path in an unweighted graph?",
- 'step-predict' cards reference an algorithm + input + step index and are rendered live,
- 'code-line' cards show a line of code and ask what invariant it maintains.

Cards become active only once the user has watched or learned that algorithm — implement
`eligibleCards(progress, cards)`. Add vitest coverage for gradeCard, isDue, and forecast.
```

---

## Prompt 6.4 — `/review`

[PASTE SHARED CONTEXT]

```
Build `/review` (`src/pages/Review/`) on top of srs.ts + progressStore.reviewCards.

Start screen: due count, forecast sparkline for the next 14 days, session-length chooser
(10 / 20 / all), a "hardest first" toggle, and an EmptyState with the next due date when nothing
is due (offer "study ahead — 10 cards" as a secondary path).

Session screen: one card, centred, max-w-[680px]. Front shown first; for 'step-predict' cards
render the live FrameView at that step. Space or click reveals the back with a flip animation
(fade + 2% scale under reduced-motion). Then four grading buttons with keyboard shortcuts 1-4 and
the *next interval* previewed on each button ("Good · 6d") — this transparency is a real UX win.
Top bar: progress through the session, elapsed time in mono, and an exit-with-confirm.

Results screen: cards reviewed, again/hard/good/easy breakdown as a small bar, XP earned, streak
updated, next session date, and a CTA back to /app. Call gradeCard + awardXp + touchStreak.

Undo: the last grading can be undone once (a toast with an Undo action) — restore the previous
card state exactly.
```

---

## Prompt 6.5 — Lesson & review polish

[PASTE SHARED CONTEXT]

```
Small, high-leverage additions. Change nothing else.

1. `src/components/common/XpToast.tsx` — a compact toast "+40 XP · Lesson complete" with a mono
   number that counts up; a level-up variant that shows the new level badge and a subtle
   ring-fill animation. Wire it into awardXp via a store subscription so every XP event surfaces
   exactly once (debounce bursts within 400ms into a single toast).
2. Session guard: if the user leaves a lesson or review session mid-way, show a shadcn
   AlertDialog "Leave and keep your progress?" using a router blocker. Progress must already be
   saved, so the copy is reassuring, not threatening.
3. `useIdleNudge()` — after 90 seconds with no interaction inside a lesson, softly highlight the
   Next button (a one-shot pulse, skipped under reduced-motion).
4. Add "Add to review" buttons on `/algorithms/:slug` (About tab) and on lesson sections that
   inject that algorithm's eligible cards immediately.
5. Streak safety: if the user's streak is about to break (no activity today and it's after 20:00
   local), show a dismissible amber banner in AppShell with a "2-minute review" CTA.
```

---

## Acceptance checklist — Batch 06

- [ ] Closing a lesson mid-way and reopening it resumes on the same section.
- [ ] Changing lesson section seeks the visual panel to that section's `visualStep`.
- [ ] All four quiz kinds are answerable with the keyboard only, including 'order-steps'.
- [ ] `generateQuiz` produces 3 non-trivial predict-step questions for BFS and quicksort.
- [ ] Grading 'again' brings the card back within the same session.
- [ ] Grading buttons show the correct next interval, and it matches what gets stored.
- [ ] XP toast fires once per event; a level-up is visibly distinct.
- [ ] srs vitest suite passes, including the 30-day forecast.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Quiz answers leak into the DOM before submitting | `Do not render the correct answer or explanation until the user submits. Keep them out of the DOM entirely.` |
| Intervals balloon to years | `Clamp ease to [1.3, 2.8] and interval to a maximum of 180 days. Add a test for 10 consecutive 'easy' grades.` |
| Lesson forks the player | `Reuse the existing player store and PlaybackBar. Delete the duplicated playback logic.` |
| Drag-only reordering | `Add up/down buttons with aria-labels to every row so the question is completable without a pointer.` |
| XP double-counts | `Award XP in exactly one place per event, keyed by an idempotency id stored in progressStore.` |
