# dead-letter-office

Mid-century US Postal Service undeliverable mail as a literal UI system — cards ARE envelopes, badges ARE rubber ink stamps, and the whole page reads as manila kraft paper under a typewriter.

## Core Concept
Manila-envelope kraft canvas (`#D8CC94`) with fine noise grain, Special Elite's genuine typewriter-strike face for body/mono and Libre Baskerville serif for display. The metaphor is total: cards are `.envelope-card` elements with `.postal-stamp` floating top-right and diagonal airmail-stripe corners; badges are `.rubber-stamp` elements, individually rotated a degree or two off-axis (`transform: rotate(1deg)`) to fake a hand-stamped imperfection. Unusually, `border: #1B3A8B` reuses secondary's postal-blue directly as the universal border color, not a neutral gray — every rule and envelope edge is "airmail blue," not generic gray.

## Color Role Guidance

### primary (`#CC1122` postal red) — shares hex with `error`
- When to use: urgent/undeliverable states — "RETURN TO SENDER" stamps, primary buttons, anything meant to read as officially flagged. Primary and error intentionally share one hex.
- Surface area: stamps, buttons, accent ink — small deliberate marks against the kraft field, like real rubber-stamp ink, not large fills.
- Don't: don't treat primary as a neutral "brand" color separate from urgency — in this theme, red always carries an "attention/problem" connotation even when used as primary.

### secondary (`#1B3A8B` airmail blue) — also the universal `border` color
- When to use: structural, not just accent — every border, rule, and airmail stripe in the theme uses this exact blue; it's doing the job most themes give a neutral gray.
- Surface area: large — borders, dividers, stripe patterns throughout, not a minor highlight.
- Don't: don't replace secondary-as-border with a neutral gray during any edit — the postal-blue border is a defining, deliberate choice, not an oversight to "fix" toward convention.

### accent (`#6A4A8B` official-purple)
- When to use: a third, rarer ink color — official stamps/seals, a "processed by a different department" signal distinct from red urgency or blue structure.
- Surface area: small — the least-used of the three chromatic roles, reserved for a specific "official" register.
- Don't: don't use accent as a generic highlight color — its scarcity and specific "purple ink stamp" connotation should be preserved.

## When To Use
- Archival, bureaucratic, retro-Americana, or postal/logistics-themed content — the theme's literal metaphor (envelopes, stamps, route codes) rewards genuine mail/document-tracking use cases.
- Status-heavy content where "rubber stamp" badges (RECEIVED/PENDING/RETURN TO SENDER/FORWARDED/DELIVERED) map naturally onto real states — support tickets, shipment tracking, application/document workflows.
- Content wanting warm, tactile, analog nostalgia rather than digital-native chrome.

## When NOT To Use
- Modern, clean, tech-forward products — every element of this theme (kraft paper, typewriter face, hand-stamped rotation) actively resists a polished digital read.
- Content without any status/tracking dimension — the rubber-stamp badge system is the theme's centerpiece; without genuine states to stamp, it has little to do.
- Long-form reading — Special Elite's typewriter face is characterful but has poor extended readability; reserve it for short labels/body copy, not dense paragraphs.

## How To Use — Full Potential
- Use `.envelope-card` as the default card treatment, not a special case — the postal-stamp-in-corner + airmail-stripe-corner combination is the theme's signature and should be the norm, not an occasional flourish.
- Apply the rubber-stamp badge pattern (`.rubber-stamp`, individually rotated a degree or two) to every status/tag element — the slight per-instance rotation is what sells "hand-stamped" over "printed label"; keep badges un-rotated and it reads as a generic UI kit instead.
- Reuse secondary blue as the universal border/rule color everywhere, never falling back to a neutral gray — consistency here is what makes the postal metaphor cohesive rather than spot-decorated.
- If only one thing: apply a rotated rubber-stamp badge with postal-red ink to a status label — the single fastest, most recognizable signal of dead-letter-office.

## Apply-Mode Notes
- Step 4a: preserve secondary-as-border — don't remap borders to a neutral gray during harmonize; the postal-blue border is load-bearing for the theme's identity.
- Step 4f (JS/SVG hardcoded colors) / general badge harmonize: any status/tag component should become a rotated rubber-stamp treatment, not a standard pill badge — flat, unrotated badges undersell this theme significantly.
