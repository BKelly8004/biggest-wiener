# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static HTML site: a "punishment cookbook" for the Devaraiders fantasy football league, 2025 season. Eight courses, one protein (hot dogs), every dish gluten-free. There is no build system, no package manager, and no tests — every page is hand-authored HTML sharing one stylesheet (`daily.css`). It's hosted on GitHub Pages from `main`.

## Working with this repo

There are no build/lint/test commands — edit the `.html`/`.css` files directly and open them in a browser (or use a local static server, e.g. `python3 -m http.server`) to preview. Pushing to `main` deploys via GitHub Pages.

## Site structure

| File | What it is |
|---|---|
| `index.html` | Cover / landing page. Clean — no league content. |
| `menu.html` | Full menu: all eight dishes, names and pictures only. |
| `menu1.html` … `menu8.html` | Cumulative menu. `menu3` shows the first three dishes. Cards link to the matching recipe anchor (e.g. `day3.html#course-2`). |
| `day1.html` … `day8.html` | Cumulative recipes. `day3` contains Courses I–III in full. |
| `404.html` | Styled not-found page. |
| `daily.css` | Shared stylesheet for every page above. Edit once, restyles all pages. |
| `the-full-book-*.html` | Private, unlisted full edition (paginated flip-through with roast intro and per-course commentary). Deliberately not linked from anywhere on the site — do not link to it. |

### Critical convention: content is duplicated by design, not templated

There is no templating engine. Each `dayN.html` is **cumulative** — it contains the full markup for Courses I through N, copy-pasted from the previous day's page. Likewise each `menuN.html` cumulatively repeats menu cards I through N. This means:

- A change to Course II's recipe (ingredients, steps, name, image) must be applied to **every** page that contains it: `day2.html` through `day8.html`.
- A change to a menu card must be applied across `menu2.html` through `menu8.html` (and `menu.html`, which shows all eight).
- Each dish's photo (an Unsplash URL) appears in its day pages, its menu cards, `og:image` meta tags, and the private full-book edition — update all of them together.
- When editing recipe content, grep across all `day*.html`/`menu*.html` files for the course name/number to find every copy that needs the same change.

### Per-page anatomy (day pages)

Each `dayN.html` follows the same skeleton:
- `<head>`: standard meta + Open Graph tags (`og:title`, `og:description`, `og:image`, `og:url`) that must be kept in sync with the page's actual content/day number, plus `<meta name="robots" content="noindex, nofollow">` (see Privacy below).
- `.bar` header with left/center/right labels (site name, league/season, "Day N of 8").
- `.intro` section — full cookbook intro/roast copy, present **only** on `day1.html` (the reveal). Days 2–8 omit it and go straight to the menu head.
- One `<article class="course" id="course-N">` per released course, each with `.course-media` (image), `.course-head` (label/title/subtitle), `.meta-strip` (Protein/Method/Vessel/Time), and `.course-cols` (Ingredients list + numbered Preparation steps).
- `.pagenav` linking back to the previous day and forward to that day's cumulative menu.
- `.foot` footer restating day number and course range.

Menu pages (`menuN.html`) follow a parallel but simpler skeleton: `.bar` header, `.menu-hero`, a `.menu-grid` of `.menu-card` figures (one per released course, each linking to `dayN.html#course-N`), `.pagenav`, `.foot`.

### Style system (`daily.css`)

CSS custom properties define the palette: dark ground `#0A0A0A`, gold `#B8965A`, bone `#F2EDE4`. Fonts: Playfair Display (display type), Cormorant Garamond (body), Courier Prime (labels), loaded via Google Fonts `<link>` in each page's `<head>`. Class names are consistent across all pages (`.sheet`, `.bar`, `.intro`, `.course`, `.meta-strip`, `.menu-grid`, `.menu-card`, `.foot`, etc.) — reuse existing classes rather than introducing new ones when adding content.

Images use `onerror="this.style.background='#1a1a18'"` as a fallback if the Unsplash URL fails to load — replicate this on any new `<img>`.

## Privacy model

- `robots.txt` disallows all crawlers; every page also carries `<meta name="robots" content="noindex, nofollow">`. Preserve this meta tag on any new page.
- The repo is public, so anyone with the URL can read these pages — the protection is against search-engine discovery only, not against someone who has a link.
- `day1.html` is the only public page carrying the full roast intro (it's the reveal); days 2–8 are recipes only. Do not add the roast intro to other public day pages.
- Earlier commits still contain the roast intro on all eight day pages; removing it would require rewriting git history — do not attempt this without being explicitly asked.
- The full-book edition is served from an unlisted filename and must stay unlinked from the public pages.
