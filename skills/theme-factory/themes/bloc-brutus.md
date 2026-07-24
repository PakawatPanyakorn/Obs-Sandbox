# bloc-brutus

Architecture as ideology — raw concrete gray, one harsh red, zero softening. Brutalism as a structural stance, not a texture applied on top of a normal theme.

## Core Concept
Concrete-gray canvas (`#D2CEC6`) with a faint architectural grid overlay (`patternType: grid`, blueprint feel), Anton's ultra-condensed heavy display face against Barlow body text. The theme's entire "3D" language comes from offset box-shadows (`4-12px, 0 blur`, `elevation: layered`) — there is no gradient, no glow, no border-radius anywhere (`gradients.*: none`, `effects.luminescence: none`, `borderRadius: 0px`). Secondary is near-black (`#1C1C1A`), not a hue — this palette has exactly one chromatic color (red) against concrete and near-black.

## Color Role Guidance

### primary (`#E8321A` harsh red)
- When to use: the theme's only real chromatic signal — primary CTA, the one accent that must not be missed. Per `design.notes`, "red as the only sharp contrast" — its power depends on staying singular.
- Surface area: small, sharp hits against the concrete field — a button, a rule, a single card's shadow tint (`--shadow-colored`).
- Don't: don't dilute red's exclusivity by introducing a second chromatic accent color elsewhere — this theme's confrontational effect depends on red being the *only* color that isn't gray/black/off-white.

### secondary (`#1C1C1A` near-black)
- When to use: structural text and high-contrast elements — headings, borders, the "ink" of the composition.
- Surface area: large — this is effectively the theme's second major tone alongside concrete gray, not a small accent.
- Don't: don't treat secondary as a "brand color" needing its own gradient or glow treatment — it's structural ink, meant to be flat and absolute.

### accent (`#F5B800` raw yellow)
- When to use: sparingly, for warning-adjacent or construction-signage-style emphasis (hazard-stripe energy) — a second-tier flag, not a co-equal brand color with red.
- Surface area: small — the theme's stated discipline is "red as the only sharp contrast," so accent should appear less often than primary, not at equal frequency.
- Don't: don't let accent and warning (`#C88800`) blur together in the same view — they're close in hue; use accent for compositional emphasis, warning strictly for caution states.

## When To Use
- Architecture, construction, civic/infrastructure content — the theme's own metaphor ("architecture as ideology") is literal, not decorative.
- Portfolios or products wanting deliberate confrontation and raw structural honesty over polish — anti-corporate, anti-soft positioning.
- Content that can carry heavy offset shadows and zero-radius geometry without needing rounded, friendly affordances anywhere.

## When NOT To Use
- Any warm, approachable, or consumer-friendly context — the theme is built to feel uncompromising, not welcoming.
- Content needing more than one strong chromatic accent — the whole effect depends on red staying singular against gray/black.
- Fast, springy interactions — `motion.easing: linear`, `feel: instant` is deliberately blunt, not delightful.

## How To Use — Full Potential
- Use offset box-shadows (`--shadow-md`, `--shadow-colored`) as the *only* elevation mechanism — never mix in blur-based soft shadows; the hard, blockish offset is what reads as "brutalist," not just "flat."
- Reserve the red-tinted shadow (`--shadow-colored: 6px 6px 0 #E8321A`) for exactly one element per view — the single most important action or callout — mirroring the "red as only sharp contrast" rule.
- Lean on Anton's extreme condensed weight for short, declarative headlines — the theme's typographic confrontation depends on brevity; long headlines in this face lose impact.
- If only one thing: apply a heavy offset shadow (`4-8px, 0 blur, gray`) to a bordered block — the single fastest move that reads as bloc-brutus rather than a generic light theme.

## Apply-Mode Notes
- Step 4a: keep red as the sole chromatic accent — don't introduce a second bright hue during harmonize even if the target file has multiple category/status needs; use secondary (near-black) and accent (yellow, sparingly) instead.
- Step 4d/4j: zero gradients, zero glow by design — any hero/colored-section harmonize step should use a flat color fill with an offset shadow, never a gradient or blur-based glow.
