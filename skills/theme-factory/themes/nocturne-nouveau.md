# nocturne-nouveau

Art Nouveau's organic floral palette (gold, teal, rose, violet) rendered on deep midnight indigo — sensuous color married to sharp, unrounded geometry, a deliberate tension rather than a soft cottagecore read.

## Core Concept
Deep midnight-indigo canvas (`#0A0818`) under a 4-layer organic radial gradient — gold, teal, rose, violet, "Art Nouveau floral colour palette on deep midnight indigo." Italiana's elegant condensed display against Fraunces' optical-size serif body. The theme's defining tension: despite `personality: ornate, sensuous` and a lush multi-hue background, `borderRadius/cardRadius/buttonRadius` are all `0px` — every panel is sharp-cornered, giving the floral palette a stained-glass/leaded-window structure rather than a soft, rounded "pretty" read.

## Color Role Guidance

### primary (`#D4A840` warm gold)
- When to use: the dominant "gilt" tone — primary buttons (`--gradient-button`, gold gradient), headline text-shadow glow (`0 0 30px rgba(212,168,64,0.4)`), the largest layer in the background mesh.
- Surface area: generous — gold leads the visual hierarchy throughout, appropriate for large use, not just accents.
- Don't: don't apply gold without its glow — `textShadow` and glow shadows are present on every primary use; a flat gold fill loses the "nocturnal gilt" quality.

### secondary (`#2A8888` aqua-teal)
- When to use: a cool counterpoint inside the warm-dominant palette — secondary buttons, one background mesh layer, the middle stop in the 3-color gradient border.
- Surface area: moderate — a genuine second voice, cooler and calmer against gold's warmth.
- Don't: don't let teal dominate — the theme's overall temperature is warm (gold-led); teal should read as a jewel-tone accent, not compete for lead position.

### accent (`#E8604A` rose-coral)
- When to use: the "floral bloom" note — gradient endpoint (`--gradient-accent`, gold→rose), the third background mesh layer, a warm-but-distinct highlight from gold.
- Surface area: small — a bloom of color against the indigo dark, not a large fill.
- Don't: don't confuse accent-rose with `error` (`#D04040`, a more saturated red) — accent is decorative warmth, error is a genuine failure state.

## When To Use
- Luxury, fashion, perfume/beauty, or fin-de-siècle-inspired editorial content — the theme's genuine Art Nouveau floral-on-midnight register rewards sensuous, indulgent content.
- Dark-mode products wanting warmth and ornament without softness — the sharp-cornered geometry keeps it from reading as twee or overly decorative.
- Content that can sustain generous whitespace (`density: spacious`) and dramatic elevation (`elevation: dramatic`) — this is not a compact, information-dense theme.

## When NOT To Use
- Soft, rounded, approachable branding — the zero-radius geometry is a deliberate counterpoint to the ornate palette; rounding corners during any edit undoes the theme's core tension.
- Minimalist or restrained content — 4-layer gradient mesh, 3-color gradient border, and generous glow are inherently maximalist.
- Fast, information-dense UI — `density: spacious`, `motion.feel: expressive`, `durationSlow: 500ms` are tuned for indulgent pacing, not efficiency.

## How To Use — Full Potential
- Keep every corner sharp (0px radius) even as the color palette goes lush and organic — this contrast (geometric frame, floral content) is the theme's most distinctive and easily-lost trait.
- Lead with the 4-layer radial gradient mesh as a body-level background — the "Art Nouveau floral palette on midnight" effect depends on all four hues (gold, teal, rose, violet) being visible together, not isolated to a hero.
- Reserve the 3-color gradient border (gold→teal→rose) for a single ornamental frame per view — a jewelry-box or vitrine effect that loses specialness if applied broadly.
- If only one thing: apply gold's glow text-shadow to an Italiana headline against the indigo background — the fastest way to signal nocturnal, gilded Art Nouveau.

## Apply-Mode Notes
- Step 4c (shape): preserve zero border-radius throughout — do not soften corners even where the target file's original design used rounded elements; the sharp/ornate contrast is structural to this theme.
- Step 4j: the 4-layer gradient mesh and gold glow are load-bearing — dropping either during harmonize collapses the theme into generic dark-purple-with-gold-accent.
