# darkroom-safelight

A working photographic darkroom under safelight — content "develops" out of deep red ambient darkness the way an image emerges in a chemical bath, with zero color anywhere except the chemistry itself.

## Core Concept
Deep safelight-red near-black canvas (`#160404`, "simulates darkroom ambient under Kodak OC filter") with silver-halide off-white as the dominant text/foreground tone. This theme inverts the usual role assignment: **primary is the light "developed" tone** (`#D4CCC0`), not a saturated brand hue — it's what content looks like once it exists, while **secondary carries the red** (`#8B2020`), representing the ambient safelight itself. `gradients.*` are entirely `none` and `luminescence: none` — this theme is genuinely photochemical in restraint, not just "dark and red."

## Color Role Guidance

### primary (`#D4CCC0` silver-halide white)
- When to use: this is the "image has developed" signal — primary text, primary buttons, anything that should read as fully resolved/present against the red darkness. Unlike most themes, primary here is a near-neutral, not a saturated hue.
- Surface area: body text, headlines, resolved UI elements — generous, since this is functionally the theme's main foreground tone.
- Don't: don't treat primary as a "bold accent" the way most themes do — it's meant to feel neutral and photographic, like a print, not vibrant.

### secondary (`#8B2020` safelight red)
- When to use: the ambient/atmospheric color — glow shadows (`--shadow-colored`, `--glow-*` all use this red), borders, anything meant to feel like it's still bathed in the darkroom's red light rather than fully resolved.
- Surface area: structural — borders, glow, ambient ring shadows (`0 0 0 1px #3A1010` border pattern) — this is effectively the theme's "atmosphere" color, doing more surface-area work than usual for a "secondary."
- Don't: don't demote secondary to a minor accent — it's doing the job most themes give primary (setting the overall visual mood); pairs with primary's white as the theme's core duality (developed vs. still-developing).

### accent (`#B87722` chemical amber/warning gold)
- When to use: shares its hex with `warning` — genuine caution states, or a specific "chemical process" marker (timer warnings, fixer-stage indicators) if the content has a literal darkroom-process narrative.
- Surface area: small — a specific process marker, not a general highlight.
- Don't: don't use accent as a generic third brand color — its meaning is tied to caution/chemistry, not decoration.

## When To Use
- Photography portfolios, film/analog culture content, darkroom or archival-process storytelling — the theme's own vocabulary (frame numbers, contact-sheet layout) is built for exactly this.
- Content wanting a genuinely restrained, monochrome-plus-one-hue dark theme distinct from generic "dark mode with red accent."
- Editorial content that benefits from a "developing/emerging" visual metaphor — reveal-style interactions, before/after content.

## When NOT To Use
- Any content needing a conventional primary/secondary/accent hierarchy where primary is the "bold brand color" — this theme's inverted assignment (primary = neutral, secondary = the saturated hue) will surprise anyone expecting the usual convention.
- Bright, colorful, or maximalist content — `gradients: none`, `luminescence: none`, and a near-monochrome-plus-red palette make this one of the most restrained dark themes in the catalog.
- Fast-paced, high-density UI — `density: compact` but `motion.feel: subtle` and zero decorative effects mean the theme relies entirely on typographic/layout precision, not visual flourish, to feel considered.

## How To Use — Full Potential
- Use the contact-sheet/frame-number vocabulary literally where possible — numbered frames, film-strip layout metaphors reinforce the theme's photographic premise more than generic cards would.
- Reserve the red glow (`--glow-md`/`--glow-lg`) for elements that should feel "still in the chemical bath" — actively processing/pending states — while fully resolved content stays in plain silver-halide white with no glow.
- Pair DM Serif Display (headlines) with IBM Plex Mono (everything else, including body) — the serif/mono contrast plus the theme's photographic restraint together read as "archival documentation," not generic editorial.
- If only one thing: set body copy in silver-halide white against the deep safelight-red background with zero additional color — the starkness alone signals darkroom-safelight.

## Apply-Mode Notes
- Step 4a: do NOT apply the generic "primary = brand/bold color" assumption — in this theme primary is the neutral/resolved tone and secondary carries the saturated hue; harmonizing a target's "primary button" to this theme's primary is correct even though it looks understated.
- Step 4d/4j: zero gradients and zero luminescence by design — any hero/colored-section harmonize should stay flat, with red-tinted borders/glow as the only "effect," never a gradient fill.
