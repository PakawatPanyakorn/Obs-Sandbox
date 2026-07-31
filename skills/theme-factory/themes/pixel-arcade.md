# pixel-arcade

The glow of a coin-op cabinet in a dark room — every corner notched instead of rounded, every shadow a hard offset instead of a blur.

## Core Concept
A near-black CRT canvas (`#0D0B1A`) under fine horizontal scanlines (`background.patternType: lines-h`, 3px pitch) carries three saturated cartridge colors — hot magenta, cyan, lime — that never blend into each other. The theme's `playful` aesthetic and `retro` personality come less from the palette and more from two structural choices: the `.pa-notch` clip-path replaces every border-radius with an 8-sided pixel-notch, and `--easing: steps(4, end)` makes hovers and transitions advance in visible frames rather than glide. Space Mono's exaggerated monospace quirks (`.pa-display`) and Share Tech Mono's raw digital body copy keep the whole page reading as a single low-res font family, the way an actual cabinet only ships with one bitmap face.

## Color Role Guidance

### primary (`#FF2E88`)
- When to use: the one "press this" action per screen — `.pa-btn-primary`, the `P1 READY` badge, headline glow (`.pa-header h1`).
- Surface area: buttons and short display text only, always paired with `--glow-md`/`--shadow-colored` — a flat unglowing magenta reads as a mistake, not a design choice.
- Don't: don't use primary for body text or large fills; it's a beacon color, not a reading color, and at body size the glow makes it fatiguing.

### secondary (`#29E0FF`)
- When to use: the "system" voice — subheads (`.pa-h3`), secondary CTA (`.pa-btn-secondary`), the `COMBO x3` badge. Reads as informational rather than urgent.
- Surface area: roughly matched to primary in weight but always the second-most prominent color on any given screen, never competing with primary in the same button row.
- Don't: don't pair primary and secondary glow on the same element — each has its own shadow tint (`--shadow-colored` vs. the inline `#0C6E80` offset) specifically so they stay visually distinct.

### accent (`#B6FF3C`)
- When to use: scorekeeping and reward moments only — `.pa-card-score`, the lit credit blocks in `.pa-credit-row`, the `EXTRA LIFE`-adjacent success badge.
- Surface area: small, celebratory, and rare — it should feel like a bonus popping up, not a fourth structural color.
- Don't: don't use accent for any persistent UI chrome (nav, borders, labels) — it loses its "you earned this" meaning if it's always on screen.

## When To Use
- Retro/8-bit gaming products, game-jam pages, dev-tool changelogs that want deliberate low-fi charm instead of polish.
- Any dark-mode surface that wants a genuinely blocky, hard-edged alternative to the library's existing smooth neon themes (`synthwave-84`, `cyber-terminal`).
- Short-session, high-density UI — score readouts, leaderboards, level-select grids — where `.pa-mono` status lines and compact spacing (`density: compact`) fit naturally.

## When NOT To Use
- Long-form reading content — the monospace-only type system and `steps()` motion are built for glanceable HUD text, not paragraphs.
- Anything needing rounded, soft, or approachable framing — every shape in this theme is deliberately hard-notched; a rounded card dropped in will look like a bug, not a variation.
- Alongside `cyber-terminal` or `synthwave-84` in the same project — all three are dark neon-on-black registers and will blur together without a strong content reason to keep them apart.

## How To Use — Full Potential
- Lead with `.pa-header`'s combination: flat surface background (no hero gradient, by design), `text-shadow: var(--glow-md)` on the `<h1>`, and the lit/unlit `.pa-credit-row` blocks — that trio reads as "cabinet screen" instantly.
- Apply `.pa-notch` to any card, tile, or button that should read as native to this theme — it's the single biggest tell that separates pixel-arcade from a generic dark theme with bright accents.
- Keep `--easing: steps(4, end)` on interactive transitions (hover, focus, toggle) rather than swapping in a smooth cubic-bezier — the stepped motion is as load-bearing to the "arcade" read as the color palette.
- If only one thing: give a heading `.pa-notch` cropping plus `text-shadow: var(--glow-sm)` in Space Mono — that single combination is the fastest way to make a block unmistakably read as pixel-arcade.

## Apply-Mode Notes
- Step 4c (radius): this theme has zero border-radius anywhere by design — apply `.pa-notch` clip-paths instead of introducing any `border-radius` value, even a small one, when harmonizing into a target file.
- Step 4j (gradients/glow): `gradients.hero/card/button/text/accent` are all `none` — glow comes exclusively from `box-shadow`/`text-shadow`, never from a gradient fill. Do not add a gradient hero even as a "single hue" compromise; this theme's flat-panel header is intentional.
- Step 4k (motion): don't substitute a standard ease-out curve for `steps(4, end)` — smoothing the motion is the most common way a harmonized page stops reading as pixel-arcade.
