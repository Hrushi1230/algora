# Algora — Section 6: Account (5 pages)

Image-generation prompts for GPT-4o / "gpt image 2". Each prompt renders ONE complete, pixel-perfect SaaS screen as a single **16:9 desktop** screenshot. Copy-paste one block at a time. These are the identity, progress, and settings screens — calm, premium, trustworthy, always on-brand.

**Brand recap (do not deviate):**
Algora — a gamified platform where CS students master algorithms through synchronized visualization, code, and plain-English explanation. Tagline: *"See the algorithm think."*
Light theme only. Paper background, ink text, one teal accent. Instrument Sans (headings/body) + JetBrains Mono (code, labels, stats).

**Shared visual system (paste inside every prompt):**
- Background warm off-white paper #F7F9F8; elevated cards pure white #FFFFFF; hairline borders #E4E9E7.
- Text near-black ink #0E1513 for headings, muted slate #5B6763 for secondary text.
- ONE accent: teal #0E9C86 (highlight #14B8A6) — used only for primary buttons, active/selected states, focus rings, progress, XP, streaks, links, and the logo glyph.
- NO dark backgrounds anywhere, NO black panels, NO purple, NO rainbow gradients, NO glowing blobs/orbs, NO stock photos of people, NO emojis, NO cartoon mascots. Flat solid colors, crisp edges, soft realistic light shadows only.
- Type: Instrument Sans for headlines (large, tight, geometric); JetBrains Mono for stats, field labels, dates. Corners 12–16px, 1px hairline borders, pale-teal focus ring, generous whitespace, high contrast, WCAG-AA. Ultra high-fidelity, 4k, clean.

**Shared APP SHELL convention (paste inside every prompt in this section):**
- A persistent LEFT SIDEBAR (white, ~240px, hairline right border): top = "algora" wordmark + small teal two-node graph glyph. A vertical nav of mono-labeled items with small teal line icons: "Dashboard", "Explore", "My Path", "Practice", "Review", "Compete", "Achievements" — the current page shown ACTIVE with a pale-teal tint pill and a teal left indicator bar. Bottom of sidebar: a compact user chip (initials avatar circle "AR", ink name "Arjun R.", mono "Lvl 12") and a slim teal XP progress bar.
- A persistent TOP BAR (white, hairline bottom border): left = page title / breadcrumb in ink; center = a wide search field with mono placeholder "Search algorithms, lessons…"; right = a teal flame streak chip "23", a mono XP chip "2,150 XP", a bell notification icon with a tiny teal dot, and the user avatar.
- The MAIN CONTENT sits on paper background to the right of the sidebar, below the top bar, with generous padding and a clear content grid.

---

## PROMPT — 31. Public profile (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is a student's PUBLIC PROFILE (a shareable page showing their identity, level, badges, and activity). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for level, badges earned, progress, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for stats, handle, dates. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR (no item active, or a subtle "Profile" affordance in the user chip); persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT (paper background):
- A PROFILE HEADER card (white, wide, hairline border): a large initials avatar circle "AR" in a pale-teal tint, ink display name "Arjun Rao" + mono handle "@arjun", a slate one-line bio ("CS undergrad · loves graphs & DP"), a small teal "Lvl 12" pill and a mono "Joined Mar 2025" note. Right side: a ghost "Share profile" button and a teal "Follow" button.
- A row of FOUR white stat cards with mono labels: "Skills mastered · 18", "Day streak · 23", "Total XP · 24,150", "Rank · Teal League".
- A left column "Badges" white card: a small grid of ~8 flat geometric badge medallions (teal earned / gray locked) with mono names beneath, plus a "View all 24 →" teal link.
- A main "Recent activity" white card: a vertical timeline of ~5 rows, each with a small teal line icon, ink line ("Mastered Dijkstra's Algorithm", "Earned 'Graph Master' badge", "Completed Sorting path"), and a mono relative date ("2d ago").
- A right "Learning paths" white card: 3 slim path rows each with an ink title, a slim teal progress bar, and a mono "%".

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), no real people or photos, consistent alignment, single cohesive light design language matching the Algora product screens.

---

## PROMPT — 32. Personal progress / analytics (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the PERSONAL PROGRESS / ANALYTICS screen (the student's private dashboard of their own learning data over time). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for chart lines/bars, progress, buttons, links, logo glyph only — charts use teal as the single data color with pale-teal fills; gridlines are hairline gray. NO dark backgrounds, NO black panels, NO purple, NO multi-color chart palettes, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for axis labels, values, dates. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR with "Dashboard" ACTIVE; persistent TOP BAR with search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT:
- Header: ink headline "Your progress" + slate subline "How you're learning over time." A right-aligned mono date-range segmented control "7d / 30d / All" with "30d" active in teal.
- A row of FOUR white KPI cards with mono labels and a tiny teal sparkline each: "XP this month · 4,120 ↑", "Problems solved · 86", "Avg accuracy · 78%", "Study time · 14h".
- A large "XP over time" line-chart card (white, dominant): a clean teal line with a pale-teal area fill, hairline gridlines, mono X-axis dates and Y-axis values, a subtle hover tooltip showing "May 18 · +180 XP".
- A "Topic mastery" horizontal bar-chart card: ~6 topic rows ("Arrays", "Sorting", "Graphs", "Trees", "DP", "Greedy") each a teal bar with a mono "%" and a pale track.
- A "Accuracy by difficulty" small card: 3 slim teal bars ("Easy 92%", "Medium 74%", "Hard 55%").
- A "Weak spots" white card: 3 rows suggesting topics to review, each with an ink title, a mono "accuracy 58%", and a teal "Review →" link.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic clean single-accent charts (teal only, no rainbow), legible placeholder data (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 33. Account settings (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the ACCOUNT SETTINGS screen (profile info, security, and preferences). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for active toggles, selected settings-nav item, primary buttons, focus rings, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for field labels. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR (user chip context); persistent TOP BAR with breadcrumb "Settings", search, streak, XP, bell, avatar — as per the shared convention.

MAIN CONTENT (a two-pane settings layout):
- A LEFT SETTINGS SUB-NAV (white card, ~220px) with mono items: "Profile" (ACTIVE, teal tint pill), "Security", "Preferences", "Notifications", "Billing", "Danger zone" (muted). 
- A RIGHT SETTINGS PANEL (white card, dominant) titled ink "Profile":
  - An avatar row: a large initials avatar "AR" in pale teal with a ghost "Change photo" button and a mono note "PNG or JPG, up to 2MB".
  - Form fields with mono labels and outlined inputs: "Full name" ("Arjun Rao"), "Username" ("@arjun"), "Email" ("arjun@example.com" with a small teal "Verified" chip), "Bio" (a small textarea), "Country" (select). Fields sit in a tidy two-column grid with the bio full-width; one field shows a pale-teal focus ring.
  - A "Security" preview block below with rows: "Password ········ · Change", "Two-factor authentication" with a teal ON toggle, "Active sessions · 2 devices · Manage".
  - A sticky footer bar inside the panel: a mono "Unsaved changes" note (left), a ghost "Cancel" and a solid teal "Save changes" button (right).

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment and form spacing, single cohesive light design language matching the Algora product screens.

---

## PROMPT — 34. Subscription and billing (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the SUBSCRIPTION AND BILLING screen (current plan, payment method, and invoice history). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for the active plan, "Paid" status, primary buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis, NO real card-brand logos (use a neutral flat card glyph). Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for prices, dates, invoice IDs. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR; persistent TOP BAR with breadcrumb "Settings · Billing", search, streak, XP, bell, avatar — as per the shared convention. (A left settings sub-nav with "Billing" ACTIVE may be shown for consistency with page 33.)

MAIN CONTENT:
- Header: ink headline "Subscription & billing" + slate subline "Manage your plan and payment details."
- A CURRENT PLAN card (white, wide, pale-teal accent border/left bar): a teal "Pro" pill, ink "Pro — Annual", a big mono price "$96 / year" with a slate "renews Mar 3, 2026", a small feature bullet row (mono "Unlimited paths · All visualizers · Priority review"), and right-aligned ghost "Change plan" + subtle text "Cancel subscription" link.
- A "Payment method" white card: a neutral flat card glyph, mono "•••• 4242", ink "Visa · exp 08/27", a small teal "Default" chip, and a ghost "Update" button.
- A "Billing history" white card (dominant, table): columns mono "Invoice", "Date", "Amount", "Status", "" — ~5 rows ("INV-2041 · Mar 3 2025 · $96.00 · Paid", …) with teal "Paid" status chips and a teal "PDF ↓" download link per row.
- A right rail "Usage this cycle" white card: 2 slim teal progress rows ("Paths in progress 4", "Visualizer runs 320") and a mono "Next invoice: $96 on Mar 3, 2026".

IMPORTANT: ONE clean single-screen light desktop app UI, no real payment-brand logos or real card numbers, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 35. Notifications (light)

Generate ONE complete, pixel-perfect SaaS app screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport with the app shell, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is the NOTIFICATIONS screen (an inbox of activity plus per-channel notification preferences). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for unread dots, active toggles, selected filter, buttons, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for timestamps, labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.

APP SHELL: persistent LEFT SIDEBAR; persistent TOP BAR with breadcrumb "Notifications", search, streak, XP, a bell with a teal unread dot, avatar — as per the shared convention.

MAIN CONTENT (a two-column layout):
- LEFT — an INBOX column (dominant, white card): header ink "Notifications" with a mono "5 unread" chip and a ghost "Mark all read" link; a mono filter segmented control "All / Unread / Mentions" with "All" active in teal. Below, a vertical list of ~7 notification rows, each: a small teal line icon in a pale-teal square (badge earned, streak reminder, path recommendation, leaderboard change, reply, weekly recap), an ink title line ("You earned the 'Graph Master' badge", "You dropped to #9 in Teal League", "New lesson added to your path"), a slate one-line detail, and a right mono timestamp ("2h", "Yesterday", "Jun 12"). UNREAD rows have a small teal dot at left and a very faint pale-teal tint; read rows are plain white. Group headers mono "Today", "Earlier".
- RIGHT — a "Preferences" white card (~320px): ink "How you're notified" with rows for each type ("Streak reminders", "Achievements", "Path updates", "Leaderboard", "Weekly recap"), each row showing two small toggles labeled mono "Email" and "Push" — active ones teal ON, others gray OFF; a "Quiet hours" row with a mono time range "22:00 – 08:00"; a solid teal "Save preferences" button at the bottom.

IMPORTANT: ONE clean single-screen light desktop app UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora product screens.
