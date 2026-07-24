# feature-trio-grid

**Archetype:** feature-trio-grid · **Family:** grid-discipline

## Core Concept

A centered hero sits above exactly three (rarely four) identically-sized panels in a single row. The hierarchy mechanism here is unusual for this skill: instead of size contrast separating important from secondary, all three panels are deliberately equal because the content genuinely is three parallel, equally-weighted claims — this is the one archetype in the whole catalog where uniform sizing is the correct structural signal rather than the default-card-grid anti-pattern. The tell that someone got it wrong: try swapping the order of the three panels. If one clearly has to come first, or a fourth got added "real quick," the content was never actually parallel, and the trio's whole justification collapses.

## When To Use

- A SaaS or product marketing page's "why choose us" section, stating three genuinely interchangeable value propositions in a fixed count of three.
- A landing page proving traction with three comparable metrics measured the same way (not three unrelated KPIs dressed up to look parallel).
- A services page introducing exactly three comparable engagement types or tiers before a dedicated pricing/comparison page takes over the fine-grained detail.

## When NOT To Use

- Content where one item is genuinely more important than the other two — that's `magazine-well`'s job, where size contrast does the work this archetype deliberately refuses to do.
- More than three genuinely parallel items — once there are four or more, this is `card-catalogue-index`'s job (a real table/list), not a stretched or wrapped trio.
- Any page that wants the panels to carry a border, shadow, or rounded card treatment as a decorative default — the moment that happens, this has drifted into the exact uniform-card-grid anti-pattern this archetype's discipline exists to avoid, even though the layout looks superficially similar.

## Region / Component Guidance

- **`.lf-ftg-header`** (`masthead`, spans `1 / 13`): logo, a short primary nav (2-3 items), and a single secondary CTA/login link. The judgment call: resist a second header row — a mega-menu or breadcrumb here starts competing with the hero for the first-glance moment.
- **`.lf-ftg-hero`** (`lead`, spans `1 / 13`): a centered headline, one-line subhead, and exactly one primary CTA button. This is the only region that gets `--lf-shadow-hero`/`--lf-gradient-hero` treatment. The judgment call: keep the subhead to one sentence — a second sentence here starts duplicating what the trio panels are about to say individually.
- **`.lf-trio`** (`well`, spans `1 / 13`, internally `grid-template-columns: repeat(3, 1fr)`): each `.lf-trio-item` gets an optional small `.lf-trio-icon` (or `.lf-trio-stat` in the chart-heavy variant), an `<h3>`, and exactly one sentence of `<p>`. The judgment call people get wrong most often: adding a fourth `.lf-trio-item` "just this once" — do that and the count is no longer three, and the equal-weight claim needs re-justifying from scratch, not just a wider grid.
- **`.lf-ftg-closing`** (`body`, spans `1 / 13`): optional — a one-line restated CTA. The judgment call: omit this region entirely rather than inventing a second call-to-action; a page with two competing CTAs undermines the hero's single primary one.

## Content-Type Notes

**textHeavy**: drop `.lf-trio-icon` entirely on every panel — with no supporting imagery anywhere on the page, the hero's subhead needs to do a little more work to frame what the three panels are about to individually restate in one sentence each.

**chartHeavy**: replace `.lf-trio-icon` with `.lf-trio-stat` (a bare number in display type) above the heading — but only when the three numbers are measured the same way across the same population. If they come from different time windows or different segments, they aren't parallel enough for this archetype; route them through `data-dense-report-grid` instead, where per-figure caveats have room to exist.

**cardOrListHeavy**: each `.lf-trio-item` becomes one comparable offering (a plan, a tier, an engagement type) with its name as the `<h3>` — still capped at three, still no border beyond the shared hairline top-rule, and still ordered so that swapping any two panels loses no information a reader needs.

## Medium Notes

`mediaAdaptation.presentation` is a genuine strength here, not an afterthought: the trio maps directly onto a 3-up slide body zone (pair with `slide-master-deck-grid` for the deck-level frame) with no adaptation needed, unlike most editorial archetypes which have to be reinvented for slides.

## Pairing Notes

- **bauhaus-geometry** — reach for this when the trio should read as literally geometric — its "shapes ARE the UI" philosophy makes the three-equal-badges concept visually explicit rather than merely structural.
- **acid-garden** — reach for this to stress-test the trio's discipline under a maximalist register; if the "exactly three, one sentence each" rule still reads clearly through this much color, it'll hold under anything calmer.
- **harbor-clay** — reach for this for enterprise/B2B marketing that wants the trio to read as trustworthy and restrained rather than playful.
