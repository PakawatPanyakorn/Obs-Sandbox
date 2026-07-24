# titanium-cloud

Enterprise developer-platform SaaS design — a genuinely modern product-blue/violet/teal system on cool off-white, engineered to feel like a real platform's marketing site, not a generic "corporate blue" template.

## Core Concept
Ice-white canvas (`#F6F8FA`) with a fine 32px cool-gray grid ("engineering graph paper / product blueprint"). The theme's own notes specifically distinguish its gray from a blue-tinted alternative — this is a deliberately *neutral* cool gray, not a blue-cast gray, keeping the grid from competing with the product-blue primary. Outfit's clean geometric display against Figtree's humanist body is the modern-SaaS-standard font pairing. `luminescence: none`, `glowBlur: 0` — despite being a "product design" theme, it has zero glow; polish comes from soft layered shadows (`shadows.elevation: subtle`) and a subtle hero gradient, not luminescence.

## Color Role Guidance

### primary (`#2563EB` product blue)
- When to use: the platform's core brand action — primary buttons (`--gradient-button`, blue gradient), the dominant hue in the hero gradient, gradient-border pairing.
- Surface area: generous — standard SaaS-primary usage, appropriate for buttons, links, and key UI throughout.
- Don't: don't add glow to primary elements — `luminescence: none` is deliberate; this theme's polish comes from clean shadows and gradients, not light effects.

### secondary (`#7C3AED` violet)
- When to use: a premium/differentiated counterpoint to blue — the second stop in `--gradient-text` (blue→violet), secondary UI, "enterprise-tier" signaling.
- Surface area: moderate — a genuine second brand color, used the way SaaS products use a secondary brand hue for premium features or differentiated sections.
- Don't: don't let violet compete with blue for primary-action status — it's a supporting brand color, not an alternative CTA color.

### accent (`#0891B2` teal)
- When to use: data/technical accents — the second stop in `--gradient-accent` (blue→teal), a cooler technical counterpoint distinct from violet's "premium" connotation.
- Surface area: small to moderate — technical UI details, data visualization accents.
- Don't: don't conflate accent-teal with secondary-violet — they carry different connotations (teal = technical/data, violet = premium/differentiated).

## When To Use
- Developer platforms, API products, enterprise SaaS, or B2B tech products wanting a genuinely modern, "funded startup" visual register.
- Content benefiting from clean grid-paper texture and soft layered shadows over glow or gradient maximalism.
- Marketing sites, docs, or dashboards for technical products needing high hierarchy clarity (`hierarchyClarity: high`).

## When NOT To Use
- Consumer, playful, or warm-branded content — this is a precise, clean, B2B-tech register.
- Content wanting glow, luminescence, or glassmorphic depth — none of those effects exist in this theme by design.
- Dark-mode-only contexts — no dark variant; the ice-white/cool-gray base is structural to the "engineering blueprint" read.

## How To Use — Full Potential
- Use the subtle hero gradient (`#EDF2FF → #F6F8FA → #F0F4FF`) behind marketing/landing content — it's a near-white, barely-there gradient that adds polish without calling attention to itself, exactly matching how real SaaS product sites use hero backgrounds.
- Keep the cool-gray grid visible at low opacity across the full page — it's the theme's "engineering blueprint" signal and should read as ambient texture, not a decorative overlay.
- Reserve the blue→violet gradient border for premium/differentiated UI moments (e.g., an upgrade CTA, an enterprise-tier badge) — consistent with how real SaaS products use a secondary gradient for premium signaling.
- If only one thing: apply the blue gradient button with the fine cool-gray grid background behind it — the fastest way to signal titanium-cloud's modern-SaaS register.

## Apply-Mode Notes
- Step 4j: this theme has zero glow/luminescence by design — don't add glow during harmonize even for hover/focus states; use shadow elevation changes instead.
- Step 4a: keep violet (secondary) and teal (accent) semantically distinct — violet for premium/differentiated, teal for technical/data — rather than treating them as interchangeable "extra" colors.
