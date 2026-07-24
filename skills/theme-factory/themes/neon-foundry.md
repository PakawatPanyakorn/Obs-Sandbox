# neon-foundry

Factory-floor precision meets retro-futurism — rust-fire orange against charcoal steel, with an explicit, functional color-to-meaning mapping (teal = data/success, yellow = warning) baked into the token schema itself.

## Core Concept
Near-black charcoal-steel canvas (`#0E1014`) with a fine orange-tinted 32px grid ("industrial blueprint feel"), Bebas Neue's all-caps condensed display against Barlow's clean sans body. Per `design.notes`, this theme has an unusually literal functional mapping: **secondary shares its hex with `success`** (`#00C8A0` teal = "data/success") and **accent shares its hex with `warning`** (`#FFD200` yellow = "warning/alert"). This isn't incidental — it means secondary and accent already carry semantic meaning beyond decoration, more like an instrument panel than a brand palette.

## Color Role Guidance

### primary (`#FF6B35` rust-fire orange)
- When to use: the theme's dominant "foundry fire" signal — primary buttons (`--gradient-button`), the strongest glow (`textShadow`, `--glow-lg`), headline gradient start.
- Surface area: generous — orange anchors the visual system throughout, from grid tint to glow to buttons.
- Don't: don't apply primary without its glow — every primary element in the preset carries `textShadow` or a glow shadow; a flat orange fill loses the "molten/fire" quality.

### secondary (`#00C8A0` electric teal) — also `success`
- When to use: per the theme's own convention, teal means "data" and "success" simultaneously — status-good indicators, secondary UI, data readouts.
- Surface area: moderate — a genuine cool counterpoint to orange, used for its functional meaning as much as its color.
- Don't: don't use teal for anything that isn't data/success-adjacent — its dual role as secondary AND success means introducing a separate "true success" color during harmonize would be redundant.

### accent (`#FFD200` industrial yellow) — also `warning`
- When to use: caution/alert signals specifically — accent and warning are the same hex, so any "accent" use should carry at least a hint of "pay attention" meaning.
- Surface area: small — hazard-stripe energy, not a general highlight.
- Don't: don't use accent for purely decorative emphasis unrelated to caution — its shared identity with warning means it always reads as "alert" to some degree.

## When To Use
- Industrial dashboards, manufacturing/factory-floor software, military/tactical UIs, or retro-futuristic sci-fi content wanting genuine mechanical precision.
- Data-dense technical products where teal-for-data-and-success and yellow-for-warning can be used as an actual functional status system, not just decoration.
- Dark-mode products wanting a warm "forge" glow instead of the more common cool neon-cyberpunk register.

## When NOT To Use
- Content without genuine status/data semantics — the secondary=success and accent=warning collapses are most valuable when there's real status data to color; without it, the theme is just "orange and teal."
- Warm, friendly, or approachable branding — `feel: instant`, sharp near-zero radii, and all-caps display type are deliberately blunt and mechanical.
- Light-mode contexts — no light variant; the entire effect depends on charcoal-steel darkness.

## How To Use — Full Potential
- Use secondary/teal specifically for both data readouts and success confirmations — leaning into the shared role (rather than inventing a separate green) is what makes the theme feel like a real instrument panel.
- Apply the fire-glow treatment (`textShadow: 0 0 20px rgba(255,107,53,0.5)`, `--glow-lg`) to primary headlines and key numerals — it's the theme's signature "molten metal" effect and should appear on the most important content, not just decoratively.
- Keep the fine orange grid visible at low opacity across the full page — it establishes the "industrial blueprint" register globally, not just in a hero section.
- If only one thing: apply the orange glow text-shadow to a Bebas Neue all-caps headline over the dark steel grid — the fastest way to signal neon-foundry.

## Apply-Mode Notes
- Step 4a: preserve the secondary=success and accent=warning collapses — don't introduce separate success/warning colors during harmonize; reuse secondary/accent exactly as the theme does.
- Step 4j: the fire-glow (text-shadow + glow shadows) on primary is structural, not optional — dropping it during harmonize is the most common way this theme collapses into a generic dark orange/teal theme.
