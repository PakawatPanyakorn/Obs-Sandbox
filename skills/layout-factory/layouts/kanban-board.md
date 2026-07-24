# kanban-board

**Archetype:** kanban-board · **Family:** dashboard-legitimate

## Core Concept

A variable number of equal-width vertical lanes, each a content-driven stack of individually bordered cards. The hierarchy mechanism is stage, not size — a card's importance is signaled by which lane it's in and whether it carries a flag, never by making it visually bigger than its neighbors. This is the one archetype in the whole catalog where individually bordered/shadowed card boxes are correct by default rather than the anti-pattern this skill otherwise guards against, because each card is a genuinely discrete, independently movable unit of work — exactly the "distinct unit" exception `anti-patterns.md` itself allows. The tell that someone got it wrong: a card that's really just decorative section content dressed up as a task, or a lane whose width or card styling differs from its neighbors for no structural reason.

## When To Use

- Software issue trackers, editorial content pipelines, hiring pipelines, and sales pipelines — any workflow genuinely organized by discrete, movable stage.
- Lightweight personal or team to-do systems where stage (not priority) is the primary organizing axis.
- Support/ticket queues that want a stage-based view alongside (not instead of) real analytics.

## When NOT To Use

- A one-time linear process walked through once (an onboarding checklist, a setup wizard) — that's a plain ordered list, not a board people repeatedly move cards through.
- Content that needs real flow analytics (cycle time, throughput, burn-down) as its primary purpose — that's `kpi-strip-hero-chart` or `dashboard-with-rail`'s job; a kanban board's per-lane count badge is the only number that belongs on this page.
- A workflow with a fixed, small, always-the-same number of stages known in advance — if the stage count and order never vary, `quad-chart-briefing-grid` (for exactly four) or a plain sequence may communicate it more clearly than a live board.

## Region / Component Guidance

- **`.lf-kb-header`** (`masthead`, spans `1 / 13`): title, filters, and an add-card control. The judgment call: keep per-lane counts in the lane header (`.lf-kb-lane-count`), not duplicated here.
- **`.lf-kb-rail`** (`rail`, optional, `flex: 0 0 160px`): a board/view switcher. The judgment call: omit this entirely when there's only one board — adding a rail just to look like a "real" tool when there's nothing to switch between is the dashboard-trope anti-pattern applied to this archetype specifically.
- **`.lf-kb-lane`** (`lane`, repeated, `flex: 1 1 0`): a `.lf-kb-lane-header` plus a vertical stack of `.lf-kb-card` elements. The judgment call people get wrong most often: forcing every card in a lane to the same height "for tidiness" — card height must stay entirely content-driven.
- **`.lf-kb-card`**: the archetype's one legitimate bordered box. Fields (title, optional tag, footer with assignee/date) should stay consistent across every lane so a card's shape doesn't change when it moves between stages. `.flagged` cards get the emphasis-border treatment for genuine blockers or SLA risk — never applied decoratively.

## Content-Type Notes

**textHeavy**: cards hold a title and at most one line of `.lf-kb-card-desc`. If a task genuinely needs paragraph-length context, that context belongs in a linked document, not expanded inline on the card.

**chartHeavy**: a `.lf-kb-card-stat` (a bare number in display type) may appear on individual cards to represent a per-card metric — but a genuine analytics view belongs in a separate archetype entirely; don't let this become the board's second purpose.

**cardOrListHeavy**: the native mode — every card gets the same small field set (title, optional `.lf-kb-card-tag`, `.lf-kb-card-footer` with an avatar and a date), varying only in content and height, across every lane.

## Medium Notes

`mediaAdaptation.presentation` and `.print` are both genuinely weak here — a live, draggable board has no meaningful static equivalent. If a snapshot is needed for a deck or document, treat it explicitly as a dated screenshot rather than trying to preserve interactivity, or better, re-express the same information as a `data-dense-report-grid` table (task, stage, owner).

## Pairing Notes

- **neon-foundry** — reach for this to make kanban's own factory-floor lineage (it originated as a Toyota production-control system) explicit rather than incidental.
- **cosmica** — reach for this for a sci-fi "mission-control tile board" register, a near-literal description of the archetype's own lanes-of-cards structure.
- **bauhaus-konstrukt** — reach for this when cards need a second visual signal (type/label) via its own multi-hue card-bar convention, without inventing a new component.
