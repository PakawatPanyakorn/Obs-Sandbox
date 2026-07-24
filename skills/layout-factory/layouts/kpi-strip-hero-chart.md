# kpi-strip-hero-chart

**Archetype:** kpi-strip-hero-chart · **Family:** dashboard-legitimate

## Core Concept

A capped horizontal strip of three to six top-line KPI tiles sits directly above one dominant hero chart, followed by two or three smaller captioned exhibits. The hierarchy mechanism is causal, not just visual: the strip creates a question ("why does uptime look like that?") and the hero chart directly beneath it is required to answer that specific question — not introduce a new topic. The tell that someone got it wrong is a hero chart that doesn't obviously relate to any tile in the strip above it, or a strip that keeps growing past six tiles because "there's room." This is deliberately the simplest member of the `dashboard-legitimate` family — no persistent nav rail at all, unlike `dashboard-with-rail` or `holy-grail` — because it models a single overview screen, not a multi-section app shell.

## When To Use

- A BI or analytics tool's default "Overview" screen: a handful of top-line numbers plus the one chart that explains their current state.
- An executive dashboard or weekly metrics review page where the reader scans numbers first, then reads exactly one chart to understand why they look that way.
- A status page (via the text-heavy variant) that wants an at-a-glance state strip before the incident narrative.

## When NOT To Use

- Content with no genuine top-line numbers — see Content-Type Notes on `textHeavy` for the honest fallback; don't invent KPI tiles just to look data-driven.
- A multi-section app with real navigable facets — that's `dashboard-with-rail`'s or `holy-grail`'s job; this archetype is deliberately rail-free and single-screen.
- Content with two or more charts that are each independently important — split them across two screens of this archetype (or use `data-dense-report-grid`, which allows multiple co-equal exhibits) rather than fighting for one hero slot.

## Region / Component Guidance

- **`.lf-masthead`** (`masthead`, spans `1 / 13`): identity plus a scope/date-range selector. The judgment call: don't let a nav tree creep in here — the absence of a rail is the point.
- **`.lf-kpi-strip`** (`summary`, spans `1 / 13`, `grid-template-columns: repeat(auto-fit, minmax(140px, 1fr))`): three to six `.lf-kpi-tile`s, at most one carrying `.emphasis`. The judgment call people get wrong most often: letting a seventh tile sneak in "just this once" — that's the exact discipline this archetype is built to hold the line on.
- **`.lf-hero-exhibit` / `.lf-hero-panel`** (`lead`, spans `1 / 13`): the one chart or panel with real visual weight (`--lf-shadow-hero`/`--lf-gradient-hero`). The judgment call: this region is mandatory — a strip with nothing beneath it explaining the numbers is stat-tile decoration, not this archetype.
- **`.lf-exhibit-grid`** (`river`, spans `1 / 13`): two to three `.lf-exhibit-mini` blocks, each with a numbered caption and one sentence of interpretation. The judgment call: never let a bare number reappear here without a caption — that's the same "generic dashboard" anti-pattern the strip itself is disciplined against.

## Content-Type Notes

**textHeavy**: the strip becomes 3-4 `.lf-status-chip` indicators (a few words each, not numbers), and the hero region becomes a written narrative (`.lf-hero-panel` with a timeline) instead of a chart. If a status needs more than three words, it belongs in the narrative, not the chip.

**chartHeavy**: the archetype's native mode — fill the strip with genuinely top-line numbers, the hero with the one chart that most explains them, and the river with 2-3 smaller exhibits, each captioned and interpreted in one sentence. This is the variant most tempting to over-fill; hold the strip at six tiles and the river at three exhibits even when more data exists.

**cardOrListHeavy**: the strip stays numeric (count, average age, oldest item); the hero becomes the single most urgent record as a `.lf-hero-panel`; the river becomes a plain `.lf-record-list` — only the hero record ever gets the bounded-panel treatment.

## Medium Notes

`mediaAdaptation.presentation` is a real strength: the strip maps onto a slide's title band, the hero chart becomes that slide's dominant visual per `slide-rule-of-thirds`, and each river exhibit becomes its own follow-up slide — no reinvention needed, unlike most dashboard-family archetypes which degrade hard outside the browser.

## Pairing Notes

- **cyber-terminal** — reach for this for a literal "analyst workstation" monitoring register; green phosphor readouts are what this archetype's strip looks like at its most technical.
- **prism-ledger** — reach for this for finance/exec-summary content where the KPIs really are ledger numbers; its ruled-ledger register makes the ledger metaphor explicit.
- **amber-signal** — reach for this when you want the same CRT-instrumentation feel as cyber-terminal but in a warmer, single-wavelength amber register instead of green.
