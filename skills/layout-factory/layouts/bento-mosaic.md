# bento-mosaic

**Archetype:** bento-mosaic · **Family:** grid-discipline

## Core Concept
A modular 6×3 grid where tile area is a stated claim about importance, recency, or data density — never decoration. The archetype sits right next to the uniform-card-grid anti-pattern it exists to avoid, so the defining discipline is the **shuffle test**: if any two tiles could swap positions without changing what the page communicates, the sizing has drifted from bento into decoration wearing a grid.

## When To Use
- A quarterly letter, metrics review, or portfolio index with a genuine one-item-dominates-the-rest shape: one lead finding, two mid-tier exhibits shaped differently from each other on purpose (one tall/dense, one wide/flat), and a tier of truly interchangeable peer items.
- Content where you can name, out loud, *before* you start building, why each tile is the size it is — importance, recency, or data density are the only three legitimate reasons.

## When NOT To Use
- A set of items that are all genuinely comparable in weight — inventing size variety to "look organized" is the exact anti-pattern this archetype must avoid; use `card-catalogue-index` or a plain list instead.
- Content where nothing is actually more important than anything else this period — padding the lead tile with filler prose to justify its size is the textbook failure mode, called out directly in the preset's own copy.

## Region / Component Guidance
- **lead** (`.lf-tile-lead`, grid area `columns 1/4, rows 1/3` — 3×2, 6 of 18 units): reserve for the single statistically/narratively dominant item. It's the *only* tile that gets the theme's real hero treatment (`--lf-gradient-hero`, `--lf-shadow-hero`) and the only zone that carries `.lf-pullquote` — giving a second tile that same visual weight is the anti-pattern the archetype exists to avoid.
- **exhibit-b** (`.lf-tile-exhibit-b`, `columns 4/6, rows 1/3` — 2×2, tall): use for content that's genuinely multi-dimensional (a multi-series chart, a two-part update). The height exists to serve data density — "height serves density, not drama," per the preset's own concept-tab copy.
- **exhibit-a** (`.lf-tile-exhibit-a`, `columns 1/4, row 3/4` — 3×1, wide/short): use for a single flat comparison with no need for height. If you find yourself wanting a second row here, the content probably belongs in exhibit-b instead.
- **river-1..5** (`.lf-tile-river-*`, 1×1 each): the one place uniform sizing is legitimate — these five must be genuine peers, ranked only by recency. `river-1` additionally carries `.lf-tile-emphasis` (a border-color swap only, per the theme's own "alt card" convention) as the most-recent-item marker.

## Content-Type Notes
- **textHeavy**: tile area buys word count, not imagery — lead gets a full paragraph + pull quote, exhibits get one to two sentences sized to their span (exhibit-b's height buys two short paragraphs, exhibit-a's width doesn't), river tiles get one clause each. If every tile ends up roughly the same length, this is the wrong archetype.
- **chartHeavy**: the archetype's native mode — tile size maps directly to statistical significance, recency, or data density. Every tile still carries a one-line interpretation caption (`.lf-tile-caption`/`.lf-tile-reason`); a bare floating number is the dashboard-trope anti-pattern wearing this archetype's clothes.
- **cardOrListHeavy**: tile size maps to project/item scope — one flagship case study in lead, medium-scope items in the exhibits, quick items in river. Don't force scope differences onto items that are actually comparable just to fill the grid shape.

## Medium Notes
- Markdown degrade order is fixed: lead, exhibit-b, exhibit-a, river-1..5 — heading level and paragraph length must still track the original tile size (H2 + full paragraph for lead, H3 + one sentence for exhibits, a bolded clause for river). A flat bullet list of eight equal-looking items erases the entire point of the archetype.
- Presentation: never compress all 8 tiles onto one slide — split lead alone / the two exhibits side by side / river as a ranked list across at least 3 slides.
- Breakpoints collapse to a strict single-column list in the *same* hierarchy order (`lead, exhibit-b, exhibit-a, river-1..5`), never a naive reflow of `grid-template-areas` that would scramble the hierarchy.

## Pairing Notes
- `acid-garden` — proves the sizing discipline survives a theme that's itself chromatically maximalist; reach for this pairing when you want to demonstrate the archetype isn't just a "quiet theme" trick — cell size still tracks importance/density, never the palette.
- `cosmica` — dark glass-panel register reads as literal mission-control tiles; use this pairing specifically for chart-heavy/analytics use cases where a sci-fi-dashboard register is wanted, distinct from acid-garden's light chromatic energy.
