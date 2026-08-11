# The Biggest Wiener

A punishment cookbook. Devaraiders Fantasy Football, 2025 season.
Eight courses, one protein, every dish gluten-free.

Hosted on GitHub Pages from `main`.

## Pages

| File | What it is |
|---|---|
| `index.html` | Cover / landing page. Clean — no league content. |
| `menu.html` | Full menu: all eight dishes, names and pictures only. |
| `menu1.html` … `menu8.html` | Cumulative menu. `menu3` shows the first three dishes. Cards link to the matching recipe. |
| `day1.html` … `day8.html` | Cumulative recipes. `day3` contains Courses I–III in full. |
| `404.html` | Styled not-found page. |
| `daily.css` | Shared stylesheet for every page above. Edit once, restyles all. |

There is also a full private edition of the book — the original paginated
flip-through, with the roast intro and the per-course commentary intact. It
is served from an unlisted filename and is deliberately not linked from
anywhere on the site.

## Daily release

One link per day, in order:

```
day1.html   Course I      day5.html   Courses I–V
day2.html   Courses I–II  day6.html   Courses I–VI
day3.html   Courses I–III day7.html   Courses I–VII
day4.html   Courses I–IV  day8.html   Courses I–VIII
```

`day1.html` is the only public page carrying the roast intro — it is the
reveal. Days 2–8 are recipes only.

## Privacy

- `robots.txt` disallows all crawlers; every page also carries
  `<meta name="robots" content="noindex, nofollow">`.
- The repo is public, so anyone with a URL can read these pages. The
  protection here is against search-engine discovery, not against someone
  who has the link.
- Earlier commits still contain the roast intro on all eight day pages.
  Removing that would require rewriting history.

## Editing

Recipes are duplicated across the cumulative day pages by design — a change
to Course II has to land in `day2.html` through `day8.html`. Menu cards are
duplicated the same way across `menu*.html`.

Images are Unsplash URLs in the form:

```html
<img src="https://images.unsplash.com/photo-XXXXX?w=800&q=80" alt="...">
```

Each dish's photo appears in its day pages, its menu cards, and the private
edition — update all of them together.

## Style

Dark ground `#0A0A0A`, gold `#B8965A`, bone `#F2EDE4`. Playfair Display for
display type, Cormorant Garamond for body, Courier Prime for labels.
