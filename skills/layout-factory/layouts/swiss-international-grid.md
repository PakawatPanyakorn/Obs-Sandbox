# swiss-international-grid

**Archetype:** swiss-international-grid · **Family:** grid-discipline

## Core Concept
A strict twelve-column modular grid where hierarchy is built entirely from scale and position — an asymmetric flush-left headline column set against grid-locked photography or exhibits, never a box or shadow. Everything is poured into the module; nothing is centered or free-floating. Importance is read off column count and type scale alone — the discipline that separates this from a generic "grid layout" is that every region's span is a declared line-range, never fractional or auto placement.

## When To Use
- Manifestos, policy briefs, technical standards, specifications — long-form prose where the grid's job is pure reading discipline, not photo layout.
- Data reports, scientific figures, transit/wayfinding studies, engineering documentation — content where several exhibits must hold to one shared column discipline.
- Spec sheets, exhibition catalogues, transit timetables, session/agenda listings — comparable items that still need a strict scan order.

## When NOT To Use
- Anywhere the instinct is to center the text column "to balance" an empty exhibit space — flush-left, ragged-right must hold even with no image counterweight; centering breaks the module.
- Multiple exhibits wanting to be resized "to look better" rather than holding to their declared column span — that inconsistency is exactly what this archetype's discipline exists to prevent.
- List items wanting bordered or shadowed boxes for separation — a 3-up card grid here is the exact uniform-grid anti-pattern this archetype exists to replace with real grid discipline; the column module and a hairline rule are the only separators.

## Region / Component Guidance
- **masthead** (`1 / 13`): small, quiet, states the module reference (grid/gutter/date) — never competes with the lead.
- **lead** (`1 / 6`): dominant headline + intro copy, flush-left, ragged-right, asymmetric placement. Scale alone signals importance, no box or background fill. Carries the page's pull quote as an oversized type statement with a hairline rule ABOVE it (a grid line made visible), never a left border or quotation marks.
- **exhibit** (`6 / 13`, occasional): grid-locked photography/chart module, present only when there's a genuine image or chart — a text-only page reassigns these columns to marginalia instead of inventing a placeholder. Every exhibit carries a numbered, flush-left caption, never a bare stat tile.
- **body** (`1 / 8`): running text in a narrower measure than the full grid, flush-left ragged-right. The margin column (8-12) carries sidenotes and citations set in mono/caps, never a footnote block at the page bottom.

## Content-Type Notes
- **textHeavy**: exhibit region drops out rather than being filled with a placeholder; the lead's asymmetric split becomes a wide headline column (1-7) against a narrow strip of grid-locked marginalia (8-12) so the page still reads as asymmetric even with no photography.
- **chartHeavy**: exhibit becomes the dominant element at its exact declared column span with a numbered caption at the same left edge. Most likely variant to drift into a dashboard — prevented by every exhibit being a numbered figure with a caption and pre-declared column span, never a floating stat tile.
- **cardOrListHeavy**: comparable items run as a flush-left list within the body column, separated by hairline rule at a fixed baseline interval, item numbers in mono type. A genuinely more significant item gets larger type scale or the full exhibit treatment, never a background fill or shadow.

## Medium Notes
- Presentation: each slide repeats the same title/body/footer margin system — fixed-position title block flush-left at the same inset on every slide, a body region holding exactly one idea, a footer rule plus folio number at a fixed baseline; the module never changes, only its content.
- Print: classic modular grid — identical outer margins every page, running section/folio number in the same corner of every spread, text/image blocks locked to the same column module throughout; no page invents its own margin or column count.
- Markdown: degrades to strict flush-left heading hierarchy — masthead becomes a small kicker or is omitted, lead headline becomes H1, exhibit becomes an image reference with numbered caption, body runs as plain paragraphs. The asymmetric column split can't survive; numbering and heading discipline carry over instead.

## Pairing Notes
- `prussian-blueprint` — its entire UI chrome (leader lines, dimension ticks, callout markers, a literal three-layer grid background) is a drafting-table rendering of the same modular grid this archetype formalizes.
- `titanium-cloud` — a literal fine cool-gray grid background ("engineering graph paper") and restrained SaaS register favor structure over decoration without ever fighting the twelve-column module.
- `bauhaus-konstrukt` — Swiss International Style descends directly from Bauhaus/New Typography's insistence on grid, function, and primary color as structure; its red/blue/yellow triad and zero-radius geometry read as this archetype's ideological ancestor made explicit.
