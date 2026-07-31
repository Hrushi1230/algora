# Algora — Section 3: Onboarding (3 pages)

Image-generation prompts for GPT-4o / "gpt image 2". Each prompt renders ONE complete, pixel-perfect SaaS screen as a single **16:9 desktop** screenshot. Copy-paste one block at a time.

**Brand recap (do not deviate):**
Algora — a gamified platform where CS students master algorithms through synchronized visualization, code, and plain-English explanation. Tagline: *"See the algorithm think."*
Light theme only. Paper background, ink text, one teal accent. Instrument Sans (headings/body) + JetBrains Mono (code, labels, stats).

**Shared visual system (paste inside every prompt):**
- Background warm off-white paper #F7F9F8; elevated cards pure white #FFFFFF; hairline borders #E4E9E7.
- Text near-black ink #0E1513 for headings, muted slate #5B6763 for secondary text.
- ONE accent: teal #0E9C86 (highlight #14B8A6) — used only for primary buttons, active/selected states, focus rings, progress, links, and the logo glyph.
- NO dark backgrounds anywhere, NO black panels, NO purple, NO rainbow gradients, NO glowing blobs/orbs, NO stock photos of people, NO emojis. Flat solid colors, crisp edges, soft realistic light shadows only.
- Type: Instrument Sans for headlines (large, tight, geometric); JetBrains Mono for code, badges, stats, field labels. Corners 12–16px, 1px hairline borders, pale-teal focus ring, generous whitespace, high contrast, WCAG-AA. Ultra high-fidelity, 4k, clean.
- Onboarding layout convention: a **16:9 landscape desktop viewport** (single screen, NOT a long scrolling page). Thin white top bar with the wordmark and a step progress indicator. A centered onboarding "wizard" card on paper, wide but not full-width (~880–960px), with a persistent step tracker. Small mono footer line. All three screens share the same stepper so they read as one flow.

---

## PROMPT — 14. Learning goals (light)

Generate ONE complete, pixel-perfect SaaS onboarding screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Render a single full desktop viewport, nothing cropped, nothing cut off.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is ONBOARDING STEP 1 of 3: LEARNING GOALS. Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict): Background warm off-white paper #F7F9F8; cards pure white #FFFFFF; hairline borders #E4E9E7. Text near-black ink #0E1513 headings, muted slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for primary button, selected states, focus, progress, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Type: Instrument Sans headlines; JetBrains Mono for labels, badges, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k ultra high-fidelity.

TOP BAR (thin, white, hairline bottom border): left "algora" wordmark in mono with a small teal two-node graph glyph. Center a compact 3-step progress tracker: "1 Goals · 2 Assessment · 3 Your path" with step 1 active in teal (filled dot + teal label), steps 2–3 muted slate. Right a muted slate mono link "Skip for now".

LAYOUT — CENTERED WIZARD CARD (white card with hairline border on paper, ~920px wide, generous whitespace):
- Small mono pill badge "◆ STEP 1 OF 3" (teal on pale-teal tint).
- Ink headline "What brings you to Algora?" (period as a small teal square). Slate subhead: "Pick your goals so we can shape the right path. Choose all that apply."
- A responsive grid of FOUR selectable goal cards (2×2), each a white tile with hairline border, a small teal line icon (24px), a bold ink title, and a short slate sentence. Two of them shown SELECTED with a teal border, pale-teal tint, and a teal check in the corner:
  1) "Interview prep" — "Crack FAANG-style DS&A questions." (selected)
  2) "Ace my coursework" — "Keep up with CS classes and exams." (selected)
  3) "Competitive programming" — "Train speed and pattern recognition."
  4) "Curiosity & fundamentals" — "Truly understand how algorithms work."
- Below, a mono label "Weekly time commitment" over a horizontal segmented selector with four pill options: "Casual · 1–2h", "Steady · 3–5h", "Focused · 6–9h", "Intense · 10h+" — with "Steady · 3–5h" selected in teal.
- A mono label "Experience level" over three pill options "Beginner", "Intermediate", "Advanced" — "Intermediate" selected in teal.
- Footer row inside the card: left ghost outline button "Back" (disabled/muted), right solid teal primary button "Continue" with a small right-arrow.

FOOTER: small centered mono slate line "© 2026 Algora · Personalizing your experience · Reduced-motion friendly".

IMPORTANT: ONE clean single-screen light desktop UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora marketing and auth screens.

---

## PROMPT — 15. Skill assessment (light)

Generate ONE complete, pixel-perfect SaaS onboarding screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is ONBOARDING STEP 2 of 3: SKILL ASSESSMENT (a short diagnostic quiz that calibrates the path). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical to step 1): Background paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for primary button, selected/active states, focus, progress, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for code, labels, badges. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

TOP BAR (thin, white, hairline bottom border): left "algora" wordmark + teal two-node graph glyph. Center the same 3-step tracker "1 Goals · 2 Assessment · 3 Your path" with step 1 shown COMPLETE (teal check), step 2 ACTIVE in teal, step 3 muted. Right muted slate mono link "Skip assessment".

LAYOUT — CENTERED WIZARD CARD (white card with hairline border on paper, ~940px wide):
- Top row inside the card: left mono pill badge "◆ QUESTION 4 OF 8", right a slim teal progress bar about half full with a mono "50%" label.
- Ink headline "What does this traversal visit first?" (period as small teal square). Slate subhead: "No pressure — this just calibrates your starting point."
- A two-column question body:
  - LEFT: a small WHITE visualizer sub-card with hairline border showing a binary tree of 7 numbered nodes with connecting edges — the root highlighted teal as "Start", the rest white/gray; a tiny mono legend.
  - RIGHT: a compact code sub-card (white, subtle line numbers) in JetBrains Mono showing a short BFS/DFS snippet, with a small "Python ▾" selector.
- Below, FOUR multiple-choice answer rows, each a white pill/row with hairline border, a mono letter chip (A/B/C/D), and ink answer text. One option shown SELECTED with a teal border, pale-teal tint, and a teal radio dot. Options like: "A) The left subtree entirely", "B) Level by level, breadth-first" (selected), "C) The deepest node first", "D) A random node".
- Footer row inside the card: left ghost outline "Back", center a muted slate mono link "I'm not sure — skip", right solid teal primary button "Next question" with a right-arrow.

FOOTER: small centered mono slate line "© 2026 Algora · Calibrating your path · Reduced-motion friendly".

IMPORTANT: ONE clean single-screen light desktop UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, matching the Algora design language.

---

## PROMPT — 16. Personalized path result (light)

Generate ONE complete, pixel-perfect SaaS onboarding screen as a single landscape screenshot (aspect ratio 16:9), rendered as a real product UI — NOT an illustration, NOT a collage. Single full desktop viewport, nothing cropped.

PRODUCT: "algora" — a gamified algorithm-learning platform. This is ONBOARDING STEP 3 of 3: PERSONALIZED PATH RESULT (the generated custom learning plan). Tagline: "See the algorithm think."

VISUAL SYSTEM — LIGHT THEME (strict, identical to the other onboarding steps): Background paper #F7F9F8; cards white #FFFFFF; hairline borders #E4E9E7. Ink #0E1513 headings, slate #5B6763 secondary. ONE accent teal #0E9C86 (highlight #14B8A6) for primary button, active states, progress, links, logo glyph only. NO dark backgrounds, NO black panels, NO purple, NO gradients/blobs, NO stock photos of people, NO emojis. Flat colors, crisp edges, soft light shadows. Instrument Sans headlines; JetBrains Mono for labels, badges, stats. Corners 12–16px, 1px borders, pale-teal focus ring, WCAG-AA, 4k.

TOP BAR (thin, white, hairline bottom border): left "algora" wordmark + teal two-node graph glyph. Center the 3-step tracker "1 Goals · 2 Assessment · 3 Your path" with steps 1 & 2 COMPLETE (teal checks) and step 3 ACTIVE in teal. Right a muted slate mono line "Signed in as arjun@stanford.edu".

LAYOUT — CENTERED RESULT CARD (white card with hairline border on paper, ~960px wide):
- A small mono pill badge "◆ YOUR PATH IS READY" (teal on pale-teal). Ink headline "Your personalized path: Interview Prep Fast-Track." (period as small teal square). Slate subhead: "Built from your goals and assessment — 42 lessons across 6 skills, tuned to ~4h/week."
- A summary stat row of three white mini-cards with mono labels: "Level start · Intermediate", "Est. completion · 7 weeks", "Weekly XP goal · 1,200 XP" (the XP value in teal).
- A MAIN two-column body:
  - LEFT (wider): a "Your skill roadmap" WHITE sub-card showing a small horizontal skill tree / path of ~6 connected nodes — the first node teal "Start here: Arrays & Two Pointers", the next two pale-teal "Up next", the rest gray "Locked" with small lock icons; connecting hairline edges.
  - RIGHT (narrower): a "First 3 lessons" list, each a white row with a small teal line icon, ink lesson title, and a mono duration chip: "Two Pointers · 20m", "Sliding Window · 25m", "BFS on Grids · 30m". Below, a teal XP progress ring reading "Lvl 1" with "0 / 1,200 XP".
- A reassurance line in slate mono: "You can adjust goals anytime in settings."
- Footer row inside the card: left ghost outline "Adjust goals", right solid teal primary button "Start learning" with a right-arrow. A small mono slate microcopy under the button: "Jump straight into your first visualized lesson."

FOOTER: small centered mono slate line "© 2026 Algora · Welcome aboard · Reduced-motion friendly".

IMPORTANT: ONE clean single-screen light desktop UI, realistic legible placeholder copy (no lorem, no misspellings), consistent alignment, single cohesive light design language matching the Algora marketing, auth, and onboarding screens.
