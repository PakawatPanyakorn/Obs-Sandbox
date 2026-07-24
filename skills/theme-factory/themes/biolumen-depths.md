# biolumen-depths

Midnight-zone bioluminescence rendered with scientific restraint — "field log meets alien wilderness," where every glow is grounded in a real deep-sea phenomenon rather than generic sci-fi neon.

## Core Concept
Absolute ocean-black canvas (`#020d1a`) pierced by three scientifically-motivated light sources: teal (organism bioluminescent core), cold blue (pressure-depth light scatter), and amber (dinoflagellate flash) — the palette is a deliberate metaphor map, not an arbitrary triad. A sonar-ring background (`patternType: sonar-rings`, concentric depth-contour rings from a bottom-left focal point) plus fractal noise grain reinforces the "field instrument" read (`.tf-sonar-demo`, `.tf-header-depth`). `glassBlur: 12px` and `backdropFilter: blur(12px) saturate(150%)` give surfaces genuine depth-refraction, distinct from a flat dark theme.

## Color Role Guidance

### primary (`#00e5c8` bioluminescent teal)
- When to use: the "organism core" — primary buttons (`--gradient-button`, a teal gradient not a flat fill), the strongest glow anywhere on the page (`--glow-lg`), depth-marker labels (`.tf-header-depth`).
- Surface area: small, intense glow sources — this color is meant to look like it's *emitting* light against total darkness, not filling large surfaces.
- Don't: don't apply primary as a large flat background fill — every primary application in the preset carries glow/gradient; a flat teal panel loses the "creature glow" metaphor entirely.

### secondary (`#1e8fff` pressure-depth blue)
- When to use: ambient/atmospheric light scatter — background bloom, gradient-border pairing with primary (`--gradient-border: linear-gradient(135deg, #00e5c8, #1e8fff)`), cooler secondary UI accents.
- Surface area: diffuse, soft — reads as scattered ambient light, not a direct source like primary.
- Don't: don't give secondary the same intensity of glow as primary — it's "depth scatter," inherently softer and more diffuse by the theme's own physical metaphor.

### accent (`#ff8c42` dinoflagellate amber)
- When to use: the rare "flash" moment — a single alert, a highlighted data point, anything meant to read as a sudden, momentary bioluminescent flash against the teal/blue field.
- Surface area: small and infrequent — amber's entire value depends on scarcity; overusing it turns "flash" into "third brand color."
- Don't: don't use accent for routine UI (buttons, badges) at the same frequency as primary — it should feel like an event, not a palette member in regular rotation.

## When To Use
- Scientific/research dashboards, deep-sea or space-exploration content, "field instrument" data products wanting a haunting, alien-but-grounded register.
- Dark-mode data visualization where glow can carry real meaning (signal strength, activity, depth) rather than being purely decorative.
- Content that benefits from glassmorphic surfaces (`backdropFilter: blur(12px)`) over pure-black panels — cards read as suspended in water, not stacked flat.

## When NOT To Use
- Warm, human, or approachable contexts — the theme is built entirely around cold, alien darkness; there's no accessible "light mode" variant.
- Content needing 4+ evenly-weighted categorical colors — accent's whole effect depends on rarity; a taxonomy that uses amber as often as teal collapses the "flash vs. ambient" distinction.
- Static/print output — glassmorphic blur and multi-layer glow shadows depend on real compositing; they degrade to plain flat panels without it.

## How To Use — Full Potential
- Lead with the sonar-ring background + noise grain combination — this exact pairing (`patternType: sonar-rings` + `noiseOpacity: 0.04`) is what separates this theme from a generic dark-teal theme; a flat solid background loses the "scientific instrument" read.
- Use `--glow-lg`'s triple-layer glow (`0 0 32px / 64px / 100px`, decreasing opacity) on the single most important element per view — it's tuned to read as bioluminescent falloff, not a generic drop shadow.
- Reserve `--gradient-border` (teal→blue) for card/panel edges that should read as "lit from within" — paired with `glassTint: rgba(0,229,200,0.04)`, it's the theme's signature "underwater glass" panel treatment.
- If only one thing: apply `--glow-md` to a primary-colored label against the dark background — the fastest way to make an element read as bioluminescent rather than merely teal.

## Apply-Mode Notes
- Step 4a: accent must stay rare by design — don't let harmonize distribute accent evenly across a taxonomy; reserve it for genuine "flash" moments (alerts, single highlighted values) even if the target file has several categorical states.
- Step 4j: glass/glow effects are structural here (`glassBlur`, `backdropFilter`, multi-layer `--glow-*`) — dropping them during harmonize is the most common way this theme collapses into a generic flat dark theme with teal accents.
