# wisdom

Ancient Greek classicism — Platonic marble, Aegean lapis lazuli, and gold inscription, contemplative rather than ornamental, evoking philosophy-school gravitas over religious/institutional pomp.

## Core Concept
Warm Parian-marble parchment (`#F4EFE2`) with desaturated fractal-noise grain (`feColorMatrix saturate(0)` explicitly strips color from the noise to keep it reading as stone grain, not paper texture). Cinzel's carved-inscription capitals ("Cinzel columns") against EB Garamond's classical body ("EB Garamond scrolls"). The palette maps directly to materials: lapis-lazuli blue (primary), terracotta/sienna clay (secondary, literal pottery-color `#8B4513`), gold leaf inscription (accent) — `gradientBorder: linear-gradient(135deg, #B8860B, #1E3B6F, #B8860B)` (gold-blue-gold, symmetric) evokes an inscribed stone tablet's bordered edge.

## Color Role Guidance

### primary (`#1E3B6F` Aegean lapis lazuli)
- When to use: the "sky/sea" authority color — the hero's 3-stop blue gradient, primary buttons, structural headers. Lapis was historically among the most precious pigments (like ultramarine in [[vellum-codex]]), reserved for the most significant elements.
- Surface area: generous — this theme's primary carries real structural weight, appropriate for large use.
- Don't: don't soften primary with glow — `luminescence: none`; blue must read as painted/inscribed stone, not lit.

### secondary (`#8B4513` terracotta/sienna)
- When to use: the "pottery/earth" note — a warm, grounded counterpoint to the cooler lapis, evoking Greek amphora and terracotta artifacts.
- Surface area: moderate — a genuine second material reference, not just a color accent.
- Don't: don't treat secondary as decorative-only — it specifically references fired clay/pottery, so use it where an "artifact" or "vessel" association fits.

### accent (`#B8860B` gold inscription)
- When to use: the "carved and gilded" note — gradient text (`--gradient-text`, gold-dominant), the symmetric gold-blue-gold border, headline text-shadow (`0 1px 3px rgba(184,134,11,0.2)`).
- Surface area: small — inscription-style detailing, echoing gilded lettering on stone or gold leaf on manuscript capitals.
- Don't: don't confuse accent with `warning` (`#B07820`, a similar but distinct duller gold) — accent is ceremonial/inscriptive, warning is a genuine caution state.

## When To Use
- Philosophy, classics, academic, museum, or "timeless wisdom" content wanting genuine Hellenic classicism rather than generic "ancient" pastiche.
- Contemplative, scholarly editorial content benefiting from dignified restraint (`luminescence: none`, `glowBlur: 0`) over ornamental maximalism.
- Content that can carry Cinzel's carved-inscription display for headers and EB Garamond's classical serif for extended reading.

## When NOT To Use
- Playful, casual, or contemporary tech content — every choice (marble texture, inscription typography, muted palette) is deliberately ancient and formal.
- Content already using [[vellum-codex]] or [[embassy-gold]] in the same project — all three are gold-accented, blue-or-navy-primary, historically-inspired editorial themes; pick the one whose specific era/register (Hellenic vs. medieval-manuscript vs. corporate-Deco) actually fits.
- Content needing vibrant, saturated color — this is a muted, marble-desaturated palette throughout.

## How To Use — Full Potential
- Use the symmetric gold-blue-gold gradient border on ceremonial elements — pull quotes, section openings — echoing an inscribed tablet's bordered edge.
- Pair Cinzel headers with EB Garamond body consistently — the carved-inscription/classical-scroll contrast is what sells "Hellenic," not color alone.
- Keep the desaturated marble-grain noise texture visible across the full page — it's calibrated specifically to read as stone, not paper (unlike similar-looking parchment themes), via the explicit color-desaturation of the noise filter.
- If only one thing: apply the gold gradient text treatment with the symmetric gold-blue-gold border to a single headline — the fastest way to evoke an inscribed stone dedication.

## Apply-Mode Notes
- Step 4d/4j: zero glow/luminescence by design — this theme's richness comes from material reference (marble, lapis, gold) and typographic contrast, not light effects; don't add glow during harmonize.
- Step 4a: keep secondary/terracotta tied to "artifact/vessel" associations rather than general accent use, preserving the material-reference logic of the palette.
