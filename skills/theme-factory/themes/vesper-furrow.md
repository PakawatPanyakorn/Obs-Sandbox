# vesper-furrow

Formal editorial tone with countryside grime — dying amber dusk light bleeding from the top of a dark-earth canvas, dusty mauve and terracotta underneath, restrained rather than romantic.

## Core Concept
Dark earth-brown canvas (`#1c1915`) with a warm amber glow specifically positioned at the top ("simulates last light of dusk," fading out by 38% down the page) plus fractal-noise grain for "dirty countryside texture." Fraunces' variable-optical display against Lora's warm serif body. `glassTint: rgba(36,32,24,0.65)` gives panels a genuine dusty, semi-opaque quality even with `glassBlur: 0` — opacity does the "dust in the air" work that blur would do elsewhere.

## Color Role Guidance

### primary (`#b8914a` dying amber)
- When to use: the "last light" signal — primary buttons (`--gradient-button`, amber gradient), the top-of-page dusk glow, headline gradient (`--gradient-text` runs amber tones only).
- Surface area: concentrated toward the upper portion of a composition, mirroring the dusk-light background gradient — don't spread it evenly as a generic brand color ignoring the vertical light metaphor.
- Don't: don't brighten primary into a cheerful gold — "dying" is the operative word; keep it desaturated and waning, not vibrant.

### secondary (`#7d6b78` dusty mauve)
- When to use: the "dust/dusk shadow" note — one gradient stop (`--gradient-accent` runs amber→mauve), a cool-leaning counterpoint to the warm amber/terracotta pair.
- Surface area: moderate — a muted, desaturated presence, never bright.
- Don't: don't saturate secondary toward purple — its desaturation is what keeps it reading as "dust in fading light" rather than a decorative accent.

### accent (`#a0745a` terracotta)
- When to use: earth/clay tones — a warm counterpoint between amber and mauve, grounding the palette in "furrow" (tilled earth) imagery.
- Surface area: small to moderate — an earthy highlight, not a fill.
- Don't: don't brighten accent toward a cheerful orange — restraint (per `personality: restrained`) applies to every color in this palette, not just primary.

## When To Use
- Rural, agricultural, countryside, or "end of day" narrative content — the theme's own dusk/furrow imagery is literal.
- Formal editorial content wanting warmth without brightness — a desaturated, restrained register distinct from more vivid earth-tone themes in the catalog.
- Content that benefits from a genuine top-of-page light gradient rather than a flat dark background.

## When NOT To Use
- Bright, energetic, or urban content — every color is deliberately desaturated and "dying," resisting vibrancy.
- Content needing a cheerful or optimistic register — this is restrained melancholy dusk, not a warm sunrise.
- Light-mode contexts — no light variant; the dark-earth base with fading amber is structural.

## How To Use — Full Potential
- Position the amber dusk-glow gradient specifically at the top of the page, fading out within the first third — this positional light source, not just the color palette, is what makes the theme feel like "last light," and applying amber evenly loses that.
- Use `glassTint`'s semi-opaque dusty panels (`rgba(36,32,24,0.65)`) for cards/modals — the opacity-without-blur approach evokes dust in fading air more accurately than a blurred glass effect would.
- Keep every color desaturated relative to a typical warm-earth palette — restraint is load-bearing across primary, secondary, AND accent, not just the dominant hue.
- If only one thing: apply the top-of-page amber gradient fading into dark earth — the fastest way to establish vesper-furrow's "dusk" premise.

## Apply-Mode Notes
- Step 4d: preserve the top-positioned dusk-light gradient rather than converting it to a uniform background — the vertical light-source metaphor is structural to this theme.
- Step 4a: keep all three chromatic roles desaturated during harmonize — resist brightening any of them even where a target's existing palette was more vivid; restraint is the defining trait here.
