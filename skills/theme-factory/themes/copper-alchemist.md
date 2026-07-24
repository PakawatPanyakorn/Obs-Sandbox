# copper-alchemist

Victorian steampunk forge-light — copper, verdigris patina, and burnished gold rendered with genuine metallurgical logic, not just "brass and gears" pastiche.

## Core Concept
Near-black forge-brown canvas (`#160E08`) under a diagonal crosshatch lattice (`patternType: grid`, "wrought iron grating over forge darkness"), Josefin Slab's geometric slab-serif display paired with Lora's classical body serif for "Victorian precision." The triad is materially motivated: copper (primary, the base metal), verdigris teal (secondary, copper's oxidized patina), burnished gold (accent, the alchemical "refined" state) — `--gradient-accent` runs copper→verdigris directly, visualizing the oxidation process itself.

## Color Role Guidance

### primary (`#C87830` copper)
- When to use: the "raw metal" — primary buttons (`--gradient-button`, a copper-toned gradient), hero backgrounds, the base material state before transformation.
- Surface area: generous — copper is the theme's base tone, appropriate for buttons, borders, and structural accents throughout.
- Don't: don't render primary as a cold flat fill — every primary surface carries a subtle gradient or warm glow (`textShadow: 0 0 24px rgba(200,120,48,0.35)`); flattening it loses the "forge-warm metal" quality.

### secondary (`#4A9090` verdigris)
- When to use: the "aged/transformed" state — secondary buttons, anything meant to read as time-worn or chemically altered rather than freshly forged.
- Surface area: moderate — a deliberate cool counterpoint to the warm copper/gold pair; don't let it dominate, since the theme's overall temperature is warm.
- Don't: don't use verdigris as if it were a generic teal/cyan — its role is specifically "oxidized copper," so pair it visually near copper (shared gradients, adjacent swatches) rather than isolating it as an unrelated cool accent.

### accent (`#E8B840` burnished gold)
- When to use: the "refined/alchemical" end-state — highlights, the brightest text moments, gradient endpoints (`--gradient-text` runs gold→copper→dark-copper).
- Surface area: small, precious — gold should feel earned/rare within a composition, the payoff at the end of the copper→gold visual narrative.
- Don't: don't use gold and warning interchangeably even though they're visually adjacent — `warning` reuses primary's copper (`#C87830`), while accent gold is reserved for genuine "refined" emphasis, not caution.

## When To Use
- Steampunk, alchemy, artisan-craft, or Victorian-industrial content — the theme's material logic (copper/patina/gold) rewards genuine craft narratives.
- Dark-mode products wanting warmth without going neon — the forge-glow register (`glowLg`, warm text-shadow) sits between "cozy" and "industrial."
- Content that can sustain illustrative imagery (`imageStyle: illustrative`) — the theme pairs naturally with engraved/etched-style visuals.

## When NOT To Use
- Cold, clinical, or futuristic-tech content — the entire palette is warm and material; there's no cool/neon register to fall back on.
- Fast-paced, high-frequency UI — `motion.feel: subtle`, `durationSlow: 380ms` is tuned for deliberate, weighty interactions, not snappy feedback.
- Content needing a clean, neutral base color — even `surface`/`surfaceAlt` here carry warm brown undertones; a design needing true neutral gray will fight this palette.

## How To Use — Full Potential
- Use the copper→verdigris→gold gradient sequence (`--gradient-accent`, `--gradient-text`) as a literal narrative device — introduce copper first, transform to verdigris or resolve to gold to signal a state change (e.g., "before/after," "raw/refined").
- Lead with the hero's three-stop dark gradient (`--gradient-hero: 160deg, #261A0A → #160E08 → #120A04`) — this subtle brown-to-black falloff is what makes the background feel like it recedes into forge-darkness rather than reading as flat black.
- Pair Josefin Slab (display) with Lora (body) consistently — the slab-serif/humanist-serif contrast is what sells "Victorian precision" per the theme's own notes; substituting either font for a sans-serif breaks the register.
- If only one thing: apply the warm copper text-shadow (`0 0 24px rgba(200,120,48,0.35)`) to a headline — the fastest way to make a page feel forge-lit rather than merely dark brown.

## Apply-Mode Notes
- Step 4a: preserve the material narrative — map primary/secondary/accent to raw/aged/refined states wherever the target content has any before/after or state-transition data, rather than a generic brand-hierarchy split.
- Step 4j: the warm glow and gradient treatments are load-bearing for the "forge" read — flattening them during harmonize is the most common way this theme collapses into a generic brown dark-mode theme.
