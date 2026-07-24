# soviet-agitprop

Constructivist propaganda poster discipline — stark red, ink black, newsprint cream, with diagonal slash dividers as literal structural elements, not decoration.

## Core Concept
Newsprint-cream canvas (`#F2EDD7`) with faint paper-grain noise, Oswald's ultra-condensed display face (evoking Rodchenko-era poster type) against PT Serif body. `gradients.*: none`, `luminescence: none`, `borderRadius: 0px` — every visual move is flat, hard-edged, and offset-shadowed (`4px 4px 0 #111111`, no blur), consistent with letterpress/silkscreen poster production. Per `design.notes`, "cards cut like ROSTA Window panels" — a specific historical reference (Mayakovsky's ROSTA propaganda-window poster series) that should inform actual card/panel treatment, not just color choice.

## Color Role Guidance

### primary (`#CC1111` stark red)
- When to use: the singular ideological signal — primary buttons, the one color meant to command attention against the cream/black field, per classic agitprop's disciplined single-red-accent convention.
- Surface area: precise and sharp — bold blocks and rules, not soft accents; red should hit hard where it appears.
- Don't: don't soften red with any gradient or glow — `gradients.*: none` is absolute; red must read as flat ink/paint, not a lit brand color.

### secondary (`#111111` ink black)
- When to use: structural — every border in the theme uses this exact black (`border: #111111`), all offset shadows are black-on-black (`--shadow-sm/md/lg/xl`), headline text.
- Surface area: extensive — black is doing the job of borders, shadows, and primary text throughout, more structural weight than a typical "secondary."
- Don't: don't lighten black to a soft gray for "friendlier" UI — the stark black/cream/red contrast is the entire point.

### accent (`#FFD700` gold)
- When to use: a rare third note — star/emblem details, a single flag of emphasis distinct from red's ideological urgency.
- Surface area: small — gold should be sparse, used the way a poster uses gold leaf or a star emblem, not as a UI color.
- Don't: don't use gold as a general highlight — its scarcity and specific "emblem" connotation should be preserved.

## When To Use
- Historical, political-design, protest-poster, or constructivist-inspired content wanting genuine period authenticity.
- Bold editorial or campaign content wanting maximum stark contrast and confrontational energy.
- Content that can sustain diagonal structural dividers and hard offset shadows as real layout devices, not just color theming.

## When NOT To Use
- Any content needing neutrality or political non-affiliation — the propaganda-poster register is inherently loaded and should be used with awareness of that connotation.
- Soft, friendly, or approachable branding — every design choice (stark contrast, zero radius, condensed type) resists warmth.
- Content needing more than one bold chromatic accent — red's power here depends on staying the singular ideological color; a second bright hue dilutes it.

## How To Use — Full Potential
- Use diagonal slash dividers as actual structural section breaks, not decorative flourishes — per the theme's own framing, they're load-bearing layout elements, echoing constructivist poster composition.
- Cut cards/panels with the ROSTA Window reference in mind — sequential, poster-panel framing rather than generic rounded cards.
- Reserve hard black offset shadows (`4px 4px 0 #111111`) as the only elevation mechanism — never introduce blur-based soft shadows.
- If only one thing: apply a bold red block with a hard black offset shadow against the cream field — the fastest way to signal soviet-agitprop.

## Apply-Mode Notes
- Step 4a: keep red as the sole loud chromatic accent — don't introduce a second saturated hue during harmonize even for multi-category content; use black structurally and gold sparingly instead.
- Step 4d/4j: zero gradients, zero glow, zero radius by design — any hero/colored-section harmonize must stay flat with hard offset shadows only.
