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

Orientation: an earlier rotation pass turned most of the library the wrong way,
so ~38 of the 46 files sat on their side on the live site. All 46 have now been
rotated to render upright **in Chrome** and re-verified there.

Do not trust `sips`, the Read tool, or ffmpeg's default decode on these files —
they disagree with each other, because a handful carry an EXIF orientation tag
the others don't. The only reliable check is to render `assets/*.jpg` in a real
browser and look. To fix one, go via PNG so no metadata survives to flip the
rotation back:

    ffmpeg -noautorotate -i in.jpg -map_metadata -1 tmp.png
    ffmpeg -i tmp.png -vf transpose=2 -map_metadata -1 -q:v 2 out.jpg

(`transpose=2` is 90° counter-clockwise, `transpose=1` clockwise.) Check any
newly added photo the same way.

Two naming traps in `assets/`: `charcoal-portrait-study.jpg` is a photo of a
Ganesh statue (a duplicate of `reel-portrait.jpg`) — the actual charcoal
portrait is `bts-4.jpg`; and `shivani-spiritual-painting.jpg` and
`reel-spiritual.jpg` are the same photograph under two names.

Two subjects have no real photo yet and are shown as labelled "Image to
supply" slots rather than a mismatched stand-in: **pet portraits** and
**abstract art**. These appear in the "What I Paint" section on the homepage,
in the Gallery/Collections pet and abstract sections, and in the Live
Weddings "Which Wedding Moment" grid (Your Pets) — swap for real photos once
the client supplies them.

The "A Few Pieces From My World" section on the homepage is a scroll-driven
3D fold reveal, rebuilt in Sep 2026 to match a reference recording the client
supplied. The cards stand upright across the middle band of the viewport and
lie flat away from the viewer at either end — they do not fold in on entry and
latch flat, which is what the earlier version did and what the client called
"very subtle".

Measured off the reference and implemented in `updateCaseStudyStage()`:
`perspective: 2600px` on the wrapper (roughly 4x the card height — a much
flatter perspective than the old 1000px, which is what lets a ~54° rotation
read as a fold rather than a warp), `transform-origin: center`, `rotateX` 0 →
54°, `scale` 1 → 0.81, plus a `[data-cs-dim]` ink overlay 0 → 0.52. Progress is
each card's own position in the viewport, eased `t²`, and the bands are
deliberately asymmetric: a card holds upright much longer coming in from the
bottom than it does going out the top.

Cards are `aspect-ratio: 1/1` — a compromise. The reference's cards are 2:1
landscape, but these photos are 3:4 portrait and a landscape card cropped the
faces and canvases out of frame. Square keeps the subject and still leaves the
fold room to read.

Vanilla JS/CSS throughout (no React/Framer Motion; the site has no build
pipeline).

Gallery and Collections cover overlapping categories but serve different
jobs, kept intentionally distinct rather than merged: Collections is the
commission pitch (short copy, FAQs, 1-2 images per category, strong CTA per
category — plus 3 categories Gallery doesn't cover: events, hospitality,
weddings-as-a-service). Gallery is the visual portfolio (bigger grids, more
images per category, "Behind the Scenes" process shots). Each links to the
other ("Want to Commission Your Own? See Collections" on Gallery; "Explore My
Work" on Collections).

The homepage "What Clients Say" section is a rotating testimonial carousel
(7 quotes, 6.5s auto-advance, click-to-jump dots, pauses on hover and focus,
static under `prefers-reduced-motion`). The quotes are **real, publicly posted
reviews republished from the client's WedMeGood profile**, attributed by name,
with the source credited in the section ("5.0 from 20 reviews on WedMeGood").
Three further reviews exist but were left out because only truncated text was
available — do not reconstruct them. Confirm with the client that they are
happy to republish reviewer names before this goes live.

Blog/Enquire content is still placeholder (bracketed `[ ]` text) — client to
supply real copy and post content. The `Kind Words.dc.html` page still has its
"[Couple Names]" placeholder slots.

## Shared rules

- Copy is the client's own, verbatim from `content.md`.
- Images live in `assets/`; each is used once per page — no repeats of the
  same photo, and no reuse of a similar-looking photo in a nearby section.
- Responsive down to ~360px, honours `prefers-reduced-motion`, body text
  15px or above.
