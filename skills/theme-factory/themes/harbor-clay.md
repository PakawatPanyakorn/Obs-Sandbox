# harbor-clay

A deliberately corporate-editorial split-complementary pairing — deepened navy against desaturated terracotta clay, explicitly engineered to avoid reading as "craft-boho" despite using an earthy warm accent.

## Core Concept
Neutralized warm-paper canvas (`#F5F1E9`, desaturated from a more rustic cream specifically to read "cleaner, less rustic") with DM Serif Display headlines against Lora body. The color theory is explicit in the theme's own description: navy (~217°) and terracotta (~15°) are near-complements on the color wheel, chosen for professional tension rather than a matched analogous palette. Unusually, **the CTA/action color is secondary (terracotta), not primary (navy)** — `--gradient-button` and `glowColor` both use secondary; primary/navy anchors structure (hero gradient start, text) while secondary carries warmth and action.

## Color Role Guidance

### primary (`#3B4A63` deepened navy)
- When to use: structural authority — hero gradient's starting anchor (`--gradient-hero` runs navy→mid-blue→terracotta), headline text, the "serious" register of the split-complementary pair.
- Surface area: generous in structural/text contexts, but notably *not* the default button color — this theme reserves primary for gravitas, not action.
- Don't: don't default to primary for CTAs out of habit — this theme's own button gradient uses secondary/terracotta; putting navy on the main CTA understates the theme's actual warmth strategy.

### secondary (`#BF5F49` terracotta clay)
- When to use: the theme's real action color — `--gradient-button`, `glowColor`, `--shadow-colored` all key off secondary, not primary. This is the "warm, human, refined" half of the split-complementary pairing.
- Surface area: primary CTA surfaces, glow-bearing elements — secondary does more of the "interactive" visual work than a typical secondary role.
- Don't: don't treat secondary as a minor accent — in this theme it's functionally the primary *action* color even though it's named secondary in the token schema.

### accent (`#D98866` lighter terracotta)
- When to use: a lighter step of the same clay hue — gradient endpoints (`--gradient-text`, `--gradient-accent` both run terracotta→lighter-terracotta), hover states.
- Surface area: small — a tonal lightening of secondary, not a separate hue.
- Don't: don't treat accent as chromatically distinct from secondary — they're the same clay family at different values, reinforcing the split-complementary discipline (only 2 real hues: navy and clay).

## When To Use
- Professional services, editorial, or consultancy content wanting warmth without losing corporate credibility — the theme is explicitly engineered for this balance.
- Content where a typical navy-only corporate theme would feel too cold, but a full craft/boho terracotta theme would feel too casual — harbor-clay sits precisely between.
- Photographic imagery-driven content (`imageStyle: photographic`) — the refined, subtle glow and shadow system supports real photography well.

## When NOT To Use
- Content wanting a single dominant "brand navy" CTA color throughout — remember this theme puts action on terracotta, not navy; a target expecting navy buttons will need adjustment.
- Playful, youthful, or craft/artisan branding — despite the warm terracotta, the theme is explicitly *not* boho; it's corporate-editorial first.
- High-chroma or maximalist contexts — this is a controlled 2-hue split-complementary system; adding more saturated colors dilutes its careful color-theory balance.

## How To Use — Full Potential
- Use the 3-stop hero gradient (navy → mid-blue → terracotta) as the theme's signature move — it visually enacts the split-complementary relationship in a single element, more effective than using navy and terracotta in separate, disconnected places.
- Keep CTAs and glow-bearing interactive elements on secondary/terracotta, reserving primary/navy for headlines and structural chrome — this exact division is what makes the theme read as "warm but professional" rather than either extreme.
- Use the diagonal gradient border (`gradientBorder: terracotta → navy`) on cards/panels that should visually bridge both halves of the palette.
- If only one thing: apply the navy→terracotta hero gradient to a header or banner — it's the fastest way to demonstrate the theme's core color-theory idea in one glance.

## Apply-Mode Notes
- Step 4a: don't default the target's primary-button color to this theme's `primary` token — map CTAs to `secondary` (terracotta) instead, matching the theme's actual action-color convention, and use primary/navy for headings and structure.
- Step 4j: preserve the terracotta-keyed glow (`glowColor: #BF5F49`) on interactive elements — a navy glow would be visually incorrect for this theme despite navy being "primary" in the token name.
