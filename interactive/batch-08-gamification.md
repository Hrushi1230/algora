# Batch 08 — Gamification that isn't cheap

**Goal:** retention. The rule for this batch: **every reward must be earned by real
understanding, and every number must be honest.** No random loot, no fake urgency, no dark
patterns. Mastery is measured, not awarded.

**Prerequisites:** batches 05, 06, 07 (progressStore must already be recording real events).

---

## Prompt 8.1 — Mastery map

[PASTE SHARED CONTEXT]

```
Build `/mastery` (`src/pages/Mastery/`). This is the "am I actually getting better?" screen and
it should feel like the most trustworthy page in the app.

- Top: overall mastery RingProgress (weighted average across the 15 categories), a mono breakdown
  "watched 22 · learned 14 · practiced 9 · mastered 6 of 24", and a level badge.
- The map: a dependency graph of the 24 algorithms laid out by category using the existing
  GraphView-style SVG (reuse the layout helper from src/engine/layout.ts — do not hand-place
  coordinates). Node fill encodes mastery (viz-idle → tint → accent), size encodes importance,
  and prerequisite edges are drawn. Click a node → a side sheet with that algorithm's mastery
  breakdown, last-seen date, and CTAs (Visualize / Lesson / Practice / Add to review).
  Locked nodes (unmet prerequisites) render outlined with a lock badge and a tooltip naming the
  missing prerequisite. Pan/zoom with buttons AND drag; a "fit to screen" button; fully
  keyboard-navigable via a parallel list view toggle (mandatory — the graph alone is not accessible).
- Category strip below: 15 rows, each with a mastery bar, count, and a "drill" CTA that deep-links
  into /explore with that category filter.
- "Mastery decay" honesty feature: algorithms not reviewed in 21+ days show a small amber
  "fading" chip and drop 10% displayed mastery, with a tooltip explaining why. Implement decay as
  a pure function in src/lib/mastery.ts — never mutate stored progress.
```

---

## Prompt 8.2 — Quests and streaks

[PASTE SHARED CONTEXT]

```
Build the quest system on real events. Nothing random.

`src/lib/quests.ts` — pure evaluators. Each quest declares a metric it reads from today's/this
week's activity + progress: stepsWatched, lessonsCompleted, cardsReviewed, problemsSolved,
minutesActive, newAlgorithmsSeen, perfectQuizzes. Export `evaluateQuests(progress, nowISO)` →
Record<questId, { progress, target, complete }>. Daily quests reset on the local calendar day
(periodKey 'YYYY-MM-DD'); weekly on the ISO week (periodKey 'YYYY-Www'). Rolling over a period
must clear unclaimed progress but never remove already-claimed XP.

Wire `evaluateQuests` into progressStore so quest progress updates automatically after every
recorded event — no manual increments scattered through components.

/quests — Daily section (3 quests) and Weekly section (3 quests): each a card with icon,
title, description, ProgressBar with "7 / 10" in mono, XP reward, and a Claim button that is
disabled until complete and shows a claimed state afterwards. A "resets in 4h 12m" mono countdown
per section. Below: a "quest history" list of the last 14 days with claimed/missed markers.

/streak — a calendar heatmap of the last 6 months (real activity data), current + longest streak
as big mono numbers, milestone markers at 7/30/100/365 with the next one highlighted, streak
freeze inventory (2 per month, explained plainly, spendable to protect yesterday only), and an
honest "what counts as active?" explainer (any XP-earning action). Include a "protect my streak"
CTA that starts a 2-minute review session.
```

---

## Prompt 8.3 — Achievements and leaderboard

[PASTE SHARED CONTEXT]

```
/achievements — 24 achievements from src/data/achievements.ts in a grid, grouped by tier
(bronze/silver/gold/platinum). Locked ones are visible but desaturated with a progress bar toward
the criteria ("solve 25 problems — 18/25"), never hidden and never vague. Filter tabs
All / Unlocked / In progress. Clicking one opens a sheet with the criteria, the unlock date, and
the exact next step to earn it. Write `src/lib/achievements.ts` with a pure
`evaluateAchievements(progress)` and wire it into progressStore like quests — an unlock triggers a
single celebratory toast (badge + name, one scale-pop, no confetti storm) and awards its XP once.

/leaderboard — a league system, not a global vanity board: the user is placed in a bronze/silver/
gold/diamond league of 30 plausible mock peers (generate them deterministically in
src/data/peers.ts with a seeded RNG so ranks are stable across reloads). Show weekly XP, the
promotion zone (top 7, accent tint) and demotion zone (bottom 5, warning tint) with a legend,
the user's row sticky-highlighted and auto-scrolled into view, a mono countdown to the week's end,
and tabs for This week / All time / Friends (Friends = an EmptyState with an invite CTA).
Add a clearly-labelled "these are practice peers while we're in beta" note — do not pretend mock
users are real people.
```

---

## Prompt 8.4 — Reward feel pass

[PASTE SHARED CONTEXT]

```
One focused pass on how progress *feels*. Restrained, premium, never Duolingo-loud.

1. `src/components/common/LevelUpDialog.tsx` — a modest centred dialog on level-up: new level in
   large mono, what it unlocked, XP curve context ("next level at 5,400 XP"), one primary
   "Keep going" CTA. A single 600ms ring-fill + scale animation; static under reduced-motion.
2. Micro-interactions: ProgressBar fills animate from the previous value (not from 0) using a
   spring; XP counters tween with framer-motion's animate(); the streak flame gets a one-shot
   pulse when it increments. All skipped under reduced-motion.
3. `src/hooks/useSound.ts` — three tiny WebAudio-generated tones (correct / level-up / claim).
   Off by default, toggled in prefsStore.soundOn, respecting the OS mute. No audio files.
4. AppShell header: XP chip with a hover popover breaking down today's XP by source; streak pill
   with a popover showing the last 7 days.
5. `src/components/common/ShareCard.tsx` — renders an on-brand summary card (level, streak,
   mastered count, one algorithm thumbnail) into a canvas and offers "copy image" + "download
   PNG". This is your organic-growth surface; make it genuinely attractive at 1200×630.
```

---

## Acceptance checklist — Batch 08

- [ ] Solving a problem visibly moves: XP, level bar, quest progress, mastery, heatmap, activity.
- [ ] Quest progress is computed from events, never incremented ad hoc in a component.
- [ ] Rolling the local date over resets dailies without losing claimed XP.
- [ ] Achievements unlock exactly once and re-render correctly after a reload.
- [ ] Leaderboard ranks are identical across reloads (seeded RNG) and mock peers are disclosed.
- [ ] Mastery map has a keyboard-accessible list-view equivalent.
- [ ] Decay never mutates stored progress (verify by reloading after a decay is displayed).
- [ ] Sound is off by default; every animation is disabled under reduced-motion.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| XP inflation / double awards | `Route every award through progressStore.awardXp with an idempotency key. Add a test that replaying the same event twice awards once.` |
| Quests use Math.random | `Quests must be deterministic evaluations of recorded activity. Remove all randomness.` |
| Graph map unusable on mobile | `Add a list-view toggle that becomes the default under lg, with the same data and CTAs.` |
| Celebration overload | `Cap celebrations: one toast per event, one dialog per level-up, no confetti. Restrained is the brand.` |
| Leaderboard reshuffles on reload | `Generate peers from a seeded PRNG in src/data/peers.ts so output is stable.` |
