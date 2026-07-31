# Algora — Admin Suite (9 pages)

> Image-generation prompts for GPT-4o / "gpt image 2". Each prompt renders ONE complete, pixel-perfect internal admin screen as a single **16:9 desktop** screenshot. Copy-paste one block at a time. This is the staff-facing back office for running the Algora platform — operational, data-rich, trustworthy, and clearly distinct from the student app while staying strictly on-brand.

**Brand recap (do not deviate):**
- PRODUCT: "algora" — a gamified algorithm-learning platform. These are the ADMIN / STAFF console screens. Tagline: "See the algorithm think."
- VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; cards pure white #FFFFFF; hairline borders #E4E9E7. Text near-black ink #0E1513 for headings, muted slate #5B6763 for secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for primary buttons, active nav, key metrics, links, and the logo glyph only. A muted amber and a muted red may appear ONLY as tiny status accents (warnings, failed payments, suspended) — never as large fills. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat solid colors, crisp edges, soft realistic light shadows. Instrument Sans for headings/body; JetBrains Mono for stats, IDs, dates, table data, and labels. Corners 12–16px, 1px hairline borders, WCAG-AA, 4k ultra high-fidelity.

**Shared ADMIN SHELL (every screen except the Admin login uses this):**
- A persistent LEFT SIDEBAR (~240px, white, hairline right border): top = "algora" wordmark + teal two-node glyph with a small mono "ADMIN" tag beside it. A vertical nav of mono items with small consistent teal line icons: "Dashboard", "Students", "Content", "Subscriptions", "Analytics", "Settings" — the current page shown ACTIVE (teal text, pale-teal rounded highlight, teal left bar). Bottom of sidebar = a small admin identity chip (monogram avatar, mono name "Maya Chen", role label "Super Admin").
- A persistent TOP BAR (white, hairline bottom border): left = the page title in ink + a slate breadcrumb; center = a wide search field (white, hairline border, teal search icon, placeholder "Search students, lessons, invoices…"); right = a mono environment pill "PROD", a teal-dot notifications bell, and the admin monogram avatar.
- MAIN CONTENT sits on the paper background to the right of the sidebar with generous padding.

---

## A1. Admin login

> Generate ONE complete, pixel-perfect internal admin sign-in screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. This screen does NOT use the admin shell.
>
> PRODUCT: "algora" ADMIN console. This is the STAFF LOGIN screen — a restricted, security-forward sign-in. Tagline context only.
>
> VISUAL SYSTEM — LIGHT THEME (strict): paper #F7F9F8; card white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 body. ONE accent teal #0E9C86 (highlight #14B8A6) for the primary button, focused field, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels and the security note. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> LAYOUT: a calm centered SIGN-IN CARD (white, hairline border, soft shadow, ~440px) on the paper background. Inside, top to bottom: the "algora" wordmark + teal two-node glyph with a mono "ADMIN" tag; an ink headline "Staff sign in"; a slate subline "Restricted access. Authorized team members only."; a "Work email" field (white, hairline border, mono label) with a focused teal ring on one field; a "Password" field with a slate show/hide eye icon; a "2FA code" field with mono placeholder "6-digit code" and a small teal "authenticator" hint; a solid teal full-width "Sign in securely" button; a ghost text link "Lost your device? Contact IT". A slim pale-teal security callout with a teal shield line icon: "All admin access is logged and monitored." A mono footer line centered: "algora · internal · v3.2".
>
> IMPORTANT: ONE clean single-screen light UI, security-forward but friendly, realistic legible copy (no lorem, no misspellings), no real people or photos, consistent alignment, single cohesive light design language matching Algora.

---

## A2. Admin dashboard (overview)

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Dashboard" active.
>
> PRODUCT: "algora" ADMIN. This is the OVERVIEW DASHBOARD — the operational pulse of the platform.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink headings #0E1513, slate #5B6763. ONE accent teal #0E9C86 (highlight #14B8A6); amber/red only as tiny status dots. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans headings; JetBrains Mono for all numbers, deltas, dates. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT:
> - A page header row: ink "Dashboard", slate "Platform overview", and a right-aligned mono date-range selector "Last 30 days ▾" plus a ghost "Export" button.
> - A KPI ROW of four white stat cards, each with a mono label, a big ink number, and a small teal delta chip: "Active students 48,210 ▲ 6.2%", "New signups (30d) 3,940 ▲ 11%", "MRR $182,400 ▲ 4.1%", "Lessons completed 1.2M ▲ 8%". One card shows an amber delta to vary.
> - A wide white CHART CARD "Signups & active users": a clean line/area chart with two teal-toned lines over a light grid, a small legend, and mono axis labels (weeks). Flat, crisp, no glow.
> - A right-column stack: a white "Live activity" card listing ~5 mono rows (student id, event "completed BFS lesson", timestamp) with tiny teal dots; and a white "System health" card with 3 rows ("Visualizer service · operational" teal dot, "Payments · operational" teal dot, "Email delivery · degraded" amber dot) and a ghost "Status page →" link.
> - A bottom white "Needs attention" table: mono columns Item / Type / Priority / Assignee, ~4 rows (e.g. "12 failed payments" red dot, "3 flagged reviews" amber dot, "New campus request" teal dot), each with a right ghost "Resolve" action.
>
> IMPORTANT: ONE clean single-screen light admin UI, realistic legible data (no lorem, no misspellings), status colors used only as tiny dots/chips, consistent alignment and typographic hierarchy, single cohesive light design language matching Algora.

---

## A3. Students (management list)

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Students" active.
>
> PRODUCT: "algora" ADMIN. This is the STUDENT MANAGEMENT list — searchable, filterable, bulk-actionable.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards/tables white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86; amber/red only as tiny status chips. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for IDs, dates, XP, plan labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT:
> - Header row: ink "Students", slate "48,210 total", right-aligned solid teal "Invite student" button + ghost "Export CSV".
> - A FILTER BAR (white card): a search field (teal icon), plus mono filter dropdowns "Plan: All ▾", "Status: All ▾", "Signup: Last 90d ▾", and a ghost "Clear filters".
> - A large STUDENTS TABLE (white, hairline row separators): a header row with a select-all checkbox and mono column labels — Student / Email / Plan / XP / Streak / Status / Joined / (actions). ~9 rows: each with a small circular monogram avatar (teal on pale-teal initials) + ink name, mono email, a plan chip ("Free" gray / "Pro" teal), mono XP ("12,480"), mono streak ("23d" with a tiny teal flame glyph), a status chip ("Active" teal / "Trial" amber / "Suspended" red), mono join date, and a right kebab menu icon. One row shown selected (pale-teal highlight).
> - A BULK ACTION strip appears above the table when rows are selected: "2 selected" + ghost buttons "Message", "Change plan", "Suspend".
> - A footer PAGINATION row: mono "Showing 1–9 of 48,210" and teal page controls "‹ 1 2 3 … 214 ›" with a "Rows: 25 ▾" selector.
>
> IMPORTANT: ONE clean single-screen light admin UI, dense but readable table, realistic legible data (no lorem, no misspellings), status colors only as small chips, consistent alignment, single cohesive light design language matching Algora.

---

## A4. Student detail

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Students" active (breadcrumb "Students / Arjun Patel").
>
> PRODUCT: "algora" ADMIN. This is a single STUDENT DETAIL / account record — everything staff need to support one learner.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86; amber/red only as tiny chips. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for IDs, dates, XP, metrics. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT (two-column):
> - PROFILE HEADER card (wide, white): a larger circular monogram avatar (teal on pale-teal initials "AP"), ink name "Arjun Patel", mono user id "usr_8f2a41" + email, a teal "Pro" plan chip and a teal "Active" status chip; right-aligned ghost actions "Message", "Reset password", "Impersonate", and a subtle red-text "Suspend".
> - LEFT COLUMN: a "Learning summary" white card with a mono stat grid (Level 12, 12,480 XP, 23-day streak, 84% mastery) and a small teal progress ring; below it an "Enrolled paths" card listing 3 paths with teal mini progress bars; and a "Devices & sessions" card with 2 mono rows (browser, last active, location) and a ghost "Revoke" per row.
> - RIGHT COLUMN: a "Billing" white card (plan "Pro · $12/mo", next renewal date, payment method "•••• 4242", a green/teal "Paid" chip) with ghost "View invoices"; and an "Activity timeline" card — a vertical timeline with small teal node dots and mono entries ("Completed Dijkstra lesson", "Earned 'Graph Explorer' badge", "Renewed subscription", each with a timestamp).
>
> IMPORTANT: ONE clean single-screen light admin UI, realistic legible data (no lorem, no misspellings, no real personal data), status colors only as chips, consistent alignment and hierarchy, single cohesive light design language matching Algora.

---

## A5. Content management

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Content" active.
>
> PRODUCT: "algora" ADMIN. This is the CONTENT MANAGEMENT screen — where staff manage lessons, algorithms, and learning paths.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards/tables white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86; amber only as a tiny "Draft" status chip. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for ids, counts, dates, difficulty labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT:
> - Header row: ink "Content", slate "Lessons, algorithms & paths", right-aligned solid teal "New lesson" button + ghost "Import".
> - A SEGMENTED TAB control (mono): "Lessons" (active teal underline), "Algorithms", "Paths".
> - A left mini-sidebar of CATEGORIES (paper/ghost card): mono list "All", "Arrays", "Graphs", "Trees", "Sorting", "Dynamic Programming", with counts; "Graphs" active in teal.
> - A CONTENT TABLE (white): mono columns Title / Category / Difficulty / Status / Completions / Updated / (actions). ~8 rows, each: an ink lesson title ("Breadth-First Search", "Dijkstra's Shortest Path", "Quicksort partition"), a category chip, a difficulty chip ("Beginner"/"Intermediate"/"Advanced" in pale-teal tints), a status chip ("Published" teal / "Draft" amber), mono completions ("18,240"), mono updated date, and right edit/kebab icons. One draft row visible.
> - A right-side "Path builder preview" white card (optional accent): a small vertical skill-tree with teal connected nodes and a couple of gray locked nodes, illustrating how lessons chain into a path, with a ghost "Open builder →".
>
> IMPORTANT: ONE clean single-screen light admin UI, realistic legible content titles (no lorem, no misspellings), status/difficulty as small chips, consistent alignment, single cohesive light design language matching Algora.

---

## A6. Subscriptions & billing

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Subscriptions" active.
>
> PRODUCT: "algora" ADMIN. This is the SUBSCRIPTIONS & BILLING console — revenue, plans, and invoices.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards/tables white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86; amber/red only as tiny "Past due"/"Failed" chips. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for money, dates, invoice ids. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT:
> - Header row: ink "Subscriptions", slate "Revenue & billing", right-aligned mono "Last 30 days ▾" + ghost "Export".
> - A KPI ROW of four white cards with mono numbers and small teal deltas: "MRR $182,400 ▲ 4.1%", "Active subs 15,120 ▲ 3%", "Trials 1,240", "Churn 1.8% ▼ 0.3%" (a positive teal down-delta).
> - A wide white "Revenue trend" chart card: a clean teal area chart over a light grid with mono month labels; a small legend "MRR".
> - A PLAN BREAKDOWN row: three white cards "Free 33,090", "Pro $12/mo · 14,010", "Campus (custom) · 1,110", each with a thin teal share bar and mono percentages.
> - A RECENT INVOICES table (white): mono columns Invoice / Customer / Plan / Amount / Status / Date / (actions). ~7 rows with mono invoice ids ("inv_20482"), a monogram + name, plan chip, mono amount ("$12.00"), a status chip ("Paid" teal / "Past due" amber / "Failed" red), mono date, and a ghost "View" per row.
>
> IMPORTANT: ONE clean single-screen light admin UI, realistic legible financial placeholder data (no lorem, no misspellings), status colors only as small chips, consistent alignment, single cohesive light design language matching Algora.

---

## A7. Analytics

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Analytics" active.
>
> PRODUCT: "algora" ADMIN. This is the ANALYTICS screen — engagement, learning outcomes, and funnels.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86 (with the lighter #14B8A6 as a secondary chart tone only). NO dark backgrounds, NO purple, NO rainbow chart palettes, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for numbers, %, axis labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT:
> - Header row: ink "Analytics", slate "Engagement & outcomes", right-aligned mono "Last 90 days ▾", a mono "Segment: All students ▾", and a ghost "Export".
> - A KPI ROW: four white cards — "DAU 21,400", "Avg session 18m", "Lesson completion 74%", "7-day retention 58%" — mono numbers + tiny teal deltas.
> - A CHART GRID (2×2 of white cards, all teal-toned, flat, crisp over light grids): (1) "Active users" area chart; (2) "Signup → activation funnel" a clean horizontal funnel with 4 teal bars and mono drop-off % labels; (3) "Lessons completed by topic" a simple horizontal bar chart (Graphs, Sorting, Trees, DP, Arrays) in teal tints; (4) "Retention cohort" a light heat-grid where cell intensity is pale→teal (NO rainbow), mono week headers.
> - A bottom white "Top lessons" table: mono columns Lesson / Starts / Completion % / Avg time, ~5 rows with tidy mono values.
>
> IMPORTANT: ONE clean single-screen light analytics UI, teal-only chart palette (light→teal tints, never rainbow), realistic legible numbers (no lorem, no misspellings), consistent alignment and hierarchy, single cohesive light design language matching Algora.

---

## A8. Admin settings

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with "Settings" active.
>
> PRODUCT: "algora" ADMIN. This is the PLATFORM SETTINGS screen — team members, roles, and system configuration.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards/tables white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86 (teal toggles/active states). NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for roles, dates, labels. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT (settings layout with a left sub-nav):
> - A LEFT SETTINGS SUB-NAV (paper/ghost card, ~220px): mono items "Team members" (active teal), "Roles & permissions", "Billing config", "Integrations", "Security", "Branding". 
> - RIGHT PANE — "Team members": header ink "Team members" + slate "Manage who has admin access", right solid teal "Invite teammate". A white TEAM TABLE: mono columns Member / Role / Last active / Status / (actions); ~5 rows each with a monogram avatar + name, a role chip ("Super Admin" teal / "Editor" / "Support" / "Analyst" in pale tints), mono last-active, a status chip ("Active" teal / "Invited" amber), and a right kebab. 
> - Below the table, a "Permissions preview" white card: a compact matrix — rows = capabilities ("Manage students", "Edit content", "View billing", "Change settings"), columns = roles, cells = teal checkmarks or slate dashes.
> - A bottom "Save changes" bar (right-aligned): ghost "Cancel" + solid teal "Save".
>
> IMPORTANT: ONE clean single-screen light admin settings UI, realistic legible copy (no lorem, no misspellings), teal toggles/checks, role chips as small labels, consistent alignment, single cohesive light design language matching Algora.

---

## A9. Admin profile & security

> Generate ONE complete, pixel-perfect internal admin screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped. Use the shared ADMIN SHELL with the admin identity chip active (breadcrumb "Settings / My profile").
>
> PRODUCT: "algora" ADMIN. This is the ADMIN'S OWN PROFILE & SECURITY screen — the staff member's personal account and access controls.
>
> VISUAL SYSTEM — LIGHT THEME (strict, identical): paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513, slate #5B6763. ONE accent teal #0E9C86; amber/red only as tiny security-status accents. NO dark backgrounds, NO purple, NO gradients, NO photos, NO emojis. Instrument Sans; JetBrains Mono for ids, dates, session data. Corners 12–16px, 1px borders, WCAG-AA, 4k.
>
> MAIN CONTENT (two-column):
> - PROFILE card (wide, white): a larger circular monogram avatar (teal on pale-teal initials "MC"), ink name "Maya Chen", mono "Super Admin · staff_0041", email; a ghost "Change avatar" and inline editable fields (Full name, Display name, Work email) with mono labels, one field focused with a teal ring; a bottom-right solid teal "Save profile".
> - LEFT COLUMN — "Security" white card: rows for "Password" (mono "Last changed 42 days ago" + ghost "Update"), "Two-factor authentication" (a teal toggle ON + mono "Authenticator app"), "Backup codes" (mono "6 remaining" + ghost "Regenerate"); a slim pale-teal callout "All admin actions are logged."
> - RIGHT COLUMN — "Active sessions" white card: ~3 mono rows (device/browser, location, last active) with the current session tagged teal "This device" and the others with a ghost red-text "Revoke"; and a "Recent admin activity" card — a vertical timeline with teal node dots and mono entries ("Suspended usr_4471", "Published lesson 'Dijkstra'", "Exported billing report") each with a timestamp.
> - A bottom subtle red-text "Sign out of all sessions" ghost action.
>
> IMPORTANT: ONE clean single-screen light admin UI, security-forward, realistic legible data (no lorem, no misspellings, no real personal data), teal toggles/checks with minimal amber/red status accents, consistent alignment and hierarchy, single cohesive light design language matching Algora.
