# gilded-fracture

A bone-clay page split by one visible gold seam — the repair is the decoration, not something smoothed away.

## Core Concept

Gilded Fracture takes kintsugi literally as a layout principle: `.gf-seam` in the header and `.gf-section-title::after`'s short gold rule are the *same* gradient (`--gradient-seam`) reused at different scales, so the whole page reads as one clay object with a single consistent repair running through it, not a decorative motif scattered per-section. This is what separates **wabi-sabi/imperfect** from `edo-stillwater`'s **formal/restrained** register — edo-stillwater is about serene control, while this theme's whole premise is that the crack is the point, gold-lined and left visible rather than sanded down. The two-tone diagonal background split (barely a value shift, at 100deg) reads as an unevenly fired glaze — texture that's felt more than seen, so the gold seam has something quiet to interrupt.

## Color Role Guidance

### primary (#C9A227)
- When to use: the seam itself (`--gradient-seam`, used in `.gf-seam`, `.gf-section-title::after`, `.gf-card-seam`), the primary CTA button, and small tag/badge accents
- Surface area: intentionally thin — a 4-5px line and one button, never a fill. Gold's power here comes from scarcity against clay, matching the real kintsugi practice of a thin gilt line, not a gold panel
- Don't: use gold as a card or section background — that reads as generic "luxury gold" branding instead of a specific literal repair line

### secondary (#8FA593)
- When to use: the celadon glaze reference — kicker text color, secondary button, one badge
- Surface area: moderate — it's the "intact glaze" counterpart to the gold "repair," so it can appear more broadly than gold without breaking the concept
- Don't: use celadon for the gold seam's job (dividers/CTAs) — the theme's guidance only supports 2 fully chromatic roles (gold + celadon); accent below is a smaller third

### accent (#B5651D)
- When to use: sparingly — a "raw clay edge" callout, an alternate badge, never the seam itself
- Surface area: under 5% — this is a minor warm counterpoint to celadon's coolness, not a co-equal brand color
- Don't: place accent directly next to primary gold — both are warm/ochre-adjacent and will blur into each other; keep celadon between them when all three appear together

## When To Use
- Craft-restoration, ceramics, artisan-repair, or wabi-sabi philosophy content where "the piece kept its history visible" is the actual subject — the card set (Bowl No. 12, Tea Bowl, Vase Fragment Set) is built for exactly that inventory shape
- Contemplative literary/editorial content wanting warmth and quiet imperfection rather than `edo-stillwater`'s cooler formal restraint
- Long-session reading contexts — `Spectral` body serif and generous `spacious` density support extended reading, not quick scanning

## When NOT To Use
- Alongside `edo-stillwater` in the same project — both are quiet East-Asian-adjacent editorial registers and will read as the same theme from a distance
- Fast-interaction dashboards or transactional UI — the `subtle` motion feel (320ms base, no bounce) and hairline borders are built for contemplation, not rapid task completion
- Content with 4+ genuinely equal chromatic roles — this palette only supports 2 full roles (gold, celadon) plus one minor accent; forcing a 4-way split flattens the "one repair, one intact glaze" concept

## How To Use — Full Potential
- Lead with `.gf-seam` in the header exactly as built — a single rotated gold gradient line crossing the hero, not multiple seams scattered around the page. One crack, not a shattered plate.
- Reuse `--gradient-seam` (not a flat gold hex) anywhere gold appears — the three-stop gradient (`#C9A227 → #E8C565 → #C9A227 → #A6811D`) is what makes it read as dimensional lacquer-and-leaf rather than a flat mustard-gold brand color
- If you only do one thing: add a `.gf-card-seam` (a 2px, 36px-wide gold-gradient bar) to the bottom of any card — it's the fastest way to make an unrelated component read as unmistakably Gilded Fracture

## Apply-Mode Notes
- Step 4a's primary-dominance check needs an unusual reading here: primary (gold) should stay under ~5% of viewport even though it's the theme's signature color — this is the one theme where "more gold" directly weakens the concept rather than strengthening brand presence.
- Step 4j (italic-headline check from the anti-pattern gate) matters more than usual for this theme specifically — the source concept leans toward italic serif headings, but headings must stay roman (`font-style: normal`) with italic reserved only for the single kicker/caption line (`.gf-kicker`), never on every header.
- Skip glow/glass harmonization entirely — `effects.glassBlur`, `glowBlur`, and all glow shadows are `0`/`none` by design; the only "effect" this theme has is the seam gradient itself.
