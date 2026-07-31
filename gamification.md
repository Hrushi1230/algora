# Algora — Section 5: Gamification (5 pages)

Image-generation prompts for GPT-4o / "gpt image 2". Each prompt renders ONE complete, pixel-perfect SaaS screen as a single **16:9 desktop** screenshot. Copy-paste one block at a time. These are the reward, motivation, and competition screens — playful but premium, never childish, always on-brand.

**Brand recap (do not deviate):**
Algora — a gamified platform where CS students master algorithms through synchronized visualization, code, and plain-English explanation. Tagline: *"See the algorithm think."*
Light theme only. Paper background, ink text, one teal accent. Instrument Sans (headings/body) + JetBrains Mono (code, labels, stats).

**Shared visual system (paste inside every prompt):**
- Background warm off-white paper #F7F9F8; elevated cards pure white #FFFFFF; hairline borders #E4E9E7.
- Text near-black ink #0E1513 for headings, muted slate #5B6763 for secondary text.
- ONE accent: teal #0E9C86 (highlight #14B8A6) — used only for primary buttons, active/selected/earned states, focus rings, progress, XP, streaks, ranks, links, and the logo glyph.
- NO dark backgrounds anywhere, NO black panels, NO purple, NO rainbow gradients, NO glowing blobs/orbs, NO stock photos of people, NO emojis, NO cartoon mascots. Flat solid colors, crisp edges, soft realistic light shadows only. Any celebration is subtle (small flat teal flecks at most).
- Type: Instrument Sans for headlines (large, tight, geometric); JetBrains Mono for stats, ranks, badges, field labels. Corners 12–16px, 1px hairline borders, pale-teal focus ring, generous whitespace, high contrast, WCAG-AA. Ultra high-fidelity, 4k, clean.

**Shared APP SHELL convention (paste inside every prompt in this section):**
- A persistent LEFT SIDEBAR (white, ~240px, hairline right border): top = "algora" wordmark + small teal two-node graph glyph. A vertical nav of mono-labeled items with small teal line icons: "Dashboard", "Explore", "My Path", "Practice", "Review", "Compete", "Achievements" — the current page shown ACTIVE with a pale-teal tint pill and a teal left indicator bar. Bottom of sidebar: a compact user chip (initials avatar circle "AR", ink name "Arjun R.", mono "Lvl 12"), and a slim teal XP progress bar.
- A persistent TOP BAR (white, hairline bottom border): left = page title / breadcrumb in ink; center = a wide search field with mono placeholder "Search algorithms, lessons…"; right = a teal flame streak chip "23", a mono XP chip "2,150 XP", a bell notification icon with a tiny teal dot, and the user avatar.
- The MAIN CONTENT sits on paper background to the right of the sidebar, below the top bar, with generous padding and a clear content grid.

---

## PROMPT — 26. Mastery map (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the MASTERY MAP (a big-picture skill tree showing every topic the student has mastered, is learning, or has locked). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for mastered/active nodes, progress, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "My Path" area / "Achievements" context — show "My Path" ACTIVE; persistent TOP BAR with search, streak "23", "2,150 XP", bell, avatar — as per the shared convention.

MAIN CONTENT (paper background):
- Header: ink headline "Mastery map" + slate subline "Your algorithm knowledge, mapped. 18 of 60 skills mastered."
- A summary strip of THREE white mini stat cards with mono labels: "Mastered · 18" (teal), "In progress · 6", "Locked · 36".
- A large SKILL-TREE canvas card (white, hairline border, dominant): a clean node-graph laid out in tiers left→right by domain ("Foundations" → "Sorting" → "Graphs" → "Dynamic Programming"), connected by hairline edges. Node states: MASTERED nodes are solid teal circles with a small white check and a mono label under them ("Arrays", "Hashing", "BFS", "DFS"); IN-PROGRESS nodes are white with a teal ring at partial fill and a small mono "%" ("Dijkstra 60%"); LOCKED nodes are pale gray with a small lock and muted label ("A* ", "Segment Tree"). A small legend chip in the corner (Mastered / In progress / Locked). Include subtle zoom/recenter controls (mono "+ −" and a "Fit" chip) bottom-right.
- A right-side or bottom "Recommended next" white card: 2 rows suggesting the next unlockable skills, each with a small teal line icon, ink title, mono prerequisite note, and a teal "Start →" link.

IMPORTANT: ONE clean single-screen light desktop app UI, a genuinely graph-like skill tree (not a random blob), realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora dashboard and product screens.

---

## PROMPT — 27. Quests (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the QUESTS screen (daily, weekly, and special goals that award XP and rewards). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for progress, completed states, rewards, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, XP, timers. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Compete" ACTIVE (or "Achievements"); persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Quests" + slate subline "Complete goals to earn XP, badges, and streak freezes." A right-aligned mono "Resets in 08:12:47" countdown chip.
- A tabbed segmented control (mono): "Daily", "Weekly", "Special" — "Daily" active in teal.
- A "Daily quests" section — a column of ~4 white quest cards, each: a small teal line icon in a pale-teal square, an ink quest title ("Solve 3 challenges", "Finish 1 lesson", "Review 10 cards", "Keep your streak"), a slate one-line detail, a slim teal progress bar with a mono count ("2 / 3", "1 / 1", "10 / 10", "23 🔥"), and a right reward chip "+50 XP"; completed cards show a teal check and a solid teal "Claim" button, in-progress cards a ghost "Go →" link.
- A "Weekly challenge" highlight card (pale-teal tint surface, never dark, spanning wide): ink "Graph Master — solve 10 graph problems this week", a big teal progress ring "6 / 10", a mono reward row "Reward: 'Graph Master' badge + 300 XP", and a teal "Continue" button.
- A subtle "Streak freezes: 2 available" mono note with a small teal shield icon.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 28. Leaderboard / leagues (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the LEADERBOARD / LEAGUES screen (a weekly ranked competition among students in the same league). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for the current user's row/rank, promotion zone, progress, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for ranks, XP, names' handles. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Compete" ACTIVE; persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Teal League" + slate subline "Top 10 advance to the Diamond League. 3 days left." A mono "Week 24" chip.
- A LEAGUE BAR row of small tier medallions (flat, teal/gray, NOT dark): "Bronze · Silver · Gold · Teal (current, highlighted) · Diamond" with the current league emphasized in teal.
- A large white LEADERBOARD card (dominant): a table of ~14 ranked rows, each with a mono rank number, an initials avatar circle, an ink display name + mono handle, a right-aligned mono weekly XP ("1,540 XP"), and a tiny up/down movement caret. Ranks 1–3 have small flat teal medal chips. A pale-teal "PROMOTION ZONE" divider after rank 10 with a mono label; a faint "DEMOTION ZONE" hairline near the bottom. The CURRENT USER's row ("Arjun R. · @arjun", rank 8) is highlighted with a pale-teal tint and a teal left bar, clearly standing out.
- A right rail (or top strip) with a "Your standing" white card: big teal "#8", mono "1,180 XP this week", a slate "220 XP to reach #6", and a teal "Solve to climb" button.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic diverse placeholder student names and handles (no real people, no photos, no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 29. Achievements and rewards (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the ACHIEVEMENTS AND REWARDS screen (a collection of unlockable badges and the reward shop). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for earned badges, progress, buttons, links, logo glyph only; LOCKED badges are flat muted gray, never dark. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, counts. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Achievements" ACTIVE; persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Achievements" + slate subline "24 of 60 badges earned. Keep going." A slim teal collection-progress bar "40%".
- A filter row (mono segmented control): "All", "Earned", "In progress", "Locked" — "All" active in teal; a right-aligned "Category ▾" dropdown.
- A responsive GRID of ~12 white badge cards (4 columns): each has a flat geometric badge medallion at top (a simple crest/hexagon with a small teal line icon inside — e.g. a graph node, a flame, a lightning bolt, a stack), an ink badge name (e.g. "First Steps", "Streak x7", "Graph Master", "Speed Demon", "Night Owl", "Century Club"), a one-line slate description, and a footer. EARNED badges are teal-tinted with a mono "Earned Jun 12" date; IN-PROGRESS badges are white with a slim teal progress bar + mono count ("6 / 10"); LOCKED badges are muted gray with a small lock and a mono unlock hint.
- A bottom "Rewards shop" strip (pale-teal tint surface, never dark): ink "Spend XP on perks", 3 small reward chips ("Streak Freeze · 200 XP", "Theme: Mono · 500 XP", "Hint Pack · 150 XP"), each with a teal "Redeem" button, and a mono "Balance: 2,150 XP" note.

IMPORTANT: ONE clean single-screen light desktop app UI, distinct flat geometric badge icons (not photos, not 3D, not emojis), realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 30. Streak calendar (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the STREAK CALENDAR screen (a heatmap of daily learning activity and streak stats). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for active days, streak, progress, buttons, links, logo glyph only — the activity heatmap uses graduated TEAL tints (pale → strong) for intensity, empty days are pale gray #EEF2F0. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for dates, counts, stats. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Dashboard" ACTIVE; persistent TOP BAR with search, streak "23", "2,150 XP", bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Your streak" + slate subline "23 days and counting — your best is 31." A right-aligned teal flame chip "23 day streak".
- A row of THREE white stat cards with mono labels: "Current streak · 23" (teal flame), "Longest streak · 31", "Freezes left · 2" (small teal shield).
- A large ACTIVITY HEATMAP card (white, hairline border, dominant): a GitHub-style contribution grid — 7 rows (Mon–Sun) × ~52 week columns — of small rounded squares in graduated teal intensities, with pale-gray empty days; month labels along the top (mono "Jan Feb Mar …") and weekday labels down the left; a small legend bottom-right "Less ▢▢▢▢ More" in teal steps. Recent weeks are densely teal.
- Below the heatmap: a "This week" mini-row of 7 day pills (M–S) each with a mono date and a teal check for completed days, current day highlighted, plus a mono "3.5 / 4h this week" note.
- A bottom pale-teal tint strip card: ink "Don't break the chain — do one lesson today", a mono "You're on track" note, and a solid teal "Start today's lesson" button.

IMPORTANT: ONE clean single-screen light desktop app UI, a realistic graduated-teal activity heatmap (clean grid, not random noise), realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora product screens.
