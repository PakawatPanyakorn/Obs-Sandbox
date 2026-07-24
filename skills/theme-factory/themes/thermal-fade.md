# thermal-fade

An end-of-roll BPA receipt, rendered with the one gimmick that defines it: content physically fades to blank as it approaches the footer, exactly as thermal ink runs out on a real receipt.

## Core Concept
Warm off-white thermal-paper canvas (`#FFF8EE`) with subtle noise texture, Courier Prime monospace for every font role (body, mono, AND display — a receipt has one typeface). The theme's entire identity is one CSS mask: `mask-image: linear-gradient(to bottom, black 0%, black 60%, rgba(0,0,0,0.6) 78%, rgba(0,0,0,0.25) 90%, rgba(0,0,0,0.05) 100%)` applied to the body — content renders crisp for the first 60% of the page, then genuinely fades toward near-invisibility by the footer. Per `design.notes`: "THE gimmick." Everything else (dashed perforation-style separators, a date/time stamp header) supports this one central effect.

## Color Role Guidance

### primary (`#1A1A0A` near-black thermal ink)
- When to use: this is the "fresh ink" tone — headlines, primary text, buttons. Like `darkroom-safelight` and `prussian-blueprint`, primary here is a neutral ink color, not a saturated brand hue.
- Surface area: generous at the top of the page, fading naturally via the mask toward the bottom — don't fight the fade by reinforcing primary's opacity manually further down.
- Don't: don't treat primary as needing a "bold" saturated alternative — thermal ink is genuinely just dark, near-black; the fade effect does the emotional work, not color choice.

### secondary (`#666650` faded olive-gray)
- When to use: already-slightly-faded text, secondary information, metadata — it reads as "one step toward the fade" even before the mask is applied.
- Surface area: moderate — supporting text, timestamps, receipt line-item detail.
- Don't: don't use secondary for content that should read as "fresh" — reserve full-strength primary for that.

### accent (`#AA7700` thermal amber)
- When to use: a specific "stamped" mark — the date/time stamp header, a rare highlight evoking a rubber date-stamp on real receipt paper.
- Surface area: small — a stamp or single flagged line item, not general emphasis.
- Don't: don't overuse accent — its value depends on evoking a specific physical mark (ink stamp), not serving as a general highlight color.

## When To Use
- Receipt, transaction-log, order-confirmation, or "this content has an expiration/decay" narrative content — the fade literally communicates ephemerality.
- Playful editorial or storytelling content wanting a genuinely novel scroll-based reveal/decay effect.
- Content where a footer naturally being de-emphasized (fine print, terms, low-priority metadata) is desirable — the fade does this automatically.

## When NOT To Use
- Any content where footer information must remain fully legible — the mask genuinely reduces opacity to near-zero; critical actions/links must not live in the faded zone.
- Long-scrolling content with important material throughout — the fade is calibrated for a single-viewport-ish "receipt" length; stretching it over a very long page either fades too early or never engages.
- Accessibility-sensitive contexts — near-invisible text by design conflicts with contrast/legibility requirements; use with explicit awareness of this tradeoff.

## How To Use — Full Potential
- Keep the mask-gradient fade as a body-level effect, not confined to a card or section — the "whole receipt runs out of ink" read depends on it applying globally.
- Use monospace for literally everything, including headings — a receipt has no separate display face, and introducing one would break the authenticity.
- Place the most important content (total, confirmation number, primary CTA) within the first 60% of the page where the mask keeps full opacity — never place critical actions in the faded zone.
- If only one thing: apply the exact 5-stop mask gradient to a page's body content — it's the single, complete signature of thermal-fade; there's no smaller unit that captures it.

## Apply-Mode Notes
- Step 4a: primary is neutral ink, not a bold brand color — don't introduce a saturated "primary" color during harmonize; the fade effect, not color, carries the theme's identity.
- Step 4j: the mask-image fade is the theme's single structural effect — preserve it exactly (same gradient stops) rather than approximating with a simple opacity fade, and verify no critical content/actions fall in the faded zone below 60%.
