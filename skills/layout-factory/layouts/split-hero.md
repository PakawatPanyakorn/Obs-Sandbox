# split-hero

**Archetype:** split-hero · **Family:** grid-discipline

## Core Concept
The page is cut once, unevenly, into a fixed 60/40 zone — a dominant visual half and a secondary text/CTA half — where the asymmetry itself, not a badge or color change, signals which half is in charge. No third zone. The ratio is asserted in CSS (`3fr 2fr`) and never drifts toward 50/50 regardless of how much copy the text half eventually holds — copy is trimmed to fit the column, not the other way around.

## When To Use
- Personal essays/op-ed openers, long-form journalism cover spreads, editorial newsletter mastheads — content where a single strong sentence can stand in for a photograph.
- Investor one-pagers, single-finding executive summary covers, research announcement pages — anywhere one result needs to lead and everything else is secondary.
- Product launch pages with two or three SKU variants, pricing pages introducing 2-3 tiers under one hero, single-release changelog covers.

## When NOT To Use
- Content with enough copy that the text half would need its width back — if the visual zone would need to shrink to fit more text, this is the wrong archetype; reach for `magazine-well` or `two-column-academic` instead.
- Chart-heavy content wanting the content half to become a column of KPI tiles — a split-hero content zone carries at most one number, and it stays inside a sentence.
- Card/list content wanting to rebalance toward 50/50 to fit more items, or wrap each entry in its own card — both erase the asymmetry that reads as "one flagship, some supporting options" instead of a catalogue grid.

## Region / Component Guidance
- **lead** (~60%, `1 / 8`): the dominant visual half — image, exhibit, or a single oversized statement standing in for one. The only region that ever carries a shadow, gradient, or photographic pattern; fixed height regardless of variant.
- **body** (~40%, `8 / 13`): headline, one line of support, one action. Never widens to fit more copy. Carries at most one callout (a proof-point line beneath the CTA, or an eyebrow label above the headline).

## Content-Type Notes
- **textHeavy**: visual half's image is replaced by a single oversized typographic statement filling the same zone at the same dominant proportion — the ratio doesn't change just because there's no photograph. Content half keeps eyebrow, headline, one-sentence dek, CTA that reads as "keep reading" rather than "buy now."
- **chartHeavy**: visual half becomes the single largest captioned exhibit — a chart or map, never a decorative photo standing in for one. Content half leads with the finding as a headline sentence, then 2-3 short supporting readouts as a plain hairline-separated list, never a stat tile.
- **cardOrListHeavy**: visual half stays the flagship product/item image; content half's list of options stays a plain vertically-stacked list with hairline rules, sized by actual copy length — not a second grid of boxes competing with the split.

## Medium Notes
- Presentation: maps directly to a two-zone slide master — this is the shape the archetype is named for; visual anchor fills ~60% bleeding to one edge, text block occupies the remaining 40%, never centered over the visual.
- Print: facing-page spread — visual half becomes a full-bleed recto or verso page, text half becomes the facing page's inner column at the same width ratio; never printed as one centered page.
- Markdown: degrades to an H1 plus a short dek paragraph followed by a horizontal rule — markdown can't express side-by-side dominance, so the asymmetry has to be re-earned by giving the headline the only H1 on the page and keeping the dek to one sentence.

## Pairing Notes
- `meridian-capital` — its own hero already leans on one dominant visual move (skewed gold accent panel plus overlapping metric cards against a champagne gradient mesh); the same "one zone commands, everything supports" logic this archetype makes explicit.
- `neon-foundry` — built around a single commanding hero block (left accent bar, orange glow, dark grid canvas) that reads immediately as a product-launch visual anchor.
- `embassy-gold` — a restrained navy hero field with a gold top-rule and Cormorant display type reads as institutional cover-page authority, suited to a content half that persuades through type alone.
