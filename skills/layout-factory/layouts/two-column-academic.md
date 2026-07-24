# two-column-academic

**Archetype:** two-column-academic · **Family:** grid-discipline

## Core Concept
A full-width masthead (title, authors, abstract) sits above a body set in two genuinely balanced text columns joined by a hairline column-rule — native CSS multi-column, not two hand-split grid tracks. Figures and tables break the column grid only when they need the full measure (`column-span: all`), appearing inline at their point of reference, then hand control straight back to the two-column flow. The masthead is the one region given surface/shadow presence, mirroring `magazine-well`'s "one hero, everything else earns its weight by content" rule with the hero swapped for the masthead.

## When To Use
- Research papers, theses, formal proposals, technical or legal reports — anything meant to be printed or PDF-bound and read closely rather than skimmed, the archetype's native case.
- Empirical papers, statistical appendices, technical reports carrying several supporting tables or figures that need inline, numbered, captioned placement.
- Literature reviews, annotated bibliographies, criteria/rubric sections — a genuinely comparable set of items as a hanging-indent list, not a card grid.

## When NOT To Use
- Anywhere the instinct is to add photography or decorative imagery to fill an empty column — this register signals rigor through typographic discipline, not visual richness; an empty column is fine, a decorative one undercuts the point.
- Content where exhibits would crowd out running text until the page is mostly captions — if interpretation shrinks to caption fragments and charts dominate, that's `data-dense-report-grid` territory instead.
- Comparable-item lists wanting bordered cards — a hanging-indent list is this register's own convention; card boxes read as marketing collateral and break the academic register the moment they appear.

## Region / Component Guidance
- **masthead** (`1 / 13`, full width, never split): kicker, title, byline, affiliations, abstract, keywords. The only region allowed real surface/shadow presence.
- **body** (`1 / 13`, `column-count: 2`): running two-column article text — the browser balances columns natively. Both columns share identical font-size and line-height so baselines line up across the gutter, not just within one column. Carries at most one small-caps "Key Finding" pull quote per major section (quiet weight, never italic or oversized — should read as data, not decoration).
- **exhibit** (`1 / 13`, breaks out via `column-span: all`): figures and tables that need the full measure, appearing inline at point of reference, never collected in an appendix. Table captions sit above the table, figure captions below — real print convention, not interchangeable.

## Content-Type Notes
- **textHeavy**: the native case — dense continuous prose runs across both columns; exhibits drop out entirely, the only breaks are a footnote reference and at most one boxed key-finding per major section.
- **chartHeavy**: every chart/table becomes a numbered, captioned exhibit breaking the column grid inline; commentary in the surrounding column text always explains what to look at. An uncaptioned exhibit with no interpretive sentence is the dashboard-trope anti-pattern this structure is built to avoid.
- **cardOrListHeavy**: a genuinely comparable set (related work, references, selection criteria) becomes a single hanging-indent list at column width, ordered by stated logic (usually chronology), entry length varying with the source's own annotation.

## Medium Notes
- Print: this archetype's native medium — US Letter/A4, ~0.75in margins, running header (journal/series name + volume) and footer (page number); the twin columns already model to a print column grid pixel-for-pixel.
- Markdown: twin columns don't exist in markdown — body degrades to a single flowing column. Preserve numbered section headings (`## 1. Introduction`) and set figures/tables/key-findings off in a fenced block or blockquote so they still read as breaking from body text.
- Presentation: poor fit — the entire structure exists to keep dense continuous prose readable across two narrow columns, which doesn't survive being chunked onto slides. If unavoidable, drop to one section per slide, single column, footnotes to an appendix slide.

## Pairing Notes
- `crypt-scholastic` — literally "dark gothic academic," a rare-books institution register that already reads as scholarly authority; the twin-column grid gives its dense manuscript-catalogue prose somewhere disciplined to run.
- `bloc-brutus` — a literal architectural grid overlay and "structure is truth" design philosophy; applied to a genuinely balanced twin-column grid, it reads as a technical/engineering report register rather than a magazine spread.
- `vesper-furrow` — its own demo content is already formal report register (land-register entries, parcel references, surveyor notes), a close sibling to the academic paper this archetype is built for.
