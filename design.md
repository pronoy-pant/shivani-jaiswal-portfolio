# Shivani Jaiswal — Site

Single homepage direction, chosen and built out: **Midnight Reel**
(`Homepage 2d Midnight Reel.dc.html`). Earlier comparison directions (1a, 1c,
2a/b/c/e, 3a/b/c, Direction Studies) were discarded once this one was picked.

## Midnight Reel — full site

One page per client content doc, all sharing the same palette / type / header
/ footer:

| Page | File | Source doc |
| --- | --- | --- |
| Home | `Homepage 2d Midnight Reel.dc.html` | 1. Home Page |
| About + Meet Our Team | `About.dc.html` | 2. About Page, Meet Our Team |
| Collections | `Collections.dc.html` | 3. Collections |
| Live Wedding Painting | `Live Wedding Painting.dc.html` | 4. Live wedding painting page |
| Gallery | `Gallery.dc.html` | 5. Gallery Page |
| Kind Words | `Kind Words.dc.html` | 6. Testimonials |
| Journal | `Blog.dc.html` + `BlogPost.dc.html` | 7. Blog Page |
| Enquire | `Enquire.dc.html` | 8. Contact me |

Palette: ink `#120E1A`, panel `#1B1526`, gold `#E0B25C`, warm white `#F3EDE4`.
Type: Cormorant Garamond (serif display) + Jost (UI/body).

Nav: Collections · Live Weddings · Gallery · About · Journal · Enquire.
Kind Words and Meet the Team sit in the footer / About page.

Copy is verbatim from the docs. Client-action items are left in the page as
bracketed `[CLIENT: …]` lines (international shipping, travel & stay, final
email address) and `[ ]` placeholders where real testimonials, couple names,
and captions are still needed.

## Imagery

Real photos supplied by the client (Drive folders, Aug–Sep 2026) replaced the
placeholder assets throughout, plus a second curation pass pulling ~16 more
images from "Shivani Drive pictures 2" (event folders + the Shivani
Artwork/artwork folders) to de-densify the Live Weddings page and give
Gallery/Collections/Home distinct, non-repeating imagery. Every image used
shows an actual painting (finished canvas, work-in-progress, or a painting
alongside real clients) — plain event/venue photos with no artwork visible
are not used.

Note: most of the client's raw phone photos ship with no EXIF orientation
tag, so a large batch (~35 files across the original and second imports)
needed a manual 90° rotation fix. If more images are added from the same
Drive folders later, check orientation before use — `sips -g orientation`
returns nothing useful; visually inspect instead.

Two subjects have no real photo yet and are shown as labelled "Image to
supply" slots rather than a mismatched stand-in: **pet portraits** and
**abstract art**. These appear in the "What I Paint" section on the homepage,
in the Gallery/Collections pet and abstract sections, and in the Live
Weddings "Which Wedding Moment" grid (Your Pets) — swap for real photos once
the client supplies them.

The "A Few Pieces From My World" section on the homepage is a scroll-driven
3D fold-flat card reveal: 4 cards (trimmed from an earlier 6), category pill
top-left, `rotateX` driven directly by each card's own scroll progress via
`updateCaseStudyStage()` (no fixed-duration animation), flattening and
staying flat as it passes the upper third of the viewport. See the
component's script in `Homepage 2d Midnight Reel.dc.html` for the effect —
it's vanilla JS/CSS (no React/Framer Motion dependency; the site has no
build pipeline), chosen deliberately over a rewrite since the existing
implementation already satisfied the brief.

Gallery and Collections cover overlapping categories but serve different
jobs, kept intentionally distinct rather than merged: Collections is the
commission pitch (short copy, FAQs, 1-2 images per category, strong CTA per
category — plus 3 categories Gallery doesn't cover: events, hospitality,
weddings-as-a-service). Gallery is the visual portfolio (bigger grids, more
images per category, "Behind the Scenes" process shots). Each links to the
other ("Want to Commission Your Own? See Collections" on Gallery; "Explore My
Work" on Collections).

Blog/Enquire content is placeholder (bracketed `[ ]` text) — client to supply
real copy and post content. Kind Words' "[Couple Names]" testimonial slots
are also placeholder, left as-is — they need real, specific client quotes
and photos rather than a generic stand-in.

## Shared rules

- Copy is the client's own, verbatim from `content.md`.
- Images live in `assets/`; each is used once per page — no repeats of the
  same photo, and no reuse of a similar-looking photo in a nearby section.
- Responsive down to ~360px, honours `prefers-reduced-motion`, body text
  15px or above.
