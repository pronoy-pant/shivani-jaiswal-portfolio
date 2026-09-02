# Shivani Jaiswal — Site

Single homepage direction, chosen and built out: **Midnight Reel**
(`index.html`). Earlier comparison directions (1a, 1c,
2a/b/c/e, 3a/b/c, Direction Studies) were discarded once this one was picked.

## Midnight Reel — full site

One page per client content doc, all sharing the same palette / type / header
/ footer:

| Page | File | Source doc |
| --- | --- | --- |
| Home | `index.html` | 1. Home Page |
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
3D fold, rebuilt in Sep 2026 against the client's reference site
(impactfloww.framer.website). The numbers are not eyeballed — they were read
out of that site's own compiled `__framer__transformTargets` config:

| | desktop (>=810px) | mobile (<810px) |
| --- | --- | --- |
| before its turn | `rotateX(-50deg) scale(0.8)` | `rotateX(-30deg) scale(0.9)` |
| at its turn | `rotateX(0) scale(1)` | `rotateX(0) scale(1)` |
| after its turn | `rotateX(+50deg) scale(0.8)` | `rotateX(+30deg) scale(0.9)` |

`perspective(2000px)` sits in the card's own transform string (not on a
wrapper), opacity stays 1 throughout (the reference has no dimming overlay —
the old `[data-cs-dim]` layer is gone), and the cards sit in a plain column
flex with a **20px** gap. Progress is linear in `d`, the card's distance from
the viewport centre measured in card pitches (height + gap), clamped to
[-1, 1]; `rotateX = -MAX * d`. The sign matters: a card leans *back towards*
the viewer on the way in and away from it on the way out. The previous build
folded the same way at both ends, which is what the client kept rejecting.

Cards are `aspect-ratio: 3/2` — a compromise. The reference's cards are 2:1,
but these photos are 3:4 portrait and 2:1 cropped the canvases out of frame
(checked by screenshot). 3:2 keeps the artwork and still reads as a fold.

Every page's logo and footer "Home" link used to point at
`Homepage 2d Midnight Reel.dc.html`, a stale duplicate of the homepage that
still carried the old animation. That file is deleted; everything now links to
`index.html`.

**Filename duplicates:** 12 groups of `assets/*.jpg` are byte-identical under
different names, so a filename-only uniqueness check misses real repeats. The
library holds 46 files but only **31 distinct photographs**. Check per page by
content hash, not by name:

    python3 -c "import re,hashlib,glob,collections,sys; H={f:hashlib.md5(open(f,'rb').read()).hexdigest() for f in glob.glob('assets/*.jpg')}; s=re.findall(r'src=\"(assets/[^\"]+\.jpg)\"',open(sys.argv[1]).read()); c=collections.Counter(H[x] for x in s); print([[x for x in s if H[x]==h] for h,n in c.items() if n>1])" <page>

All pages are clean of same-photo repeats as of this pass.

**Copy is verbatim, and placeholders are deliberately visible.** Every page was
diffed against `content/*.md` in both directions and the invented editorial
layer removed: fold-card titles and captions, section eyebrows ("Intent", "The
artist", "On the day", "Why a painting", "The reveal", "Travel", the numbered
"01 -" Collections labels), and the invented Gallery/Live Weddings figure
captions. Headings reverted to the docs' own wording ("Made to Mean
Something", "Live Painting, While the Moment Is Still Happening", "From My
Easel", "Kind Words"). The docs' bracketed `[ Add ... ]` markers now render on
the page on purpose, so the client can see what she still owes.

The homepage testimonial carousel keeps the 7 real WedMeGood quotes (see
below) rather than the doc's two empty placeholder slots — the client chose
this explicitly. It now carries the doc's heading ("Kind Words"), the doc's
CTA ("Read More Stories"), a "Read Original Review" link per quote, and a
4.2s advance (was 6.5s, which the client found too slow).

Pages other than Home and Live Weddings used to open on a text-only block.
They all now lead with a full-bleed image hero on the Live Weddings pattern
(`min-height:82vh`, image + a 105deg ink wash under a 180deg one, then the
page's own copy unchanged).

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

The homepage "Kind Words" section is a rotating testimonial carousel
(7 quotes, 4.2s auto-advance, click-to-jump dots, pauses on hover and focus,
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
