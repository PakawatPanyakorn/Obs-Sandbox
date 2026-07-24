# card-catalogue-index

**Archetype:** card-catalogue-index · **Family:** grid-discipline

## Core Concept
The one deliberate exception in the catalog that legitimately reads as "a grid of items" — because the grid is a literal table (rules + columns), never decorative cards. Hierarchy is positional and role-based (body > rail > masthead), not size-based, which is exactly right when every entry is genuinely comparable. The tell for drift: any single row getting a border, shadow, or extra padding "because it's featured" — that's the card-grid instinct sneaking back in; a pinned row earns a heavier rule at most.

## When To Use
- Glossaries, terminology references, style guides, bibliographies — content genuinely built from many comparable name+definition entries.
- API reference indexes, metrics dictionaries, changelog tables, endpoint directories — anywhere numeric fields need column alignment, not sparkline decoration.
- Component libraries, product/plugin directories, staff or vendor directories — the archetype's native mode, needing almost no adaptation.

## When NOT To Use
- Content with fewer than ~30 entries — the rail is explicitly optional and should be omitted below that threshold; adding it anyway is decoration without function.
- Content where individual entries genuinely differ in importance — this archetype's whole premise is that entries are comparable; if one deserves real visual prominence, a different archetype (e.g. `bento-mosaic`) fits better.
- Anywhere the instinct is to add colored status dots, bars, or thumbnails to every row — that turns an index into a dashboard rail, which is a different, less honest thing.

## Region / Component Guidance
- **masthead** (`1 / 13`): quiet, small, carries the index's own metadata (entry count, category count) — never a KPI dashboard opener.
- **rail** (`1 / 4`, optional, omit below ~30 entries): alphabetic or category jump-nav linking to row-groups in the body. Present only once the index is long enough to need lookup navigation.
- **body** (`4 / 13`): the index itself as a real `<table>` — rows and columns only, no borders/fills/shadows/radius on individual entries. `--lf-card-radius` and `--lf-shadow-hero` are intentionally almost unused here, reserved for one decorative textless spine strip at most, never for a row.

## Content-Type Notes
- **textHeavy**: body becomes a true glossary — one term, one definition per row, groups collapse to alphabet letters, rail becomes an A–Z jump list. Ragged row heights are correct; don't pad short definitions to make rows visually even.
- **chartHeavy**: non-label columns become numeric/data fields, right-aligned and set in mono font so digits line up; groups become module/service names instead of letters. Keep numeric columns plain aligned text — no sparklines, bars, or colored dots.
- **cardOrListHeavy**: the archetype's native mode. Each row is one item (component, product, directory entry) with name, category, status, one-line description, exactly as designed — no adaptation needed.

## Medium Notes
- Print: the rail becomes a running header repeating the current category at the top of each page, like a dictionary's guide word; the group-heading row repeats if a group spans a page break.
- Markdown: body degrades to a native markdown table (or nested definition list); rail is dropped entirely since markdown has no sticky in-page navigation — the table's natural top-to-bottom order replaces lookup.
- Presentation: rail drops entirely; each category group becomes its own slide with the group heading as the slide title, rows as a simple aligned list — still no boxes.

## Pairing Notes
- `moss-cottage` — a card catalogue was historically literal library furniture; moss-cottage's gentle herbarium/field-guide register reads as exactly that kind of orderly reference shelf, without ever reaching for a card grid.
- `alpha-signal` — its Bloomberg-terminal density (mono data columns, teal grid, compact spacing) is exactly the dense, aligned register a metrics/API index calls for; also proves the same theme can skin two structurally different archetypes (reused from `dashboard-with-rail`).
