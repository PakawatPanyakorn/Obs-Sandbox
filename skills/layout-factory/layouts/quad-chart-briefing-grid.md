# quad-chart-briefing-grid

**Archetype:** quad-chart-briefing-grid · **Family:** data-dense-report

## Core Concept

A fixed 2x2 grid of four visually identical quadrants — Situation, Complication, Data, Ask — where hierarchy comes entirely from a locked reading sequence rather than size contrast. This is a third, distinct kind of legitimate uniform sizing in this catalog: `feature-trio-grid`'s three items are interchangeable in order (any could come first), and `pricing-comparison-table` has exactly one deliberate exception; this archetype's four quadrants are both equal-sized *and* order-locked — Situation must be read before Complication, Complication before Data, Data before Ask, even though none of them is visually bigger than the others. The tell that someone got it wrong: a quadrant growing past its allotted quarter "because it needed more room," or an Ask quadrant that lists multiple options instead of committing to one recommendation.

## When To Use

- Policy briefs, executive one-pagers, and decision memos that already have a natural four-part shape: current state, what's changed, the evidence, the ask.
- Program status briefings and quarterly reviews that need to fit on a single page or slide, with exactly one supporting chart.
- Go/no-go and vendor-selection memos where the whole point is to force a single, clear recommendation rather than present a menu.

## When NOT To Use

- Content with a genuine single most-important element that size contrast should carry — use `magazine-well` or `data-dense-report-grid` instead, where hierarchy is explicitly signaled through scale.
- A comparison or narrative that doesn't fit a fixed situation → complication → data → ask sequence — forcing content into quadrants it doesn't naturally have breaks the format's logic rather than clarifying it.
- Content needing more than one real chart or table — the Data quadrant is this archetype's one legal exhibit slot; a second chart elsewhere means the content has outgrown a single page.

## Region / Component Guidance

- **`.lf-qc-header`** (`masthead`, spans `1 / 13`): title, date, and an audience/classification line. The judgment call: keep any "bottom line up front" callout here to one sentence — it previews the Ask, it doesn't replace it.
- **`.lf-qc-quad.qc-a`** (`exhibit-a`, Situation, spans `1 / 7`): the current state in one paragraph or a small exhibit. Always top-left, always read first.
- **`.lf-qc-quad.qc-b`** (`exhibit-b`, Complication, spans `7 / 13`): what's changed or what's at risk. The judgment call: this should create tension the Data quadrant then resolves — a Complication with no connection to the Data below it signals the four quadrants weren't actually planned as one argument.
- **`.lf-qc-quad.qc-c`** (`exhibit-c`, Data, spans `1 / 7`): the evidence, almost always via `.lf-hero-exhibit` with a numbered `.lf-caption`. This is the page's one legal chart slot — resist adding a second exhibit anywhere else on the page.
- **`.lf-qc-quad.qc-d`** (`exhibit-d`, Ask, spans `7 / 13`): a single named recommendation via `.lf-qc-ask`, using the quote-emphasis tokens. The judgment call people get wrong most often: writing "we could do A, B, or C" here — the format exists specifically to force a single answer.

## Content-Type Notes

**textHeavy**: all four quadrants stay prose. Situation and Complication get a tight paragraph each; Data cites figures inline rather than showing an actual chart; Ask states the decision in two or three direct sentences.

**chartHeavy**: the native mode — Data holds the one real `.lf-hero-exhibit` with a numbered `.lf-caption`, and Ask pairs its recommendation with at most one supporting stat, never a second chart.

**cardOrListHeavy**: each quadrant (except Ask) becomes a short `<ul>` of two to three items rather than full sentences; Ask stays a single `.lf-qc-ask` statement, never a list — a bulleted Ask quadrant is the clearest sign this archetype's core discipline has failed.

## Medium Notes

`mediaAdaptation.presentation` and `.print` are both native strengths, unusually so: the quad chart originated specifically as a one-page/one-slide military and policy briefing format, so this is one of the few archetypes in the catalog that needs no adaptation at all for those mediums — the web version and the "real" version are the same document.

## Pairing Notes

- **argent-vigil** — reach for this for the format's most literal historical register: a genuine military or defense-adjacent briefing.
- **soviet-agitprop** — reach for this when the memo needs to read as urgent and decisive rather than measured — its stark red/black register projects exactly that.
- **dead-letter-office** — reach for this for a bureaucratic, interoffice-memo register; its rubber-stamp status convention doubles naturally as a classification or routing stamp.
