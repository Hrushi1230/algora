# Batch 11 — The Growth Layer: shareable state, embeds, SEO, OG cards

**Goal:** turn the product into something Google can index and students can forward. This batch
implements the five sharing mechanics and the programmatic-SEO surface described in `GROWTH.md`.

**Prerequisites:** batch 03 (engine), batch 04 (visualizer workspace), batch 05 (catalog +
`src/data/algorithms.ts` fully populated). Batches 6–10 are **not** required.

---

## Read this before you start: when to run this batch

The numbering says 11, but **run it immediately after batch 05 if you want traffic this
semester.** Batches 6–9 (lessons, practice, gamification, roadmap) make people *stay*; this batch
is the only one that makes people *arrive*. A retention feature with no traffic retains nobody.

Recommended real order: `01 → 02 → 03 → 04 → 05 → 11 → 06 → 07 → 08 → 09 → 10`.

## The technical fact that dictates prompt order

Your stack is a **Vite SPA**. The HTML sent to a crawler or to Discord's link unfurler is:

```html
<div id="root"></div>
```

No title, no description, no content. Consequences, all of which are fatal to §3 of `GROWTH.md`:

- `react-helmet` sets tags **after** JS runs. Google *sometimes* renders JS; Discord, WhatsApp,
  Slack, X, iMessage and LinkedIn **never** do. Your OG cards would simply not exist.
- 60 algorithm pages would be 60 identical empty documents to a crawler.

So **prompt 11.1 (prerendering) must land before any meta-tag or OG work.** Do not reorder this
batch. If Lovable proposes `react-helmet` alone as the SEO solution, that is the failure mode in
the table at the bottom — reject it.

---

## Prompt 11.1 — Static prerendering (do this first)

[PASTE SHARED CONTEXT]

```
Convert the app from a pure client-rendered Vite SPA to a build-time prerendered static site
using `vite-react-ssg`, WITHOUT changing any component's runtime behaviour.

1. Install `vite-react-ssg`. Convert `src/app/router.tsx` to export a plain route array
   (`RouteRecord[]`) instead of calling createBrowserRouter directly, and change the entry point
   to `ViteReactSSG(...)` as that library requires. Keep every existing route path identical.
2. Provide `getStaticPaths` for the dynamic routes that must be indexed:
   `/algorithms/:slug` (from listModules() ∩ src/data/algorithms.ts), `/paths/:slug`,
   `/blog/:slug`, `/help/:slug`. Do NOT prerender authenticated routes
   (/app, /explore, /review, /practice/**, /mastery, /quests, /leaderboard, /achievements,
   /streak, /progress, /settings, /billing, /notifications, /u/**, /onboarding/**, /roadmap/**,
   /admin/**, /dev/**) — those stay client-only and must be excluded from the build manifest.
3. Anything that touches window/localStorage/matchMedia at module scope or during first render
   will crash the SSG build. Guard it: move to useEffect, or `typeof window !== 'undefined'`.
   The zustand stores must construct fine in Node with default state.
4. Playback must NOT auto-start during prerender: the static HTML for an algorithm page must
   contain the fully-rendered step 0 (real SVG markup, real narration text, real complexity
   table) and nothing time-dependent. The animation begins only after hydration, on user action.
5. Add `pnpm build:ssg` and make it the deploy build. Fix hydration mismatches until the console
   is clean — no "text content did not match" warnings.

Acceptance: `curl` on the built `/algorithms/bfs/index.html` shows the algorithm's real title,
description and step-0 SVG in the raw HTML, with JS disabled.
Change only routing/entry/config files and the specific files that break the SSG build.
```

---

## Prompt 11.2 — Per-route metadata, canonical, JSON-LD, sitemap, robots

[PASTE SHARED CONTEXT]

```
Now that pages are prerendered, give every indexable route real metadata.

1. Create `src/lib/seo.ts` exporting `buildMeta({ title, description, path, image, type })`
   returning a typed meta descriptor. Title format: "<Specific thing> — Algora"
   (max 60 chars), description 140-160 chars, written for a human, never keyword-stuffed.
2. Create `src/components/common/Seo.tsx` using vite-react-ssg's `Head` component (NOT
   react-helmet) so the tags end up in the prerendered HTML. It renders: title, description,
   canonical link, og:title/og:description/og:image/og:url/og:type/og:site_name,
   twitter:card=summary_large_image, and optional JSON-LD.
3. Add <Seo> to every prerendered page. For `/algorithms/:slug`, drive the copy from
   src/data/algorithms.ts, targeting the real search intent from GROWTH.md Trigger A:
   title "Dijkstra's Algorithm — Interactive Step-by-Step Visualization | Algora"
   description "Watch Dijkstra's shortest-path algorithm run step by step on your own graph.
   Scrub forwards and backwards, see the distance table update, with code in Python, JS and TS."
4. JSON-LD per page type: algorithm pages get `LearningResource` (+ `FAQPage` when the page has
   the FAQ block from prompt 11.6), blog posts get `Article`, help articles get `TechArticle`,
   `/` gets `Organization` + `WebSite` with SearchAction. Emit valid schema.org only — no
   invented fields, no fake `aggregateRating` or `review` (that is a manual-action risk).
5. Generate `dist/sitemap.xml` at build time from the same route+slug source used by
   getStaticPaths — never a hand-maintained list. Include only indexable routes, with lastmod.
   Add `public/robots.txt`: allow all, disallow /admin, /dev, /embed, reference the sitemap.
6. Add `<link rel="alternate" type="application/rss+xml">` and generate `dist/rss.xml` for /blog.

No visual changes in this prompt. Do not modify src/engine/**.
```

---

## Prompt 11.3 — Shareable state URLs (the highest-value mechanic)

[PASTE SHARED CONTEXT]

```
Make the URL the single source of truth for what the visualizer is showing, so a student can send
a friend the exact frame they are stuck on (GROWTH.md §4.1).

1. Create `src/lib/urlState.ts`:
   - `encodeState(rawInputs, step)` -> URLSearchParams. Short readable keys for the common case:
     ?input=5,3,8,1&target=8&step=12. Only include params that differ from the module defaults.
   - If the serialized query would exceed 500 chars (big graphs/grids), fall back to a single
     `?s=<base64url of compact JSON>` param instead.
   - `decodeState(params, module)` -> { rawInputs, step } and it MUST run module.validate() and
     clamp step into [0, steps.length-1]. Never trust the URL: malformed or hostile params fall
     back to the module's first preset plus a dismissible "that link looked broken, showing the
     default example" notice. No crash, no blank screen, no thrown error.
2. In the algorithm workspace: on mount, hydrate the player from the URL. When the user changes
   input or presses Run, `navigate(..., { replace: true })` with the new query.
3. Do NOT write the step index to the URL on every animation frame — that would flood browser
   history and tank performance. Write it (replace, debounced ~400ms) only when the user
   pauses, scrubs, or steps manually.
4. Back/forward must work: a popstate restores that input+step exactly.
5. Make sure the prerendered page ignores query params (static HTML is always the default
   preset at step 0) and hydration then applies the URL state.

Test: load /algorithms/quicksort?input=9,4,7,1,8&step=6 in a fresh tab — it must show that
input paused precisely at step 6.
```

---

## Prompt 11.4 — Share sheet: copy link, frame PNG, embed code

[PASTE SHARED CONTEXT]

```
Build `src/components/player/ShareSheet.tsx`, opened by a Share button in the visualizer toolbar
(lucide `share-2`, 20px). Use the existing shadcn Dialog/Popover and existing tokens.

Four actions, each one row with icon + label + hint:
1. "Copy link" — current URL from urlState (input only, step stripped).
2. "Copy link to this step" — includes &step=<i>, hint "opens paused at step 12 of 34".
3. "Download this frame (PNG)" — serialize the visualizer <svg>, draw to an offscreen canvas at
   2x, add a small "algora" wordmark + the algorithm name in the corner, export via toBlob.
   Must inline computed styles so the PNG is not unstyled; set crossOrigin='anonymous' on any
   image drawn to canvas.
4. "Copy embed code" — <iframe src="https://<origin>/embed/<slug>?<state>" width="100%"
   height="520" style="border:1px solid #E4E9E7;border-radius:16px" loading="lazy"
   title="..."></iframe>, shown in a read-only <pre> with a copy button.

Use navigator.clipboard with a document.execCommand fallback; show an inline "Copied" state on
the row for 2s (no toast spam). Full keyboard support, focus trap, Esc closes, aria-live
announcement of the copy result. Nothing about social networks — no Facebook/Twitter buttons.
```

---

## Prompt 11.5 — Embed mode for teachers and bloggers

[PASTE SHARED CONTEXT]

```
Add a public, chrome-free embed route `/embed/:slug` (GROWTH.md §4.3) reusing the EXISTING
renderers and playerStore. Do not duplicate visualization logic.

Layout: the visualization + a compact playback bar + the narration line. No global nav, no
sidebar, no footer, no auth check, no signup prompt. One small "Powered by Algora" link in the
bottom-right, target=_blank, pointing at /algorithms/:slug with ?utm_source=embed — that
backlink is the entire business reason embeds exist.

Requirements:
- Reads the same urlState params as the full page.
- Must be responsive down to 320px and look correct at heights 400-720px.
- Never autoplay on load (respect prefers-reduced-motion and iframe etiquette).
- Post its content height to the parent via postMessage
  ({ type:'algora:height', height }) on mount and resize, so hosts can auto-size.
- Add `noindex` on this route (canonical points to the full page) so embeds never compete with
  the real page in search results.
- Exclude /embed/** from the SSG prerender manifest? NO — prerender it too, so it loads fast
  inside slow course pages, but keep the noindex meta.
```

---

## Prompt 11.6 — The SEO body content on algorithm pages

[PASTE SHARED CONTEXT]

```
An algorithm page currently has a visualizer and little text. Google needs substance and the
panicking student needs answers. Extend `src/data/algorithms.ts` with a content field per
algorithm and render it BELOW the interactive workspace as prose sections:

- `summary`: 2-3 sentences answering "what is this and when would I use it".
- `intuition`: the one analogy that makes it click, 3-4 sentences.
- `complexity`: { best, average, worst, space } + a one-line "why" for each — render as a real
  <table> with JetBrains Mono figures.
- `dryRun`: a short worked example in prose, with a "watch this run" button that loads exactly
  that input into the player above (reuse urlState).
- `mistakes`: 3-5 "common mistakes" bullets (e.g. "using Dijkstra with negative weights").
- `faq`: 4-6 Q&A pairs written from real search queries ("is BFS or DFS better for shortest
  path?"). Feed these into the FAQPage JSON-LD from prompt 11.2.
- `relatedProblems`: links into /practice/:slug; `relatedAlgorithms`: 3 cards.

Rendering rules: one <h1> per page (the algorithm name), then <h2> per section in a semantic
<article>; a sticky in-page table of contents on lg+ screens; prose max-width ~68ch;
`text-pretty` on headings. Content must be real and technically correct — no lorem ipsum, no
"Coming soon". Write it for the first 12 algorithms in this prompt.
```

---

## Prompt 11.7 — The funnel metric that decides everything else

[PASTE SHARED CONTEXT]

```
Instrument the one number from GROWTH.md §6: the share of visitors who press play.

1. Create `src/lib/analytics.ts` with a typed `track(event, props?)` and a union of allowed
   events ONLY: 'page_view' | 'algo_view' | 'play_pressed' | 'step_manual' | 'input_changed' |
   'run_completed' | 'share_opened' | 'share_copied' | 'embed_copied' | 'signup_prompt_shown' |
   'signup_prompt_accepted'. Unknown event strings must fail type-check.
2. Back it with a cookieless, privacy-friendly provider (Plausible or Umami) loaded via a
   deferred script, and a no-op when the env var is absent so dev/preview send nothing.
   No Google Analytics, no Facebook pixel, no session recording. Never send user input contents,
   emails, or handles — event props are limited to slug, step count, and enum-ish strings.
3. Fire the events at their true moments; 'run_completed' means the user actually reached the
   final step, not that the page loaded.
4. Add a dev-only overlay on /dev/engine listing the events fired this session so you can verify
   without opening the provider dashboard.
```

---

## Prompt 11.8 — The earned conversion prompt

[PASTE SHARED CONTEXT]

```
Add the soft, earned signup prompt from GROWTH.md §5. This is the ONLY signup interruption
allowed on a public algorithm page, and it must never block the visualizer.

Trigger: the user has reached the last step of a run AND has viewed >= 2 algorithms this session
(track in sessionStorage). Then, and only then, slide in a dismissible card BELOW the player:
  title "Want the rest of the graph track?"
  body "Save your progress and get a 30-day plan built around what you just watched."
  primary "Create free account" -> /signup   secondary "Not now" -> dismiss.

Rules: appears at most once per session; "Not now" suppresses it for 7 days (localStorage);
never a modal, never an overlay, never blocks scrolling, never appears before a completed run,
and it is absent entirely in /embed/**. Fire 'signup_prompt_shown' / 'signup_prompt_accepted'.
Respect prefers-reduced-motion (fade, no slide).
```

---

## Acceptance checklist — Batch 11

- [ ] With JavaScript disabled, `/algorithms/bfs` shows a real title, description, prose and a
      step-0 SVG in the page source.
- [ ] Pasting an algorithm link into Discord/WhatsApp/Slack unfurls with a correct OG image and title.
- [ ] `/algorithms/quicksort?input=9,4,7,1,8&step=6` opens paused at exactly that frame.
- [ ] A hostile/garbage query string shows the default example with a notice — never a crash.
- [ ] `dist/sitemap.xml` contains every algorithm page and zero authenticated routes.
- [ ] `/embed/bfs` works inside a third-party `<iframe>`, is `noindex`, and links back with utm.
- [ ] Frame PNG downloads fully styled, with the wordmark.
- [ ] Rich Results Test passes for `LearningResource` + `FAQPage` on an algorithm page.
- [ ] Lighthouse SEO 100, accessibility 100 on `/algorithms/bfs`.
- [ ] Zero hydration mismatch warnings in the console on any prerendered route.
- [ ] No analytics event carries user-typed content.

## Failure modes & repair prompts

| Symptom | Repair prompt |
|---|---|
| Lovable adds `react-helmet` and calls SEO done | `react-helmet only runs after JS. Social crawlers never execute JS, so og:image would not exist. Use vite-react-ssg's Head so tags are emitted into the prerendered HTML, and prove it with curl on the built file.` |
| SSG build crashes on `window`/`localStorage` | `This runs during Node prerender. Guard with typeof window !== 'undefined' or move it into useEffect. Do not disable prerendering for the route.` |
| Hydration mismatch on algorithm pages | `The server rendered a different step than the client. Prerender must always render step 0 of the default preset; URL state may only be applied after hydration inside an effect.` |
| Step index spams browser history | `Use navigate(..., { replace: true }) and debounce ~400ms. Only write the step on pause/scrub/manual step, never per animation frame.` |
| OG images generated at request time | `This is a static host — there is no server. Generate the PNGs at build time into dist/og/<slug>.png and reference them as static files.` |
| Embed shows the app nav or a signup card | `/embed/** must render only visualization + controls + narration + the powered-by link. No shell, no auth, no prompts.` |
| Thin algorithm pages ("Coming soon") | `Write real technical content for these sections. A page with a widget and no prose will not rank for the query it targets.` |
| Fake ratings in JSON-LD | `Remove aggregateRating/review. Emit only schema.org fields backed by real on-page content.` |

---

## What this batch does NOT do

Deliberately out of scope, so the batch stays shippable: achievement cards (batch 08, they need
XP data), study-group invites and shared roadmaps (batch 09 + backend), and the build-time OG
image generation script — that one lives in **batch 10, prompt "OG images"**. If you run batch 11
before batch 10, pull that single prompt forward, because prompt 11.4's link-sharing is
half-useless without it.
