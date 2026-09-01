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

Real photos supplied by the client (Drive folder, Aug–Sep 2026) replaced the
placeholder assets throughout. Every image used shows an actual painting
(finished canvas, work-in-progress, or a painting alongside real clients) —
plain event/venue photos with no artwork visible are not used.

Two subjects have no real photo yet and are shown as labelled "Image to
supply" slots rather than a mismatched stand-in: **pet portraits** and
**abstract art**. These appear in the "What I Paint" section on the homepage
and should be swapped for real photos once the client supplies them.

The "A Few Pieces From My World" section on the homepage is a scroll-driven
3D card reveal (perspective tilt + fade, tied to scroll position — see the
component's script for the effect). The Gallery page uses a simpler
case-study card treatment: full-bleed image in a rounded panel, pill category
tag + italic serif title over a bottom scrim.

Blog/Enquire content is placeholder (bracketed `[ ]` text) — client to supply
real copy and post content.

## Shared rules

- Copy is the client's own, verbatim from `content.md`.
- Images live in `assets/`; each is used once per page — no repeats of the
  same photo, and no reuse of a similar-looking photo in a nearby section.
- Responsive down to ~360px, honours `prefers-reduced-motion`, body text
  15px or above.
