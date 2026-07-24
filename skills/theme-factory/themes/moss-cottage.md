# moss-cottage

Cottagecore rendered with genuine botanical restraint — sage, terracotta, and honey amber on warm linen, soft and handmade without tipping into saccharine.

## Core Concept
Warm linen canvas (`#F2EEE0`) with a sage-green dot-grid at 18px spacing — the theme's own notes place this deliberately "between sakura 22px and tokyo 8px," a calibrated botanical-illustration density, not an arbitrary choice. Gilda Display's soft serif against Mulish's light sans, fully rounded buttons (`buttonRadius: 999px`) and generous card radius (`16px`) reinforce the handmade softness. `luminescence: none` and zero glow keep the theme grounded and organic rather than precious — softness comes from shape and spacing, not shine.

## Color Role Guidance

### primary (`#5A7A3A` sage green)
- When to use: the "growing/living" signal — primary buttons (`--gradient-button`, a sage-only gradient), the botanical dot-grid pattern color, glow tint (though glow itself is disabled, `glowColor` stays sage).
- Surface area: generous — sage is the theme's dominant, grounding tone.
- Don't: don't render primary as a hard, saturated green — keep it muted/earthy; a bright green would break the "moss" register.

### secondary (`#A06840` terracotta)
- When to use: a warm earthenware counterpoint — secondary buttons, one gradient stop (`--gradient-text` runs sage→terracotta).
- Surface area: moderate — reads as "clay pot," a grounded warm note against the cooler sage.
- Don't: don't push terracotta toward the theme's dedicated `error` (`#9A3A2A`) — keep enough distinction that secondary reads as warm/earthy, not alarming.

### accent (`#E8A840` honey amber)
- When to use: the "sunlight/honey" note — gradient endpoints (`--gradient-accent`, sage→amber), the brightest, warmest highlight in the palette.
- Surface area: small — a warm glow-substitute (since actual glow effects are disabled) that carries the "cozy" feeling instead.
- Don't: don't confuse accent with `warning` (`#A07820`, a duller gold) — accent is decorative warmth, warning is a genuine caution state.

## When To Use
- Home/lifestyle, garden, artisan-craft, or slow-living content — the theme's own vocabulary (cottagecore, botanical, handmade) is literal.
- Content wanting softness and warmth through shape (rounded corners, pill buttons) and gentle pattern rather than glow or gradient maximalism.
- Illustrative content (`imageStyle: illustrative`) — botanical line-art or hand-drawn imagery pairs naturally with the dot-grid texture.

## When NOT To Use
- Tech, corporate, or high-precision content — the fully rounded buttons and spacious density (`density: spacious`) read as soft and unhurried, the opposite of technical/dense.
- Bold or maximalist branding — this is a muted, earthy palette; anything wanting punch or high energy should look elsewhere.
- Dark-mode contexts — no dark variant; the warmth depends on the linen base.

## How To Use — Full Potential
- Use fully rounded pill buttons (`buttonRadius: 999px`) consistently — this is the single strongest "soft cottagecore" signal in the component system, more so than color alone.
- Keep the sage dot-grid visible across the full page at its calibrated 18px spacing — it's tuned to feel botanical-illustration-like, not just decorative; changing the spacing changes the read entirely.
- Reserve the 3-color gradient border (sage→terracotta→amber) for a single hero or feature card — it's the one place all three "garden, clay, honey" tones appear together.
- If only one thing: pair a Gilda Display headline with a fully-rounded sage button beneath it — the softness of both together is the fastest way to signal moss-cottage.

## Apply-Mode Notes
- Step 4c/4e (shape/radius): preserve the fully-rounded button convention — a sharp-cornered button on this theme actively contradicts its "soft, handmade" premise.
- Step 4j: this theme has no glow/luminescence by design — don't add glow during harmonize even though `glowColor` is defined; warmth here comes from color and shape, not light effects.
