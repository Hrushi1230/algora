# Batch 09 — Onboarding, roadmap builder, account, support

**Goal:** a new user goes from signup to a personalized plan in under three minutes, and an
existing user can manage everything about their account. Onboarding comes *late* on purpose — it
can only be honest once the mastery model, lessons and practice actually exist.

**Prerequisites:** batches 05, 06, 07, 08.

---

## Prompt 9.1 — Goals and adaptive assessment

[PASTE SHARED CONTEXT]

```
Build the 3-step onboarding flow with a shared `src/pages/onboarding/OnboardingLayout.tsx`
(centred max-w-[720px], a 3-dot step indicator, no sidebar, "skip for now" ghost link that lands
on /app with a default path).

/onboarding/goals — four questions on one scrollable card, each a set of large selectable tiles
with icons (single-select unless noted):
1. Goal: Ace interviews / Pass my DSA course / Build fundamentals / Compete
2. Timeline: 2 weeks / 1 month / 3 months / no deadline
3. Experience: Never studied DSA / Know the basics / Comfortable, rusty / Strong, want depth
4. Weekly time: 2h / 5h / 10h / 15h+
Plus a multi-select "topics you already feel OK with" over the 15 categories.
Store answers in a new `src/stores/onboardingStore.ts` (persisted). Continue is disabled until
all four singles are answered; show which one is missing.

/onboarding/assessment — an adaptive 8-question diagnostic reusing QuizRunner from batch 06.
Write `src/lib/assessment.ts`: a pure adaptive selector that starts at a difficulty implied by the
declared experience, then moves up on a correct answer and down on a wrong one, sampling from a
new `src/data/assessment.ts` bank of 30 questions tagged { category, difficulty }. Include at
least two 'predict-step' questions rendered from the real engine — this makes the assessment feel
like the product. No timer, but show "question 4 of 8" and allow "I don't know" (scored as wrong,
never shamed). Output: per-category estimated level 0-3 + an overall band.

/onboarding/result — "Here's your plan": the estimated level per category as a compact bar list,
the recommended path (matched from src/data/paths.ts by goal + timeline + level), the first three
concrete items with minutes, a realistic finish date computed from the declared weekly time, and
two CTAs: "Start learning" (sets activePathSlug, seeds progressStore with the assessment results
as initial mastery, → /app) and "Customize my plan" (→ /roadmap/new prefilled from the answers).
Be honest: if the assessment says the goal timeline is unrealistic, say so kindly and offer a
tighter scope instead of silently promising it.
```

---

## Prompt 9.2 — Roadmap builder

[PASTE SHARED CONTEXT]

```
Build the custom roadmap feature. Types in `src/data/roadmapTypes.ts`:
Roadmap { id; title; createdAt; goal; weeks; daysPerWeek; minutesPerDay;
  days: Array<{ n; dateISO; items: Array<{ kind:'algorithm'|'lesson'|'problem'|'review';
  slug; minutes; done:boolean }>; theme:string }> }
Store roadmaps in `src/stores/roadmapStore.ts` (persisted, multiple roadmaps, one active).

/roadmap/new — a 3-step wizard:
1. Scope: title, goal, target date (calendar), days per week, minutes per day. Show a live mono
   summary "24 sessions · 18 hours total".
2. Content: pick categories and specific algorithms/problems with a two-column transfer list
   (available ↔ selected, with add-all-in-category). Live warning if the selection exceeds the
   available time, with a "trim to fit" button that drops the lowest-priority items and explains
   what it removed.
3. Review: the generated day-by-day plan, editable inline (drag items between days, with keyboard
   move-up/move-down alternatives), then "Create roadmap".
Generation lives in `src/lib/generateRoadmap.ts` — a pure function that respects prerequisites
(never schedule Dijkstra before BFS), interleaves review days every 4th session, alternates
theory/practice, front-loads weak categories from progressStore, and packs each day to the
minute budget ±15%. Unit-test it: prerequisite order, budget adherence, review cadence.

/roadmap/:id — overview: progress ring, streak within the roadmap, a week-by-week accordion of
days (each day: theme, items with checkboxes, total minutes, a status chip
past-due/today/upcoming), "today" auto-expanded and scrolled to, plus actions: edit, duplicate,
export as markdown (copy to clipboard), delete (confirm dialog), and "set as active".
/roadmap/:id/day/:n — the focused day view: an ordered checklist where each item deep-links into
the right screen and returns here, a session timer (start/pause, persisted), a "complete day"
button that awards XP and unlocks tomorrow, and prev/next day navigation. A calm, single-column
"just do these three things" screen — this is the highest-value page for a stressed student.
```

---

## Prompt 9.3 — Account pages

[PASTE SHARED CONTEXT]

```
Make all five account pages real, reading and writing progressStore/prefsStore only.

/u/:handle — public profile: avatar (initials), name, handle in mono, joined date, level badge,
XP, streak, mastered count, the activity heatmap, top 6 achievements, per-category mastery bars,
and a "share profile" button using ShareCard. `handle === 'me'` renders the current user with an
extra "Edit profile" button.

/progress — the analytics screen: XP-over-time area chart (recharts, accent fill at 15% opacity,
1.5px stroke, no gridline clutter), minutes-per-day bar chart, per-category mastery radar,
accuracy trend on quizzes, problems solved by difficulty (stacked bars), and a range selector
(7d / 30d / 90d / all) driving every chart. Below: an honest "insights" list generated by a pure
function in src/lib/insights.ts (e.g. "you review consistently but rarely finish practice
problems — try 1 problem after each lesson"). Cap it at 3 insights and never invent data.

/settings — sectioned form: Profile (name, handle with availability check simulation, bio,
avatar initials colour), Learning (default language, playback speed, narration on/off, sound,
reduced motion override, daily XP goal), Notifications (a matrix of email/push × 6 event types),
Appearance (font size, code font size, "high contrast" toggle that swaps to a stronger token set),
Data (export progress as JSON download, import from JSON with validation, reset all progress
behind a type-the-word confirm), Danger (delete account, confirm dialog).
Each section saves independently with a "Saved" mono flash; unsaved-changes guard on navigation.

/billing — current plan card, usage summary, a plan-switch section reusing the PLANS constant from
/pricing, payment method placeholder (clearly labelled "no real payments in beta"), invoice table
with download buttons that produce a simple generated text invoice, and a cancel flow with a
retention step offering a pause instead.

/notifications — a real inbox: grouped by today/this week/earlier, types (achievement, streak
reminder, review due, path milestone, product news) with type icons, read/unread state (bold +
accent dot), mark-all-read, per-type filters, and an EmptyState. Seed 12 plausible items derived
from actual progress events.
```

---

## Prompt 9.4 — Support pages

[PASTE SHARED CONTEXT]

```
/help — a searchable help centre over a new `src/data/help.ts` (24 articles across 6 categories:
Getting started, Visualizer, Lessons & review, Practice, Account & billing, Troubleshooting;
each with slug, title, category, body blocks, and related slugs). Category cards, a search with
highlighted matches, "popular articles" list, and a contact CTA to /contact.
/help/:slug — article layout with breadcrumbs, a table of contents, prose, a "was this helpful?"
yes/no widget with a thank-you state, related articles, and prev/next within the category.

/status — an honest status page: overall banner (all systems operational), 5 components
(Web app, Visualizer engine, Practice runner, Auth, Sync) each with a 90-day uptime strip built
from a seeded generator, current uptime percentage in mono, an incident history list with 3 past
resolved incidents (real-sounding postmortem one-liners), and a subscribe-to-updates email form.
/privacy and /terms — a shared LegalLayout: max-w-[760px] prose, last-updated date, a sticky
table of contents on xl+ with scroll-spy, and genuinely written sections (data we collect, how
progress data is used, cookies, third parties, your rights, contact) — plain language, no filler.
```

---

## Acceptance checklist — Batch 09

- [ ] Fresh user: signup → goals → assessment → result → `/app` shows a seeded, sensible plan.
- [ ] The assessment adapts (answer everything wrong vs right → visibly different questions).
- [ ] `generateRoadmap` never schedules an algorithm before its prerequisite; tests prove it.
- [ ] Roadmap day view deep-links out and back without losing the timer.
- [ ] Settings export → reset → import restores the exact prior state.
- [ ] `/progress` range selector drives every chart; charts are readable at 375px.
- [ ] Help search finds articles by body text, not just titles.
- [ ] No page in this batch invents a metric that isn't in progressStore.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Assessment is a fixed quiz | `Make it adaptive: select the next question from the bank based on the running per-category estimate. Pure function in src/lib/assessment.ts.` |
| Roadmap ignores time budget | `Pack each day to minutesPerDay ±15% and add a unit test asserting it for 3 configurations.` |
| Charts use a rainbow palette | `Charts use only accent, highlight, tint and slate. One series colour per meaning.` |
| Settings save everything at once | `Each section saves independently and shows its own saved state.` |
| Insights are made up | `Derive every insight from real progressStore data with an explicit threshold. Show none rather than a false one.` |
