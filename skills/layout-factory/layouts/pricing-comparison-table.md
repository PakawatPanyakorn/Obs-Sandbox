# pricing-comparison-table

**Archetype:** pricing-comparison-table · **Family:** grid-discipline

## Core Concept

Three (rarely four) plan columns of identical structure sit beneath a hero headline, with exactly one column carrying a deliberate visual elevation — larger scale, a stronger shadow, a "Recommended" badge. This is the one archetype in the whole catalog where breaking uniformity on a single item is the correct discipline rather than the anti-pattern this skill otherwise guards against: everywhere else, varying one box's size without a real reason is a tell; here, the elevated plan's whole job is to anchor a default choice, and *not* elevating exactly one plan is itself the failure mode. The tell that someone got it wrong: zero plans elevated (no default signal at all) or two-plus elevated (the signal cancels itself out).

## When To Use

- SaaS or product pricing pages with three or four genuinely comparable plans and a real "most people should pick this one" answer.
- Membership or subscription tiers where one tier is the intended default for the majority of signups.
- Usage-based or capacity plans (storage, seats, API calls) where the differentiator is a number rather than a feature list.

## When NOT To Use

- More than four plans, or plans that aren't genuinely comparable side by side — that's `card-catalogue-index`'s job (a real table), not a widened row of cards.
- No real recommendation to make — if every plan is equally likely to be right for a given buyer, don't manufacture a "Recommended" badge just to fill the pattern; a flat, unelevated `feature-trio-grid`-style row is more honest.
- A comparison so detailed it needs more than roughly five feature line items per plan — dense checkmark/cross grids belong in a real comparison table, not squeezed into card copy.

## Region / Component Guidance

- **`.lf-pct-header`** (`masthead`, spans `1 / 13`): logo, short nav, one secondary link. The judgment call: keep this quiet — it should not compete with the hero or the plan row for attention.
- **`.lf-pct-hero`** (`lead`, spans `1 / 13`): centered headline plus an optional `.lf-pct-toggle` (monthly/annual). The judgment call: if a toggle is present, make sure both states are genuinely supported — a fake toggle that doesn't change the prices beneath it undermines the whole page's credibility.
- **`.lf-plans`** (`well`, spans `1 / 13`, `grid-template-columns: repeat(3, 1fr)`): each `.lf-plan` shares identical internal structure (name, price, tagline/features, CTA); exactly one carries `.featured` (`transform: scale(1.04)`, `--lf-shadow-hero`, `--lf-gradient-hero`, and a `.lf-plan-badge`). The judgment call people get wrong most often: letting the featured plan's elevation creep into a genuinely different structure (extra sections the others don't have) rather than the same structure at greater visual weight.
- **`.lf-pct-closing`** (`body`, spans `1 / 13`): optional trust/guarantee line. The judgment call: omit rather than padding with generic reassurance copy that doesn't say anything the plans themselves don't already imply.

## Content-Type Notes

**textHeavy**: each `.lf-plan`'s feature list becomes a short paragraph instead of a bulleted `.lf-plan-features` list. Keep paragraph length roughly consistent across all three plans even as the content genuinely differs — a noticeably longer paragraph on one plan reads as favoritism, not information.

**chartHeavy**: add `.lf-plan-stat` (a bare number in display type) above the plan name in place of a feature checklist — but stop there. If the comparison needs more than one number per plan to make sense, this archetype has been outgrown; move to `card-catalogue-index`.

**cardOrListHeavy**: the native mode — `.lf-plan-features` stays a plain checklist (no sub-cards, no icons beyond the shared checkmark), and the featured plan's CTA (`.lf-plan-cta`) is the only one filled with `--lf-accent` rather than outlined.

## Medium Notes

`mediaAdaptation.markdown` is unusually strong for a marketing-family archetype: a plain feature-comparison table (rows = features, columns = plans) is markdown's native table syntax doing almost exactly this archetype's job, with the recommended column's header simply bolded or annotated.

## Pairing Notes

- **meridian-capital** — reach for this for premium/luxury positioning; its own hero already leans on overlapping metric cards and a single dominant accent, the same "one plan elevated" logic made literal.
- **solarpunk-utopia** — reach for this when the page's whole job is converting clicks; its pill-button and gradient-CTA convention is built for exactly a page with three buttons and one obviously-preferred choice.
- **vault-theorem** — reach for this for financial/wealth-management content; its own copy literally describes itself as a tiered framework, making genuine tiered-plan content its most natural home.
