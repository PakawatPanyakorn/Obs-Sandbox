# synthwave-84

The classic "SynthWave '84" code-editor theme translated to a full UI system — hot pink, neon cyan, and electric yellow neon glow on a deep purple-black (never true black) background.

## Core Concept
Deep purple-black canvas (`#262335`) — per the theme's own notes, "the purple cast is essential to the synthwave aesthetic and distinguishes it from plain black." Rajdhani's technical geometric display against Barlow Condensed's narrow body. `glassBlur: 12px` + `backdropFilter: blur(12px)` give panels genuine frosted depth against the neon-lit background. Nearly every shadow level (`sm` through `xl`) carries a pink glow component baked in alongside its blur/offset — glow isn't reserved for special elements, it's the theme's default elevation language.

## Color Role Guidance

### primary (`#ff7edb` hot pink)
- When to use: the dominant neon signal — primary buttons (`--gradient-button`, pink→cyan), the base glow color for nearly every shadow level, headline text-shadow.
- Surface area: generous — pink is meant to feel omnipresent, like neon signage; even non-pink shadows carry a pink glow tint by default.
- Don't: don't apply primary without glow — every shadow level in this theme's default system already includes a pink glow component; a flat pink fill with a plain shadow undersells the whole aesthetic.

### secondary (`#36f9f6` neon cyan)
- When to use: the cool neon counterpart — the second stop in `--gradient-button`/`--gradient-text` (pink→cyan), gradient-border pairing.
- Surface area: substantial — appears in nearly every gradient alongside primary, a true co-equal partner, not a minor accent.
- Don't: don't use cyan in isolation from pink — the theme's signature 2-color gradient (pink→cyan) is more central to its identity than either color alone.

### accent (`#ffe66d` electric yellow)
- When to use: the third neon note — center stop in the 3-color `--gradient-accent` (pink→yellow→cyan), warning states (shares hex with `warning`).
- Surface area: smaller than primary/secondary — a bridging color in gradients and a caution signal.
- Don't: don't treat accent as equal-frequency to pink/cyan — it's the least-used of the three, appearing mainly as a gradient midpoint or warning flag.

## When To Use
- Developer tools, retro-gaming, 80s-revival, or cyberpunk-adjacent products wanting the specific, recognizable "SynthWave '84" register (a known, beloved code-editor theme lineage) rather than generic neon-purple.
- Dark-mode products wanting glow as the default elevation system, not an occasional effect.
- Content that can sustain real backdrop blur — glass panels are meant to look lit from within against the neon backdrop.

## When NOT To Use
- Light-mode or daytime contexts — no light variant; the purple-black base and neon glow are the entire premise.
- Calm, corporate, or understated content — glow-as-default elevation is inherently loud.
- Static/low-fidelity rendering — `backdropFilter` and multi-layer glow shadows depend on real compositing; without it the theme degrades to flat dark purple with pink text.

## How To Use — Full Potential
- Use the signature pink→cyan 2-color gradient (`--gradient-button`, `--gradient-text`) as the default treatment for CTAs and headlines — it's the theme's most recognizable signature, more so than either color alone.
- Keep glow present on every shadow level by default, not just hover/focus states — this theme's elevation system is glow-by-default, distinguishing it from themes that reserve glow for emphasis only.
- Use glass panels (`backdropFilter: blur(12px)`, `glassTint`) for cards/modals floating over the purple-black base — it's what gives depth beyond flat dark-mode panels.
- If only one thing: apply the pink→cyan gradient with matching glow shadow to a button — the fastest, most recognizable signal of synthwave-84.

## Apply-Mode Notes
- Step 4j: glow-by-default is structural here, not a special-case effect — preserve pink glow tint across the general shadow scale (sm through xl), not just on primary CTAs.
- Step 4a: the pink→cyan gradient pairing is more central to this theme's identity than either color solo — wherever the target has a 2-tone gradient opportunity (buttons, headlines), default to this exact pairing.
