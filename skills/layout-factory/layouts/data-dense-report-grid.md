# data-dense-report-grid

**Archetype:** data-dense-report-grid · **Family:** data-dense-report

## Core Concept
A tight vertical stream of numbered, captioned exhibits with running commentary — every chart or table is a figure, never a floating stat tile. No single exhibit dominates; every one carries equal structural weight, and the discipline of number + caption + commentary is what keeps the sequence reading as an analyst report instead of a dashboard. This is the archetype most exposed to the dashboard-trope: a bare number or chart with no caption and no interpretation sentence is a KPI tile, not an exhibit, no matter how self-explanatory it feels.

## When To Use
- Analyst notes, quarterly business reviews, research summaries, investor letters — content organized around a sequence of findings, the archetype's native mode (4-6 exhibits, each numbered/captioned/interpreted).
- Policy briefs or long-form research summaries where narrative carries more weight than exhibits — thin the exhibits to one or two, and let the brief carry most of the argument.
- Portfolio reviews, vendor comparisons, ranked leaderboards presented as report-format ranked tables treated as numbered figures, not a grid of uniform cards.

## When NOT To Use
- Content where every comparable item wants its own card — that's the uniform-card-grid anti-pattern with numbers stapled on; group comparable items into one or two table-format exhibits instead.
- Anywhere a chart would be purely decorative — if a sentence in the brief says it better than a chart would, don't add the chart, especially in text-heavy variants.
- Live/filterable dashboard content with facets a user switches between — that's `dashboard-with-rail`'s job, not this archetype's static sequential stream.

## Region / Component Guidance
- **masthead** (`1 / 13`): small, quiet — report title + series label, same restraint as any masthead in this system.
- **brief** (`1 / 9`, narrower than full width): the opening framing paragraph stating the thesis the exhibits collectively support, before any numbers appear. Carries the report's single pull quote — a surface-tinted block with the theme's hero shadow/gradient, the one deliberately "special" visual moment on a page that otherwise treats every exhibit as a peer.
- **exhibit-stream** (`1 / 13`, repeating): 4-6 exhibits down the page, each with its own figure number, italic caption, and a paragraph of interpretation — never a bare chart. Exhibit visuals vary in height with what they actually hold (a small table vs. a multi-series chart), never forced to a uniform box.
- **sidenote** (`3 / 13`, inset within the citing exhibit, occasional): a citation/source note attached to one specific exhibit — appears only where a claim needs a source, never as a persistent running rail.

## Content-Type Notes
- **textHeavy**: exhibits thin to one or two, each a small inline table or single cited statistic; brief lengthens to carry most of the argument in prose. Don't pad text-heavy content with decorative charts that don't add information.
- **chartHeavy**: the archetype's native mode — 4-6 exhibits, each numbered, captioned, paired with 2-4 sentences of tight commentary; sidenote attaches wherever a figure draws on an external source. The rule that prevents dashboard-trope drift: every exhibit gets a figure number, caption, and commentary, no exceptions.
- **cardOrListHeavy**: comparable items (vendors, holdings, portfolio companies) become exhibits — each a ranked table treated as a numbered figure with its own caption; items that are individually unremarkable collapse into one summary exhibit instead of one card each.

## Medium Notes
- Print: classic analyst-report layout — single column, exhibits never split mid-caption across a page break, sidenotes fall to the foot of the page they're cited on like a real footnote, not collected as endnotes.
- Markdown: brief as an opening paragraph; each exhibit becomes an H2 "Fig. N — Caption" followed by a table/fenced code block, then a commentary paragraph immediately after — the H2 numbering preserves figure discipline even where the visual itself can't render.
- Presentation: one exhibit and its commentary per slide in numbered order; the figure number becomes a running kicker ("Fig. 3 of 6") so an audience can track position the way a reader would in the printed report.

## Pairing Notes
- `thermal-fade` — receipt-ledger register with a numbered TXN stamp and monospace line-item rows is structurally the same discipline as a numbered exhibit stream; already reads as an itemized statement.
- `amber-signal` — dieselpunk phosphor console with a literal transmission log and RSSI/frequency readouts reads as instrumentation for a report, not a product UI; glowing amber figures fit exhibit numbers and cited data points naturally.
- `cyber-terminal` — green-on-black CRT terminal with monospace type throughout is the most literal "analyst workstation" register; scanline texture and phosphor glow read as a terminal printing figures out one at a time, reinforcing the sequential stream.
