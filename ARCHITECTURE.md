# Architecture

## System overview

One static HTML page, `index.html`, with its styles, script and images all inside it. GitHub Pages
serves it from the `main` branch, root folder (legacy build, HTTPS enforced), at
https://maxketamine-spec.github.io/identity-shift-hockey-mockup/. `.nojekyll` makes Pages serve
the file as it is. There is no server code, no build step and no package.

## Components

All of these live in `index.html`.

| Part | Where | What it does |
|---|---|---|
| Head | `<head>` | Title, viewport and theme-color meta, Google Fonts stylesheet |
| Styles | `<style>` | Design tokens on `:root`, then one block per section; phone layout at 640px; reduced-motion block |
| Nav | `header.nav` | Sticky bar with the brand mark, links and a "Work With Us" pill; a thin gold scroll-progress bar at the top of the window |
| Hero | `section.hero` | Headline over `canvas#rink`, a perspective hockey rink drawn in 2D canvas with drifting particles; follows the pointer |
| League strip | `#leagues` | League names, rendered twice by the script and scrolled as an endless marquee |
| Player rail | `#rail` | Ten player cards built from the `players` array: photo, level badge, "Started… / Result…" journey, quote with "Read more"; arrow buttons and dots on desktop, a stacked list on phones |
| Coaching offer | `section.offers` | One offer card with an SVG progress ring that fills when scrolled into view |
| Resources | `#resources` | Three tiles: masterclass, free training, email sign-up |
| Blog | `section.blog` | Three post cards; the art is drawn on `canvas[data-art]` at load, no image files |
| Coach | `#coach` | Portrait in a spinning SVG halo, social links, bio, a "limited spots" notice |
| Final call to action | `section.final` | Large headline and button |
| Footer | `footer` | Social links, tagline, second email sign-up, legal links, "Concept redesign · preview only" |
| Script | `<script>` at the end | One IIFE: the `IMG` map of base64 photos, the `players` data, rail controls, league strip, rink animation, blog art, scroll progress, reveal-on-scroll, offer ring, preview-only form handler |

## Data flow

1. The browser loads `index.html` from GitHub Pages, then the Google Fonts CSS and font files.
2. All content is hard-coded in the file. The script turns the `players` array and the league
   list into HTML and draws the canvases. No other network request is made.
3. The rink animation pauses when the hero is off screen or the tab is hidden, and draws fewer
   particles at a lower frame rate on phones. Under `prefers-reduced-motion` every animation and
   transition is off and the rink is drawn as a still frame.
4. A subscribe form submit is stopped in the browser and replaced with a preview note. Nothing
   leaves the page.
5. Every call-to-action and nav link leaves the mock-up for the live site or a social profile, in
   a new tab.

## Integrations

| Service | How it is used |
|---|---|
| GitHub Pages | Hosts the page from `main`, root folder |
| Google Fonts | Inter Tight, Inter, JetBrains Mono, Barlow Condensed |
| identityshifthockey.com and start.identityshifthockey.com | Outbound links only (work with us, blog, masterclass, log in, privacy, terms) |
| YouTube, Instagram, Twitter, TikTok | Outbound profile links only |

No APIs, no analytics, no form backend.

## Tech stack

| Layer | Choice |
|---|---|
| Markup | HTML5, one file |
| Styling | Hand-written CSS with custom properties; no framework |
| Script | Plain JavaScript (ES2015+), no libraries |
| Graphics | 2D canvas (rink, blog art), inline SVG (icons, rings, halo) |
| Images | JPEG and PNG inlined as base64 `data:` URIs (16 in all) |
| Fonts | Google Fonts |
| Hosting | GitHub Pages, legacy build from `main` |
| Build, tests, packages | None |

## Decision Log

Newest last. Only decisions with evidence are listed.

| Date | Decision | Why | Alternatives considered |
|---|---|---|---|
| 2026-11-15 | One self-contained `index.html` with every image inlined as base64; no build step (commit 9252a9b) | TBD – confirm. Effect: the page is one file with no asset folder to host or lose | TBD – confirm |
| 2026-11-15 | Keep the live site's page order and rebuild the look as a "night rink": full-bleed bands, one 1160px column, a perspective ice surface behind the hero, player cards on a snap rail, gold from the brand mark on every call to action (layout comment at the top of the CSS) | TBD – confirm | TBD – confirm |
| 2026-11-15 | The email forms stay preview-only and send nothing (script, "subscribe (preview only)") | The page is a concept preview; the note says sign-up connects when the site goes live | TBD – confirm |
| 2026-11-15 | Host on GitHub Pages from `main`, root folder, with `.nojekyll` (commit 9252a9b, Pages settings) | TBD – confirm | TBD – confirm |
| 2026-11-15 | The repository stays public, on purpose (Max's project notes) | GitHub Pages on the account's current plan needs a public repository | Move the page to another static host and make the repository private |
| 2026-11-16 | One root AGENTS.md as the only rulebook; CLAUDE.md is the single line `@AGENTS.md`; SECURITY.md, ARCHITECTURE.md and DESIGN_SYSTEM.md added (Max's agent docs standard) | One rulebook for every coding tool, and docs that change with the code | A full CLAUDE.md beside AGENTS.md (two rulebooks drift apart) |
