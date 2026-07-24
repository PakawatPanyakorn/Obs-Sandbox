# masonry-photo-essay

**Archetype:** masonry-photo-essay · **Family:** editorial-narrative

## Core Concept
Variable-height image blocks with cutline captions, sized once per image from its real aspect ratio and narrative weight — a wide panorama is wide because it IS wide, not because it's the most important thing on the page. Distinct from `bento-mosaic`, whose sizing signal is importance/data hierarchy: here it's literal image shape. The tell that spans are image-driven, not decorative: swapping two exhibits' images without re-deriving their spans looks wrong immediately.

## When To Use
- Long-form narrative essays with photography, travel writing, memoir-with-images — content where prose carries roughly half the page's weight alongside real photographs.
- Visual research reports, cartographic essays, data-journalism pieces built around maps/diagrams with a narrative throughline (sizing shifts to "this figure needs the width," not "this matters more").
- Visual portfolios or case-study indexes where every item genuinely has its own real image at its own real aspect ratio — actual different-shaped work, not stock thumbnails forced square.

## When NOT To Use
- Feature/pricing/spec comparison lists of equal-weight items — that's a uniform card grid's job; forcing comparable items into varying-aspect exhibit blocks implies a false narrative-weight difference between things that are actually equal.
- Content where the real sizing signal is "this finding matters more" rather than "this figure is shaped this way" — that's `bento-mosaic`'s job; don't relabel a bento-mosaic as a photo essay just because the boxes happen to be different sizes.
- Markdown as the primary target — flag this to the author rather than silently degrading; standard markdown renderers erase the entire size-hierarchy signal this archetype depends on.

## Region / Component Guidance
- **essay-head** (`1 / 9`): title + narrative opener, quiet and text-only on purpose. It is *not* the entry point — the first exhibit is.
- **exhibit-hero** (`1 / 13`): the opening exhibit, sized from its own image's real proportions (could be wide, could be tall/narrow — whatever the image actually is). Gets the archetype's only shadow-hero/gradient-hero treatment, echoing `magazine-well`'s single-hero restraint rule.
- **exhibit-\*** (`3-12`, varies per instance, repeated): each independently sized to its own image's real aspect ratio and narrative beat, never a shared formula. Row height varies genuinely via grid-row span, never a padding-percentage trick.
- **exhibit-quote-break** (`1 / 13`, mid-sequence): a text-only interstitial pausing the image sequence for editorial commentary — occupies a masonry slot like any exhibit but carries no image.
- **essay-close** (`1 / 9`, last): closing passage returning to prose after the visual sequence ends.

## Content-Type Notes
- **textHeavy**: exhibits thin out — most blocks become genuinely text-only, promoted to their own masonry slot at whatever height content actually needs, alongside the handful that keep a real image. Don't invent a placeholder image just to keep the masonry rhythm going.
- **chartHeavy**: exhibits become captioned charts, maps, or diagrams; sizing shifts to "the figure genuinely needs this width," not visual variety. If the real signal is importance rather than shape, that's `bento-mosaic`'s job.
- **cardOrListHeavy**: weakest fit of the three — the archetype's narrative-sequence read fights against independent, non-sequential, comparable items. Only use where every item genuinely has its own real image at its own aspect ratio.

## Medium Notes
- Presentation: each exhibit becomes its own slide at the image's real proportions — a wide exhibit becomes widescreen, a tall one portrait, never resized to one shared 16:9 master.
- Print: exhibits flow in reading order at real aspect ratio; page breaks fall between exhibits, never mid-image — no fixed n-per-page rule, the images' own proportions set the page rhythm.
- Markdown: weak fit — flag rather than silently degrade. If unavoidable, preserve reading order with each cutline as an italic line under its image, but recommend a web or PDF export instead.

## Pairing Notes
- `tokyo-screentone` — manga panel layout (deliberately varying panel size/shape telling a visual story in sequence) is a real-world precedent for this exact archetype; its zero-softening, hard-edged ink aesthetic reads as confident photo-essay presentation.
- `verdigris-patina` — its own gimmick is color literally aging top-to-bottom down the page, a visual-progression device that fits a photo essay's narrative arc even more directly than its original pairing.
