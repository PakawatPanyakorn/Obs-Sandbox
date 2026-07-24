# amber-signal

Total monochrome CRT phosphor — a single wavelength of amber light against near-black, evoking a clandestine shortwave radio station rather than a modern screen.

## Core Concept
Near-black canvas (`#0A0800`) with high-frequency SVG noise grain (`background.patternType: noise`, `noiseOpacity: 0.04`) simulating analogue screen burn. Every color in the palette lives on the amber/orange hue wheel except `success` (a desaturated olive, "Clear") and `error` (a red "Alarm") — this is the one theme in the catalog where breaking monochrome is reserved *exclusively* for genuine alert states. Poiret One's thin geometric letterforms (`.as-display`, `.as-h2/h3`) paired with heavy letter-spacing (`0.08–0.1em`) evoke deco-radio dial typography.

## Color Role Guidance

### primary (`#FF9D00`)
- When to use: the "live" signal — primary CTA (`.as-btn-primary`), the on-air badge (`.as-badge-primary`), signal-strength bars (`.as-signal-bar span`). Reads as "actively transmitting."
- Surface area: buttons, glow-bearing elements — this theme wants primary to carry `--glow-sm`/`--glow-md`/`text-shadow` wherever it appears; a shadowless flat primary fill undersells the phosphor conceit.
- Don't: don't use primary for static/structural chrome (borders, dividers) — that's `border`/`textMuted`'s job; primary is reserved for things that are "on."

### secondary (`#C87010` dark amber)
- When to use: a dimmer, non-glowing echo of primary — secondary buttons (`.as-btn-secondary`), the "Encrypted" badge, anything that should read as amber but subdued/inactive.
- Surface area: outlines and muted fills — this theme deliberately withholds glow from secondary, so it stays visually one tier below primary.
- Don't: don't give secondary a glow/text-shadow — that would collapse the primary/secondary distinction, which here is "glowing vs. not," not just "lighter vs. darker."

### accent (`#FFD040` bright amber)
- When to use: the brightest phosphor moment — gradient text stops (`--gradient-text`), card tags (`.as-card-tag`), mono readouts (`.as-mono`). It's primary's "hot" register.
- Surface area: small text accents and gradient highlights, not fills — accent never appears as a background color anywhere in the preset.
- Don't: don't introduce accent as a fourth independent hue; like primary/secondary, it exists purely as a brightness step within the same amber wavelength.

## When To Use
- Retro-terminal, radio/signal, or dieselpunk-adjacent products — the theme's own demo content ("underground radio station," "shortwave relay," Morse/SSB channel cards) names its genre directly.
- Any dark-mode surface that wants a genuinely distinctive glow treatment beyond the generic "dark mode with a blue accent" default.
- Content with real telemetry/status data (frequency, RSSI, signal strength) that benefits from the mono readout style (`.as-mono`) and signal-bar visualization.

## When NOT To Use
- Anything requiring more than 2-3 distinguishable categorical colors — the palette is intentionally monochrome outside of success/error; a taxonomy needing 4+ hues has nowhere to go without breaking the theme's core premise.
- Bright, daytime, or optimistic contexts — the theme is built entirely around a dark screen and phosphor glow; there's no light-mode variant to fall back to.
- Content-dense reading surfaces — `noiseOpacity` grain and heavy letter-spacing display type are tuned for short transmission-log-style copy, not long paragraphs.

## How To Use — Full Potential
- Lead with `.as-header`'s combination: gradient hero background + `text-shadow: var(--glow-md)` on the h1 + the animated-looking `.as-signal-bar` — this trio is what makes a page read as a live transmission rather than a static dark theme.
- Use `.as-card:hover { box-shadow: var(--shadow-colored) }` — the glow-on-hover interaction is a theme-native affordance that should be preserved on any card/interactive surface, not flattened to a generic hover state.
- Keep `.as-mono` (accent-colored, glow-bearing monospace) for any live-data readout — it's the theme's dedicated "instrument reading" style and is what differentiates real telemetry from ordinary body text.
- If only one thing: apply `text-shadow: var(--glow-sm)` to a headline in Poiret One — the thin geometric face plus soft amber glow is the fastest single move that reads as amber-signal.

## Apply-Mode Notes
- Step 4a's generic color-distribution rule doesn't map cleanly here — treat `primary`/`secondary`/`accent` as three brightness steps of one hue, not three independent roles; the only genuine second/third hue in the palette is reserved for `success`/`error` status states.
- Step 4j (gradients/glow/effects): glow is structural to this theme, not optional — every `primary`-colored interactive element in the source presets carries a glow or text-shadow; dropping it during harmonize is the most common way this theme ends up looking like a generic dark theme with orange accents.
