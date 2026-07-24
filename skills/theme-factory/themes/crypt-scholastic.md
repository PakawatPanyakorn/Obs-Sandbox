# crypt-scholastic

A rare-books reading room built underground — gothic academic, not gothic-horror, where crimson/forest-green/aged-gold read as institutional heraldry rather than a haunted-house palette.

## Core Concept
Near-black plum canvas (`#120A10`) with fine SVG fractal-noise grain (opacity `0.05`, "aged leather binding, dungeon vaults"), Cinzel's carved-stone display against Gentium Plus's classical body serif. `shadows.colored: 0 0 0 1px var(--color-border)` is unusual — this theme uses a hairline border-ring instead of a glow for its "colored" shadow, reinforcing restraint over luminescence (`luminescence: subtle`). The 3-color gradient border (`crimson → gold → green`) is the one place all three roles appear together, evoking an illuminated manuscript's tricolor rule rather than a modern brand gradient.

## Color Role Guidance

### primary (`#8B1A3A` deep crimson)
- When to use: institutional authority — primary buttons (`--gradient-button`, crimson gradient), the hero's dominant warm note, headline text-shadow (`0 0 24px rgba(139,26,58,0.3)`).
- Surface area: buttons, borders, headline accents — confident but not dominant; this theme's `hierarchyClarity: high` comes from typography, not color saturation.
- Don't: don't push crimson toward horror-red — keep it deep and desaturated (`#8B1A3A`, not a bright red); a brighter crimson breaks the "scholastic," not "haunted," register.

### secondary (`#2A5C2A` forest green)
- When to use: a cooler institutional counterpoint — secondary buttons, one gradient stop in `--gradient-accent` (crimson→green), anything reading as "the other faculty color."
- Surface area: moderate, paired with crimson rather than standing alone — the two together evoke academic heraldry (think university crest colors), not a random duo.
- Don't: don't use green for success states more than its dedicated `success` token already does — keep secondary's role about institutional identity, not status signaling.

### accent (`#C8A840` aged gold)
- When to use: illuminated-manuscript detailing — gradient text (`--gradient-text`, gold-dominant 3-stop), the "precious" highlight on an otherwise dark, restrained page.
- Surface area: small — gilt-edge detailing, not a fill; its value depends on scarcity against the dark plum field.
- Don't: don't confuse accent gold with `warning` (`#B89020`, a distinct duller gold) — accent is decorative/precious, warning is a genuine caution state.

## When To Use
- Academic institutions, rare-book collections, esoteric societies, dark-academia content — the theme's own framing ("rare books / esoteric institution") is literal.
- Dark-mode editorial content wanting gravitas and restraint over glow or maximalism — `luminescence: subtle`, no backdrop blur, no strong glow anywhere.
- Content that benefits from genuine institutional/heraldic color logic (crimson + green + gold as a tricolor identity) rather than a single-accent dark theme.

## When NOT To Use
- Horror, occult-shock, or overtly spooky content — the palette is deliberately restrained and scholarly, not lurid; pushing any color brighter breaks the "academic" register.
- Bright, energetic, or youth-oriented products — `motion.feel: subtle`, deep desaturated tones, and dense serif body text (`lineHeight: 1.75`) are built for slow, deliberate reading.
- Content needing strong glow/luminescence as a design language — this theme intentionally under-uses glow (`glowColor: transparent`) in favor of noise grain and hairline borders.

## How To Use — Full Potential
- Use the 3-color gradient border (`crimson → gold → green`) on the single most ceremonial element per page (a title card, a certificate-style panel) — it's the theme's one "all three colors together" moment and loses impact if overused.
- Lead with the hero's dark 3-stop gradient (`#241420 → #120A10 → #100810`) plus fractal noise grain — the grain is what gives the near-black plum its "aged parchment/leather" quality; a flat solid background loses this entirely.
- Reserve `shadows.colored`'s hairline border-ring technique for cards/panels that should feel "cataloged" or "shelved" rather than elevated — it's a restrained alternative to glow that fits this theme's scholastic register.
- If only one thing: pair a Cinzel headline with a `text-shadow: 0 0 24px rgba(139,26,58,0.3)` — the soft crimson glow behind carved-stone type is the fastest way to signal crypt-scholastic.

## Apply-Mode Notes
- Step 4d/4j: this theme substitutes a hairline border-ring for the usual "colored shadow" glow (`shadows.colored: 0 0 0 1px var(--color-border)`) — when harmonizing, don't default to a glow-based colored shadow; use the border-ring technique to stay in register.
- Step 4a: treat crimson/green/gold as an institutional tricolor (like a university crest), not a primary-dominant hierarchy — balance is more even than the generic ">60% primary" default assumes.
