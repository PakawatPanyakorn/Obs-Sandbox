# uniform-tile-grid

**Archetype:** uniform-tile-grid · **Family:** grid-discipline

## Core Concept

A dense wall of perfectly equal square tiles with no persistent captions, no count cap, and no order significance — the purest form of legitimate uniform sizing in this catalog. Every other "legitimate uniformity" archetype here earns its equality through a specific constraint: `feature-trio-grid` caps at exactly three interchangeable items, `pricing-comparison-table` allows exactly one deliberate exception, `quad-chart-briefing-grid` fixes exactly four items in a locked order. This archetype has none of those constraints — tiles can be freely added, removed, or reordered without breaking anything, because the content genuinely has no hierarchy to encode in the first place. The tell that someone got it wrong: one tile is actually more important than the others (then this is the generic uniform-card-grid anti-pattern, not this archetype), or tiles carry a persistent bordered "card" treatment instead of sitting flush.

## When To Use

- Instagram-style profile grids and photography portfolios where every image is a genuine peer of every other.
- Simple product catalog grids and avatar/team walls where identity comes from the image alone.
- A tag/category wall or icon-only sitemap (via the text-heavy variant) where every entry is equally accessible with no ranking implied.

## When NOT To Use

- Content where one item is actually more important — use `bento-mosaic` (varied by importance) instead, where cell size is the whole point.
- Content whose visual weight should vary with its own aspect ratio or narrative significance — use `masonry-photo-essay` instead, where a wide panorama is wide because it genuinely is.
- Text-heavy content needing more than a two-word label per item — the square constraint makes this archetype a poor fit for anything that needs real reading room; use `card-catalogue-index` instead.

## Region / Component Guidance

- **`.lf-utg-header`** (`masthead`, spans `1 / 13`): title plus an optional sort control. The judgment call: if sort order is present, make sure it's genuinely inconsequential to the grid's meaning — a sort control on a grid where order actually matters signals this archetype was chosen for the wrong content.
- **`.lf-utg-grid`** (`well`, spans `1 / 13`, `repeat(auto-fill, minmax(140px, 1fr))`): every `.lf-utg-tile` gets `aspect-ratio: 1` and a border only (never a shadow or the emphasis token) — tiles are flush squares, not bordered cards. The judgment call people get wrong most often: adding a persistent caption band under every tile, which reintroduces the uneven-height problem the aspect-ratio lock exists specifically to prevent. Use the hover-reveal `.cap` element instead.
- **`.lf-utg-footer`** (`body`, spans `1 / 13`, optional): a load-more control. The judgment call: omit entirely when the full set already fits on one screen — inventing pagination for a dozen items just to look like a "real" gallery is unnecessary chrome.

## Content-Type Notes

**textHeavy**: use `.lf-utg-tile.label` — a short word or two centered in the square, revealed fully rather than truncated. If the label needs more than two words to make sense, the content has outgrown this archetype.

**chartHeavy**: use `.lf-utg-tile.stat` — a bare number in display type, no label, no icon. Every tile's number must come from the exact same metric and time window; mixing metric types here misrepresents unrelated numbers as comparable.

**cardOrListHeavy**: the native mode — plain `.lf-utg-tile` with an image background and a hover-only `.cap` caption. This is the Instagram/portfolio/catalog shape the archetype is named for.

## Medium Notes

`mediaAdaptation.presentation` and `.print` both explicitly recommend sampling rather than full reproduction: show six to nine representative tiles captioned as a sample, rather than trying to force a 50-tile wall onto a slide or page — the density that makes this archetype work on a scrolling web page is exactly what breaks it in a fixed-size medium.

## Pairing Notes

- **wisdom** — reach for this for a contemplative gallery-wall register, treating each tile as a small work on a museum wall.
- **tokyo-screentone** — reach for this for a graphic, high-contrast register; note it's reused from `masonry-photo-essay` to skin a deliberately *different* structural claim (uniform squares here vs. varied panel sizes there) with the same visual identity.
- **moss-cottage** — reach for this for an artisan/handmade shop-grid register, where the equality of tiles reflects genuinely comparable small-batch items.
