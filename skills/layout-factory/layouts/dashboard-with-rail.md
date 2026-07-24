# dashboard-with-rail

**Archetype:** dashboard-with-rail · **Family:** dashboard-legitimate

## Core Concept
The legitimate dashboard case named directly in `anti-patterns.md`'s "generic dashboard look on non-dashboard content" section. A persistent narrow rail (nav, filters, confined stat modules) runs beside a body showing exactly one active view at a time. The distinguishing test: every rail nav item and filter is something a user would actually click, and every stat module lives only in the rail or one bounded summary zone — never scattered through the body as loose cards. Applying this archetype to a static report with no real facets to switch between is itself the anti-pattern.

## When To Use
- Analytics consoles, monitoring dashboards, BI screens — genuinely filterable or live data with facets a user actually switches between.
- Admin panels, ticket/alert trackers, inventory or user-management tables — a genuinely browsable, filterable set of records.
- Long-form internal docs with real persistent section navigation (a runbook, policy handbook, reference guide people jump around in) — the rail becomes a table-of-contents, not a stat panel.

## When NOT To Use
- Static reports or documents with no real facets to switch between — inventing filters or live stats for content that has none is the exact anti-pattern this archetype exists to legitimately avoid elsewhere.
- Print or presentation deliverables by default — both are poor fits (see Medium Notes); re-route to `data-dense-report-grid` or `magazine-well` for print, or restructure entirely for slides.
- Content where "one active view at a time" doesn't apply — if everything needs to be visible simultaneously, this isn't a filtered/swapped-view archetype.

## Region / Component Guidance
- **rail** (`1 / 4`, persistent): navigation, filters, and confined stat modules. Never scrolls out of view independently — stays visible while body content changes beneath it. This is where numbers belong; they should not wander into the body as loose cards.
- **body** (`4 / 13`): the single active view — prose, an exhibit set, or a record list — swapped by the rail's controls rather than scrolled past. Only one hero visual per page.
- **exhibit-zone** (`4 / 13`, optional, nested in body): a single bounded chart/summary zone, present only when body content includes numbers or exhibits. Still one bounded zone, never cards strewn through prose.

## Content-Type Notes
- **textHeavy**: rail drops stat modules (prose has no numbers worth surfacing) and becomes a table-of-contents plus a small metadata block (owner, status, last-updated); body is single-column prose with one insight callout marking the single most load-bearing instruction, not running commentary.
- **chartHeavy**: rail carries real filters plus a compact stat-module stack (3-4 numbers, one emphasized); body opens with one bounded summary zone, then a hero exhibit with a numbered caption, then 2-3 smaller captioned exhibits — each paired with interpretation, never a bare number.
- **cardOrListHeavy**: rail becomes faceted browse controls (status, severity, assignee) plus a small stat stack; body pulls the single most urgent record into a hero panel, then lists the rest as hairline-divided rows — plain by default, with at most one row earning a border accent for genuine secondary urgency.

## Medium Notes
- Presentation: poor fit by default (flag as HTML/web-primary). If required, collapse the rail's nav into a single "contents" slide up front and give each body section its own slide; drop live-filter framing entirely.
- Print: also a poor fit — a printed rail reads as a static list with no way to act on it. Re-route to `data-dense-report-grid` or `magazine-well` instead of printing this archetype as-is.
- Markdown: degrades hard — no equivalent for a persistent always-visible rail. Represent rail nav as a bullet list ahead of body content, rail metadata as a small table, stat modules as an inline sentence or small table, and accept that "stays visible while body changes" is simply gone.

## Pairing Notes
- `alpha-signal` — its own description literally calls itself a "trading strategy / algorithm signal dashboard" with dense signal grid and Bloomberg-esque density; a rail confining live buy/sell/hold signals and backtest stats is exactly the content this theme was built to skin.
- `vault-theorem` — wealth-management "institutional allocation framework" with tiered navigation and a strategic allocation matrix; genuinely faceted content that a rail's filters and stat modules are built to hold.
- `eigenvalue` — a "quantitative algorithm lab" with live signal readouts and rolling factor-exposure scores beside an asymmetric hero panel; the same persistent-readout-beside-content shape this archetype formalizes into rail + body.
