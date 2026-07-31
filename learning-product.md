# Algora — Section 4: Learning Product (9 pages)

Image-generation prompts for GPT-4o / "gpt image 2". Each prompt renders ONE complete, pixel-perfect SaaS screen as a single **16:9 desktop** screenshot. Copy-paste one block at a time. This is the logged-in core product — premium, focused, and built for students.

**Brand recap (do not deviate):**
Algora — a gamified platform where CS students master algorithms through synchronized visualization, code, and plain-English explanation. Tagline: *"See the algorithm think."*
Light theme only. Paper background, ink text, one teal accent. Instrument Sans (headings/body) + JetBrains Mono (code, labels, stats).

**Shared visual system (paste inside every prompt):**
- Background warm off-white paper #F7F9F8; elevated cards pure white #FFFFFF; hairline borders #E4E9E7.
- Text near-black ink #0E1513 for headings, muted slate #5B6763 for secondary text.
- ONE accent: teal #0E9C86 (highlight #14B8A6) — used only for primary buttons, active/selected states, focus rings, progress, links, XP, and the logo glyph.
- NO dark backgrounds anywhere, NO black panels, NO purple, NO rainbow gradients, NO glowing blobs/orbs, NO stock photos of people, NO emojis. Flat solid colors, crisp edges, soft realistic light shadows only.
- Type: Instrument Sans for headlines (large, tight, geometric); JetBrains Mono for code, badges, stats, field labels. Corners 12–16px, 1px hairline borders, pale-teal focus ring, generous whitespace, high contrast, WCAG-AA. Ultra high-fidelity, 4k, clean.

**Shared APP SHELL convention (paste inside every prompt in this section):**
- A persistent LEFT SIDEBAR (white, ~240px, hairline right border): top = "algora" wordmark + small teal two-node graph glyph. A vertical nav of mono-labeled items with small teal line icons: "Dashboard", "Explore", "My Path", "Practice", "Review", "Compete", "Achievements" — the current page shown ACTIVE with a pale-teal tint pill and a teal left indicator bar. Bottom of sidebar: a compact user chip (initials avatar circle "AR", ink name "Arjun R.", mono "Lvl 12"), and a slim teal XP progress bar.
- A persistent TOP BAR (white, hairline bottom border): left = page title / breadcrumb in ink; center = a wide search field with mono placeholder "Search algorithms, lessons…"; right = a teal flame streak chip "23", a mono XP chip "2,150 XP", a bell notification icon with a tiny teal dot, and the user avatar.
- The MAIN CONTENT sits on paper background to the right of the sidebar, below the top bar, with generous padding and a clear content grid.

---

## PROMPT — 17. Student dashboard (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Render a single full desktop viewport with the app shell, nothing cropped, nothing cut off.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the logged-in STUDENT DASHBOARD (the home base after signing in). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; cards pure white #FFFFFF; hairline borders #E4E9E7. Text near-black ink #0E1513 headings, muted slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for buttons, active states, focus, progress, XP, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for code, labels, badges, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: include the persistent LEFT SIDEBAR with "Dashboard" ACTIVE (pale-teal pill + teal left bar), and the persistent TOP BAR with search, streak "23", "2,150 XP", bell, and avatar — exactly as described in the shared app-shell convention.

MAIN CONTENT (paper background, clear grid):
- A greeting header: ink headline "Welcome back, Arjun." (period as a small teal square) with a slate subline "You're 250 XP from Level 13 — keep the streak alive."
- A "Continue learning" hero card (white, hairline border, spanning the top): left a small teal line icon + ink lesson title "BFS on Grids", a mono chip "Interview Prep Fast-Track · Lesson 12 of 42", a slim teal progress bar at ~60%; right a solid teal "Resume lesson" button with a right-arrow.
- A row of THREE white stat cards with mono labels: "Streak · 23 days" (teal flame + a M–S week row with teal checks), "This week · 3.5 / 4h" (teal ring), "XP today · +180" (teal).
- A two-column lower body:
  - LEFT (wider): "Today's plan" — a white card listing 3 lesson/task rows, each with a small teal line icon, ink title, mono duration chip ("Two Pointers · 20m", "Sliding Window · 25m", "Review: 6 cards · 10m"), and a ghost "Start" link; first row has a teal "Due now" tag.
  - RIGHT (narrower): "Your path" mini skill-tree card — ~5 connected nodes, first teal "current", next pale-teal "up next", rest gray "locked" with small locks; a teal "View full path →" link.
- A bottom "Daily quest" strip card (soft pale-teal tint, never dark): ink "Solve 2 challenges to earn +100 XP", a teal progress "1 / 2", and a teal "Go to practice" button.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora marketing, auth, and onboarding screens.

---

## PROMPT — 18. Explore algorithms (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the EXPLORE ALGORITHMS catalog (browse and filter every algorithm and data structure). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical to the dashboard): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for buttons, active/selected states, focus, progress, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, badges, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Explore" ACTIVE; persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Explore algorithms" + slate subline "60+ interactive visualizers across data structures, graphs, and DP."
- A FILTER BAR row: a mono "Category" segmented control with pills "All", "Data Structures", "Graphs", "Sorting", "Searching", "Dynamic Programming" ("Graphs" selected in teal); a right-aligned mono "Difficulty" dropdown "All levels ▾" and a "Sort: Recommended ▾" dropdown.
- A responsive GRID of ~9 white algorithm cards (3 columns), each: a compact mini-visualization thumbnail at top (e.g. a tiny teal-node graph, an array of bars, a tree), an ink title (mono for the short name), a one-line slate description, a footer row with a mono difficulty chip ("Easy"/"Medium"/"Hard"), a small teal progress bar if started, and a ghost "Open →" link. Cards include: "BFS", "DFS", "Dijkstra", "Quicksort", "Merge Sort", "Binary Search", "DP Table", "Union-Find", "Heap". Show a couple with a teal "In progress" tag, one with a teal check "Mastered", and one or two with a small gray "Pro" lock.
- A subtle bottom pagination row (mono "1 2 3 … 7", current page teal).

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 19. Algorithm visualizer (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. This is the FLAGSHIP screen — make it the richest and most impressive.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the ALGORITHM VISUALIZER workspace (the synchronized visualization + code + explanation, hands-on). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for controls, active line, current node, progress, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for code, labels, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: keep a slim LEFT SIDEBAR (can be collapsed to icons only to maximize the workspace) with "Explore" area active; a slim TOP BAR showing a breadcrumb "Explore / Graphs / BFS" in ink, plus the streak, XP, and avatar on the right.

MAIN CONTENT — a THREE-PANEL synchronized workspace on paper:
- LEFT / CENTER (largest, white canvas card): the live VISUALIZATION — a binary tree or graph of ~9 numbered nodes with connecting edges; node 1 filled teal labeled "Current", nodes 2 & 4 pale-teal "Visited", the rest white/gray "Unvisited"; a small legend top-right. Along the bottom of the canvas a PLAYBACK BAR: pause/play/step-back/step-forward controls, a scrubbable timeline track with keyframe dots and a teal playhead, a teal speed slider "1.0x", and a mono step counter "Step 4 / 11". Two small mono callout tags: "current node", "queue: [2,3,4]".
- RIGHT TOP (white code pane, subtle line numbers): JetBrains Mono Python BFS code with line 7 highlighted in a pale-teal row; a small "Python ▾" language selector and a mono "Reset" link.
- RIGHT BOTTOM ("Explanation" card, pale surface): plain-English text describing the current dequeue step, with the key term in teal; a mono "Step 4 of 11" caption and prev/next chevrons.
- A top-of-content ROW above the panels: ink title "Breadth-First Search", a mono difficulty chip "Medium", a teal "Mark as complete" ghost button, and a solid teal "Next: DFS →" button.

IMPORTANT: ONE clean single-screen light desktop app UI, all three panels visibly IN SYNC (same step reflected in canvas, code line, and explanation), realistic legible placeholder copy and real-looking code (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 20. Lesson experience (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the LESSON EXPERIENCE (a guided, step-by-step teaching flow combining reading, an embedded visual, and a quick check). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for progress, active states, links, buttons, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for code, labels, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "My Path" ACTIVE; slim TOP BAR with a breadcrumb "Interview Prep Fast-Track / Lesson 12" in ink, a slim teal lesson-progress bar "Lesson 12 of 42", streak, XP, and avatar.

MAIN CONTENT — a two-column reading layout:
- LEFT RAIL (narrow, white card): a "Lesson outline" vertical stepper of ~6 sub-steps ("Intro", "The idea", "Watch it run", "Code walkthrough", "Quick check", "Recap"); completed steps have teal checks, the current "Watch it run" is teal-highlighted, later steps muted gray.
- MAIN COLUMN (wide, white reading card): ink lesson title "BFS on Grids", a slate lead paragraph, a body of well-set ink paragraphs with generous line-height, one inline mono code snippet block (white, line numbers), and an EMBEDDED visualization sub-card (white, hairline border) showing a small grid with a teal "current cell" and pale-teal "visited" cells plus a mini playback control. A pale-teal callout box "Key idea" with ink text and a teal bar on its left edge.
- At the bottom of the main column: a "Quick check" mini-card — a one-line ink question and two answer pills (one selected teal), plus a footer nav row: left ghost "← Previous", right solid teal "Continue" button, and a small mono "+40 XP on completion" chip.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), comfortable reading typography, consistent alignment, matching the Algora design language.

---

## PROMPT — 21. Practice challenge (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the PRACTICE CHALLENGE screen (a coding problem with an editor, test cases, and a run/submit flow). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for run/submit, active states, passing tests, progress, links, logo glyph only. IMPORTANT: even the code EDITOR is a LIGHT theme (white/off-white background, dark ink code text, subtle line numbers, pale-teal active line) — NO dark IDE panel. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for all code. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Practice" ACTIVE; slim TOP BAR with breadcrumb "Practice / Arrays / Two Sum" in ink, a mono timer chip "12:04", streak, XP, and avatar.

MAIN CONTENT — a split two-pane workspace on paper:
- LEFT PANE (white problem card): a mono difficulty chip "Medium" + teal "Two Pointers" topic tag; ink problem title "Two Sum II"; a slate problem statement with a small mono example block ("Input: [2,7,11,15], target=9 → Output: [1,2]"); a "Constraints" list; and small tabs "Description · Hints · Solutions" with Description active in teal.
- RIGHT PANE (white code editor card, LIGHT theme): a header row with a "Python ▾" language selector and a mono "Reset code" link; a numbered JetBrains Mono code editor pre-filled with a function stub and a couple of written lines, the current line in a pale-teal row; below it a "Test cases" sub-panel showing 3 test rows with mono I/O and status chips — two teal "Passed" checks and one gray "Not run"; a footer control row: left ghost outline "Run" button, right solid teal "Submit" button, and a mono "+80 XP" reward chip.

IMPORTANT: ONE clean single-screen light desktop app UI with a LIGHT code editor (never a dark IDE), realistic legible real-looking code and copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 22. Challenge results (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the CHALLENGE RESULTS screen (shown right after submitting a passing solution — celebratory but calm). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for success states, XP, progress, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO glowing confetti orbs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows; any celebration is subtle (small flat teal confetti flecks at most). Instrument Sans headlines; JetBrains Mono for stats, labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Practice" ACTIVE; slim TOP BAR with breadcrumb "Practice / Two Sum II / Results", streak, XP, and avatar.

MAIN CONTENT — a centered results card (white, hairline border, ~820px) on paper:
- A large teal success check mark (flat, in a pale-teal circle) with ink headline "All tests passed." (period as small teal square) and a slate subline "Nice — that's your 4th solve today."
- A row of FOUR white stat mini-cards with mono labels: "Runtime · 42 ms (teal 'beats 88%')", "Memory · 15.1 MB", "Attempts · 2", "XP earned · +80" (the +80 in teal).
- A "Complexity" white card: ink "Time O(n) · Space O(1)" with a short slate note comparing to the brute-force approach.
- A slim teal XP/level progress strip: "Lvl 12 · 2,230 / 2,400 XP" with a "+80 XP" chip and a small mono "170 XP to Level 13".
- A "What's next" row of two white suggestion cards ("Try: 3Sum · Medium", "Review: Two Pointers · 6 cards"), each with a small teal line icon and a ghost "Start →" link.
- Footer button row: left ghost outline "Back to problem", center ghost "View solution", right solid teal "Next challenge" button with a right-arrow.

IMPORTANT: ONE clean single-screen light desktop app UI, subtle and premium (not loud), realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 23. Learning-path detail (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the LEARNING-PATH DETAIL screen (the full curriculum for one path, with its modules and lessons). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for progress, current lesson, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "My Path" ACTIVE; slim TOP BAR with breadcrumb "Paths / Interview Prep Fast-Track", streak, XP, and avatar.

MAIN CONTENT:
- A PATH HEADER card (white, hairline border): left a small teal line icon + ink title "Interview Prep Fast-Track", a slate one-line description, and a mono meta row "42 lessons · 6 modules · ~7 weeks · Intermediate"; right a large teal progress ring "29%" with "12 / 42 lessons" and a solid teal "Resume" button.
- A two-column body:
  - LEFT (wider): a MODULE ACCORDION list of 6 modules; each module is a white card with an ink module title, a mono "Module 2 · 7 lessons · 60% complete" line, and a slim teal progress bar. The current module is EXPANDED, revealing lesson rows: each row has a status glyph (teal check = done, teal filled dot = current "Continue", gray lock = locked), an ink lesson title, a mono duration chip, and a small XP chip; the "current" row has a pale-teal tint. Other modules are collapsed with a chevron.
  - RIGHT (narrower, sticky): an "About this path" white card with a short slate paragraph, a mono "Skills you'll build" tag list ("Two Pointers", "Sliding Window", "BFS/DFS", "DP", "Greedy"), a "Prerequisites" mini-list, and an "Est. XP · 8,400" mono stat in teal.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 24. Review queue (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the REVIEW QUEUE (spaced-repetition flashcard-style review of previously learned concepts). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for progress, active states, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for code, labels, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Review" ACTIVE; slim TOP BAR with page title "Review queue" in ink, streak, XP, and avatar.

MAIN CONTENT — a focused review layout on paper:
- A top progress strip: mono "Card 3 of 12" with a slim teal progress bar at ~25%, and a mono "~8 min left" estimate on the right; a small teal "Due today · 12" chip.
- A large centered REVIEW CARD (white, hairline border, ~720px, subtle shadow to feel like a stacked deck): a mono topic tag "Graphs · BFS" at top; an ink prompt question "What data structure does BFS use to track the frontier?"; a small embedded visual hint (a tiny teal-node graph or a mono code line); and the card shown in its "revealed" state with a pale-teal answer box containing ink text "A queue (FIFO)" and a one-line slate explanation.
- A SELF-GRADE control row below the card: four pill buttons with mono labels "Again", "Hard", "Good", "Easy" — "Good" emphasized in solid teal, the others as light outline pills; a small mono caption under each showing the next interval ("<1m", "10m", "1d", "4d").
- A right-aligned ghost "Skip card" link and a mono "Session XP · +30".

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 25. Search / results (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the SEARCH / RESULTS screen (a query typed into global search with grouped, filterable results). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for active filters, matched terms, links, buttons, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, stats, matched code terms. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR (no single item active, or a subtle "Explore" state); TOP BAR with the SEARCH FIELD prominently FOCUSED (teal focus ring) containing the query "binary search" and a mono "results" caption; streak, XP, and avatar on the right.

MAIN CONTENT:
- A header line: ink "Results for “binary search”" (matched term subtly teal) with a slate "38 results" count.
- A FILTER CHIP ROW: mono type filters "All", "Algorithms", "Lessons", "Challenges", "Paths", "Glossary" with "All" selected in teal and result counts in parentheses.
- A two-column body:
  - LEFT (narrow filter rail, white card): "Type" checkboxes with counts, a "Difficulty" group (Easy/Medium/Hard), and a "Status" group (Not started / In progress / Mastered) — a couple checked in teal.
  - RIGHT (wide results list): GROUPED result sections with small mono section headers ("ALGORITHMS", "LESSONS", "CHALLENGES"). Each result is a white row card with a small teal type icon, an ink title with the matched substring highlighted in teal, a one-line slate snippet, a mono meta row (difficulty chip / duration / "In progress" tag), and a ghost "Open →" link. Include ~6–7 varied results (e.g. "Binary Search" algorithm, "Binary Search on Answer" lesson, "Search in Rotated Array" challenge, a glossary term "Invariant").
- A subtle bottom "Load more results" ghost button centered.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora marketing, auth, onboarding, and product screens.
