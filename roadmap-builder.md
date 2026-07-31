# Section 8: Roadmap Builder — 3 pages (16:9)

Generate each screen as a single high-fidelity **16:9 desktop** product screenshot (1440x900) for **Algora**, a premium, gamified algorithm-learning platform for students. Output the full app UI as if captured from a real, shipping web app. No device frames, no browser chrome, no mockup shadows, no annotations.

---

## SHARED VISUAL SYSTEM (STRICT — obey on every screen)

- **Theme:** Light only. Never dark. Warm, calm, premium, academic-but-modern.
- **Colors (use ONLY these):**
  - Paper background `#F7F9F8` (warm off-white)
  - Card surface `#FFFFFF` (pure white)
  - Ink text `#0E1513` (near-black, headings and primary text)
  - Slate text `#5B6763` (secondary text, labels, captions)
  - Teal accent `#0E9C86` (primary brand: buttons, active states, progress, highlights)
  - Hairline borders `#E6EBE9` (1px, all card and divider edges)
  - Soft teal wash `#E7F5F1` (selected chips, subtle fills) — use sparingly
- **No gradients. No purple/violet. No dark panels. No emojis. No decorative blobs, glows, or abstract shapes.**
- **Typography:** Headings and UI in **Instrument Sans**; all code, numbers, day counts, and stats in **JetBrains Mono**.
- **Shape language:** 12–16px rounded corners on cards, 8–10px on buttons and inputs. Generous whitespace. Crisp 1px borders, never heavy shadows — at most a very soft, low-opacity shadow.
- **Depth:** Flat and clean. Contrast comes from borders and spacing, not shadow.
- **Accessibility:** High contrast, legible 14px+ body text, clear focus/selected states.

## APP SHELL (persistent, identical to the student learning product)

- **Left sidebar (240px, white, 1px right border):** Algora wordmark top-left (ink text, small teal glyph). Vertical nav with 20px line icons + labels: Dashboard, Explore, **Roadmap** (active on these screens — teal text, soft teal wash pill, 3px teal left indicator), Practice, Mastery, Leaderboard. Bottom: streak flame with day count (JetBrains Mono) and a small circular student avatar with name.
- **Top bar (64px, white, 1px bottom border):** Left = current page title in ink. Center = slim search field with placeholder "Search topics, problems…". Right = XP total (JetBrains Mono), level ring, notification bell, avatar.
- **Content area:** Paper background `#F7F9F8`, comfortable 32px padding, max content width centered.

---

## PAGE 41 — Roadmap Setup (goal + duration)

Title in top bar: "Build your roadmap". A calm, guided single-screen builder centered in the content area, max width ~880px, presented as one tall white card OR two stacked white cards with clear step grouping.

- **Header block:** Large ink headline "What are you preparing for?" with a slate subline "We’ll build a personalized day-by-day plan around your goal and schedule."
- **Step 1 — Goal (a 3x2 grid of selectable goal cards, each white, 1px border, 16px radius, hover/selected = teal border + soft teal wash + small teal check top-right):**
  1. **FAANG Interviews** — line icon (building), title, slate caption "Big Tech DSA + system design fundamentals".
  2. **Competitive Programming** — icon (lightning/stopwatch), caption "Codeforces/ICPC style speed + math".
  3. **Small Startup** — icon (rocket), caption "Pragmatic full-stack + core CS essentials".
  4. **US-Based Roles** — icon (map pin / flag-neutral), caption "Interview loops common at US companies".
  5. **Interview Practice** — icon (chat/question), caption "Mock interviews + timed problem drills".
  6. **General Practice** — icon (dumbbell), caption "Steady skill-building, no deadline pressure".
  - Show the **FAANG Interviews** card as selected.
- **Step 2 — Duration (horizontal row of pill presets in JetBrains Mono):** 30, 60, 90, 120, 180 days, plus a **Custom** pill that reveals a small number input. Show **90 days** selected (teal fill, white text).
- **Step 3 — Daily commitment:** a horizontal slider labeled "Time per day" with tick labels 30m / 1h / 2h / 3h+, thumb in teal, currently at "1h 30m" (JetBrains Mono readout on the right). Below it a small row of day-of-week toggle chips (M T W T F S S) with weekdays active in teal, weekend slate/inactive.
- **Step 4 — Current level (segmented control):** Beginner / Intermediate / Advanced — Intermediate selected (teal).
- **Live summary strip (bottom of card, soft teal wash, 1px border):** JetBrains Mono line reading "FAANG Interviews · 90 days · ~1h 30m/day · ~135 hours total · ~46 problems". 
- **Primary CTA:** full-width or right-aligned teal button "Generate my roadmap" with a small forward arrow. A quiet ghost link "Skip, I’ll browse instead" beside it in slate.
- Keep everything airy, confident, and premium — a focused decision surface, not a cluttered form.

---

## PAGE 42 — Generated Roadmap (the plan)

Title in top bar: "Your 90-day FAANG roadmap". The generated, personalized plan. Content area splits into a left plan column (~70%) and a right summary rail (~30%).

- **Plan header card (white):** ink title "FAANG Interview Roadmap", slate subline "90 days · 1h 30m/day · Intermediate". A thin overall progress bar in teal reading "Day 12 of 90 · 13% complete" (JetBrains Mono). Small secondary buttons: "Edit plan", "Export".
- **Phase timeline (the core):** the roadmap organized into 4 vertical **phases**, each a white card with a teal phase number chip, phase title, day-range in JetBrains Mono, and a mini progress bar:
  1. **Foundations** (Days 1–20) — Arrays, Strings, Hashing, Two Pointers. Marked mostly complete (teal fill).
  2. **Core Structures** (Days 21–45) — Stacks, Queues, Linked Lists, Trees, Heaps. In progress, teal partial bar, a small "You are here" teal marker.
  3. **Algorithms** (Days 46–72) — Recursion, Sorting, Graphs, DP. Locked-ahead, slate.
  4. **Interview Mode** (Days 73–90) — Mock interviews, system design intro, timed sets. Slate/upcoming.
  - Under each phase, show 3–4 compact topic rows: a status dot (teal check = done, teal ring = current, hollow = upcoming), topic name (ink), a JetBrains Mono "problems 8/12" count, and a small right chevron. Rows have 1px dividers.
- **Right summary rail (stacked white cards):**
  - **Today card:** "Today · Day 12" heading, one highlighted lesson ("Binary Trees — Level Order Traversal") and 2 practice problems with difficulty tags (Easy/Medium in teal-tinted or slate pills), a teal "Start today" button.
  - **Stats card:** JetBrains Mono metrics — Problems solved 46, Current streak 12d, Est. finish "Nov 14", Weekly pace "on track" with a small teal check.
  - **Milestones card:** upcoming milestone badges as clean line-icon rows (e.g. "50 problems", "First graph problem", "First mock interview") with dates.
- Feel: a serious, motivating study plan — structured like a syllabus, warm and premium, never gamified-childish.

---

## PAGE 43 — Daily Study Workspace

Title in top bar: "Day 12 · Binary Trees". The focused daily execution screen a student sees when following the roadmap. Three-region layout inside the content area.

- **Top day strip (white card):** left = ink "Day 12 of 90" with slate phase label "Core Structures"; center = a horizontal day scroller of small square day chips (…9 10 11 [12] 13 14…) with completed days in teal check, current day 12 as a filled teal square, future days hollow slate; right = JetBrains Mono "1h 30m planned · 42m done" with a slim teal time-progress bar.
- **Left column — Today’s checklist (~35%, white card):** heading "Today’s plan". A vertical checklist:
  - ✔ Watch: "Tree traversal basics" (12m) — checked, teal.
  - ✔ Lesson: "BFS on trees" — checked, teal.
  - ◻ Practice: "Level Order Traversal" (Medium) — current, teal ring highlight.
  - ◻ Practice: "Minimum Depth of Binary Tree" (Easy).
  - ◻ Review: 2 flashcards due.
  Each item = status control + title (ink) + type/difficulty tag + time estimate (JetBrains Mono). A soft teal wash "Up next" marker on the current item.
- **Right column — Active problem (~65%, white card):** a clean coding problem view. Problem title "Level Order Traversal" with a Medium tag, short prose statement, a small example I/O block in JetBrains Mono on paper-tinted background, and a **light-theme code editor** panel (white background, subtle line numbers in slate, restrained syntax colors: teal keywords, ink identifiers, slate comments — never neon). Editor toolbar: language pill "Python", Run and Submit buttons (Submit = teal). A collapsed "Hints (2)" row and a slim results strip below reading "Ready" in slate.
- **Bottom bar:** left ghost "Previous", center JetBrains Mono "Daily goal 3/5 tasks", right teal "Mark day complete" button (slightly disabled-looking until tasks done) with a small streak-flame reminder.
- Keep it distraction-free, confident, and premium: a student sits down, sees exactly what to do today, and executes.

---

## IMPORTANT (applies to all 3 screens)

- Render as a real, polished product screenshot — pixel-crisp UI, aligned grids, consistent 1px borders, real-looking student data and copy.
- Strictly obey the shared visual system and app shell. Same sidebar, same top bar, same colors and type on every screen.
- Light theme only. No dark editor, no gradients, no purple, no emojis, no glows, no abstract decoration.
- Use JetBrains Mono for every number, day count, timer, and code element; Instrument Sans everywhere else.
- 16:9, 1440x900, no device frame or browser chrome.
