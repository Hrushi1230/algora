# Batch 05 — Discovery: dashboard, explore, search, paths

**Goal:** make the 24-algorithm catalog findable and make `/app` the screen a returning student
lands on and immediately knows what to do next.

**Prerequisites:** batches 01, 03, 04.

---

## Prompt 5.1 — Progress store (needed by everything from here on)

[PASTE SHARED CONTEXT]

```
Create `src/stores/progressStore.ts` (zustand + persist 'algora-progress', version 1 with a
migrate function). This is the ONLY place learning progress lives. Later batches read it; none of
them may create a parallel store.

State:
  xp: number; level: number;
  streak: { current:number; longest:number; lastActiveISO:string|null; freezesLeft:number };
  algorithms: Record<slug, { status:'locked'|'new'|'watched'|'learning'|'practiced'|'mastered';
    stepsWatched:number; lessonDone:boolean; quizScore:number|null; problemsSolved:string[];
    lastSeenISO:string; masteryPct:number }>;
  lessons: Record<slug, { completedAt:string|null; sectionIndex:number; quizScore:number|null }>;
  problems: Record<slug, { attempts:number; solvedAt:string|null; bestRuntimeMs:number|null;
    lastCode:Record<'js'|'ts'|'py',string> }>;
  reviewCards: Record<cardId, { ease:number; intervalDays:number; dueISO:string; reps:number;
    lapses:number }>;
  quests: Record<questId, { progress:number; claimedAt:string|null; periodKey:string }>;
  achievements: Record<achId, { unlockedAt:string|null; progress:number }>;
  activity: Record<'YYYY-MM-DD', { xp:number; minutes:number; steps:number; solved:number }>;
  bookmarks: string[];

Actions: awardXp(amount, reason), recordStepsWatched(slug, n), markLessonSection(slug, i),
completeLesson(slug, quizScore), recordAttempt(problemSlug, code, lang),
markSolved(problemSlug, runtimeMs), touchStreak(), useFreeze(), gradeCard(cardId, grade 0-3),
setQuestProgress(id, n), claimQuest(id), toggleBookmark(slug), resetAll().

Rules:
- `awardXp` recomputes level from `src/lib/xp.ts` (write it: levelFromXp, xpForLevel with a
  curve of 100 * level^1.35, xpToNextLevel, progressPct) and returns { leveledUp, newLevel }.
- `touchStreak` compares lastActiveISO to today in the user's local timezone: same day = no-op,
  yesterday = increment, older = reset to 1 (unless a freeze is spent).
- masteryPct is derived: watched 20% + lesson 30% + quiz 20% (scaled) + problems 30%.
- Every mutation also writes into `activity[today]`.
- Seed from `src/data/user.ts` on first run so the app never looks empty in a demo.

Also `src/hooks/useProgress.ts` with selector hooks: useAlgorithmProgress(slug),
useOverallMastery(), useCategoryMastery(), useDueCardCount(), useTodayActivity().
No UI in this prompt.
```

---

## Prompt 5.2 — `/app` dashboard

[PASTE SHARED CONTEXT]

```
Build `/app` (`src/pages/Dashboard/`) from progressStore + data files. Real numbers only —
nothing hardcoded.

- Greeting row: time-aware greeting with the user's name, today's date in mono, and a
  StreakPill (flame + current streak, amber when today isn't logged yet, teal when it is).
- ContinueCard (the hero of this page, spans 2 cols): the single best next action, chosen by
  this priority: unfinished lesson > due review cards > next item in the active path >
  weakest category's next algorithm. Shows a small live FrameView thumbnail of that algorithm's
  step 0, the reason ("you left off at section 3 of 6"), a ProgressBar, and one primary CTA.
- StatCard row: XP + level with a ProgressBar to next level, current streak, algorithms mastered
  (n/24), minutes this week.
- DailyQuests: 3 daily quests with progress bars and a Claim button that goes live at 100%
  (confetti-free — a scale pop + toast is enough).
- ReviewCard: due count, "oldest card waiting 3 days", CTA → /review, EmptyState when 0 due.
- ActivityHeatmap: last 12 weeks, 5 intensity steps from viz-idle → accent, tooltip per day,
  legend, keyboard-focusable cells with aria-labels.
- WeakSpots: 3 lowest-mastery categories with a "Drill this" CTA → /explore?category=…
- RecentlyViewed: last 4 algorithms from lastSeenISO.

Empty-state variant: if the user has zero activity, replace ContinueCard with a "Take the
2-minute assessment" card → /onboarding/goals. Loading: Skeletons, never a spinner-only screen.
```

---

## Prompt 5.3 — `/explore` catalog

[PASTE SHARED CONTEXT]

```
Build `/explore` over `src/data/algorithms.ts` + progressStore.

Toolbar: search input (name, tags, category — debounced 200ms, fuzzy on name), category chips
(multi-select, with counts), difficulty segmented control, status filter
(All / Not started / In progress / Mastered), sort (Recommended / A-Z / Difficulty / Shortest),
grid/list view toggle. ALL state synced to the URL via useSearchParams; refresh restores exactly.

AlgorithmCard: name, oneLiner, DifficultyBadge, category chip, ComplexityTag (avg time),
estMinutes, a mastery RingProgress, bookmark toggle, and a static FrameView thumbnail of step 0
that starts animating on hover/focus at 2× for 6 steps then stops (skip entirely under
reduced-motion, and never animate more than 3 cards at once — use IntersectionObserver +
a shared "who is hovered" guard). Click → /algorithms/:slug.

Left rail on xl+: category tree with per-category mastery bars. "Recommended" sort = the same
scoring used by ContinueCard (prerequisites satisfied first, weakest category first).
Results count line in mono, "clear all filters" link, EmptyState on no match.
Virtualize the grid only if it exceeds 60 items — otherwise plain rendering.
```

---

## Prompt 5.4 — Global search (Cmd-K)

[PASTE SHARED CONTEXT]

```
Build the command palette and the /search page over one shared index.

`src/lib/search.ts` — build an index from algorithms, lessons, problems, paths, posts and help
articles: { id, kind, title, subtitle, keywords[], href }. Implement a small scoring function
(exact title > prefix > word-boundary > fuzzy subsequence; boost by kind order
algorithm > lesson > problem > path > post > help). No external search library.

`src/components/common/CommandPalette.tsx` — shadcn Command dialog opened by Cmd/Ctrl-K from
anywhere (wire the AppShell search button to it too). Grouped results with kind icons, keyboard
navigation, Enter to navigate, recent searches from localStorage, and quick actions
("Start today's review", "Random algorithm", "Toggle sidebar", "Open settings").
Empty query shows 5 suggested algorithms based on progress.

/search — full-page version reading ?q=, with kind filter tabs, highlighted matched substrings,
result counts per kind, and a "nothing found → browse Explore" EmptyState.
```

---

## Prompt 5.5 — Paths

[PASTE SHARED CONTEXT]

```
/paths (public) — 4 path cards from src/data/paths.ts: title, subtitle, weeks, audience,
outcome bullets, algorithm-count, difficulty spread bar, and a preview of the first 3 modules.

/paths/:slug — hero (title, subtitle, weeks, total minutes, xp, "Start path" primary), an
outcomes list, then a vertical module timeline: each module is a card with its items
(algorithm / lesson / problem, each with an icon, minutes, and a completion check from
progressStore), a module progress ring, and locked styling for modules whose prerequisites are
unmet (locked = reduced opacity + lock icon + tooltip explaining what unlocks it, never hidden).
Sticky right rail on xl+: overall path progress ring, "next item" CTA, estimated finish date
based on the user's recent daily minutes, and a "set as active path" toggle stored in
progressStore (add an `activePathSlug` field). Unknown slug → 404.
```

---

## Acceptance checklist — Batch 05

- [ ] `/explore?category=graphs&difficulty=medium&status=in-progress` survives a reload.
- [ ] Dashboard numbers change after you watch steps on `/algorithms/bfs` (and survive reload).
- [ ] ContinueCard picks a sensible next action in all four priority branches.
- [ ] Cmd-K works on every route and Enter navigates.
- [ ] Hover thumbnails never animate more than 3 at once; scrolling stays smooth.
- [ ] Heatmap cells are keyboard-reachable with meaningful aria-labels.
- [ ] Locked path modules are visible-but-locked with a reason, not hidden.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Second progress store appears | `Delete the duplicate store. All progress reads/writes go through src/stores/progressStore.ts.` |
| Explore filters lost on reload | `Sync every filter to the query string with useSearchParams and initialise state from it.` |
| Thumbnails tank performance | `Only animate the hovered card, cap concurrent animations at 3, and pause off-screen cards via IntersectionObserver.` |
| Dashboard shows fake numbers | `Every value must come from progressStore selectors. Remove hardcoded stats.` |
