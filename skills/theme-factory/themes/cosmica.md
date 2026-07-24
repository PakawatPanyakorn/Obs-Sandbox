# cosmica

Deep-space maximalism as a literal mission-control aesthetic — 4-layer nebula gradient, frosted glass panels, and violet glow dominant enough to make Orbitron's all-caps sci-fi type feel earned rather than kitsch.

## Core Concept
Near-black space canvas (`#06041A`) under a 4-layer radial nebula mesh (violet, cyan, rose, deep-center falloff), Orbitron's geometric all-caps display against Exo 2's light-weight humanist body. `glassBlur: 16px` + `backdropFilter: blur(16px) saturate(180%)` give every panel genuine frosted-glass depth against the nebula, not just a dark card on a dark background. Per `design.notes`, "violet glow dominates" — rose/cyan exist explicitly as counterpoints, not co-equal partners (this is the pairing used with [[bento-mosaic]] in the layout-factory catalog for exactly this "mission-control tile board" register).

## Color Role Guidance

### primary (`#A855F7` cosmic violet)
- When to use: the dominant signal — hero gradients, primary buttons (`--gradient-button`, a 3-stop violet gradient), the strongest glow anywhere (`--glow-lg`, up to 96px spread).
- Surface area: large and confident — violet is meant to dominate visually, not restrained to small accents; hero backgrounds, primary CTAs, card borders (`0 0 0 1px rgba(168,85,247,*)` baked into every shadow level).
- Don't: don't apply primary without its glow — every violet surface in the preset carries a glow shadow or gradient; a flat violet fill loses the "cosmic energy" read.

### secondary (`#06B6D4` cyan)
- When to use: a cooler counterpoint inside the violet-dominant field — secondary UI, one gradient stop in `--gradient-text` (violet→cyan), alternate card accents.
- Surface area: deliberately smaller than primary — per the theme's own framing, this is a counterpoint color, not co-equal.
- Don't: don't scale cyan up to primary's visual weight — doing so would flatten the "violet dominates" hierarchy the whole theme is built around.

### accent (`#F43F5E` rose)
- When to use: the other counterpoint — `--gradient-accent` (violet→rose), error states, moments needing urgency against the cosmic calm.
- Surface area: small, sharp — a highlight or alert, not a large fill.
- Don't: don't treat rose and cyan as interchangeable "the other color" — rose reads as urgent/warm, cyan reads as cool/technical; pick per the specific counterpoint needed.

## When To Use
- Sci-fi, gaming, space/astronomy, or "mission control" analytics products — the theme's own layout-factory pairing (bento-mosaic dashboards) confirms it's built for tile-based data displays.
- Dark-mode products wanting maximal glass/glow density without tipping into pure neon-cyberpunk (that register belongs to more saturated/flat themes) — cosmica is soft-edged and diffuse, not hard-edged neon.
- Content that can sustain real backdrop-filter blur — panels are meant to look like they're floating over the nebula, not sitting on a flat dark background.

## When NOT To Use
- Content needing calm, grounded, or non-maximalist visual language — `hierarchyClarity: medium` (not high) and `personality: maximalist` mean this theme accepts some visual noise as part of its identity.
- Static/print or low-fidelity rendering contexts — `backdropFilter`, multi-layer glow, and the 4-layer nebula gradient all depend on real compositing; they degrade to a flat dark-purple background without it.
- Light-mode or daytime contexts — there is no light variant; the entire effect depends on near-black space.

## How To Use — Full Potential
- Lead with the hero's 3-stop gradient (`--gradient-hero: 135deg, #1A0A40 → #06041A → #0A0420`) plus a glass panel floating over it — this combination (dark gradient behind, frosted glass in front) is the theme's core "depth" trick.
- Use `--gradient-border` (violet→cyan→rose, all three colors together) sparingly, on the single most important panel per view — it's the one place all three chromatic roles appear together, so overusing it flattens the "violet dominates, others counterpoint" hierarchy.
- Reserve Orbitron all-caps for short labels/headlines only — Exo 2 body text at 300-weight is what keeps long-form content readable; all-caps Orbitron paragraphs would be both illegible and kitsch.
- If only one thing: apply `--glow-md` + `backdropFilter: blur(16px)` to a card — the fastest way to make a surface read as cosmica rather than a generic dark-purple theme.

## Apply-Mode Notes
- Step 4a: preserve the violet-dominant/cyan-rose-counterpoint hierarchy — don't apply the generic even-distribution color rule; violet should visually lead in any harmonized target.
- Step 4j: glass/glow effects are structural, not optional polish — `backdropFilter` and multi-layer glow are what separate this theme from a generic dark-mode purple theme; dropping them during harmonize is the most common failure mode.
