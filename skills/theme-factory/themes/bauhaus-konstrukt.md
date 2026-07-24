# bauhaus-konstrukt

The Bauhaus as historical institution, not as a shape-toy — a 1923 Weimar workshop-catalogue voice (German color labels, manifesto-style body copy) rendered in the same red/blue/yellow triad as [[bauhaus-geometry]] but with an ideological, brutalist register instead of a playful, educational one.

## Core Concept
Warm ivory canvas (`#F5F0E8`) with a near-invisible 45° diagonal stripe pattern (`patternType: lines-h`, opacity `0.04`) evoking constructivist poster paper. League Spartan at 900-weight for display, Archivo at 300-weight for body — the same heavy/light contrast as `bauhaus-geometry` but paired here with genuine period voice: German color names (Rot/Blau/Gelb/Weiss/Schwarz), a real manifesto sentence ("form derives from process, not tradition"), workshop department cards (`Vorkurs`, `Werkstatt`). `aesthetic: brutalist` (not `playful`) and `personality: ideological` are the load-bearing difference from its sibling theme.

## Color Role Guidance

### primary (`#D42020` Bauhaus red)
- When to use: the lead department/action — primary buttons (`.bk-btn-primary`), the first workshop card's accent bar (`.bk-card-bar`), the "Rot" swatch's featured position.
- Surface area: bars, buttons, accent stripes on cards — flat fills, no gradient (this theme has none by design).
- Don't: don't soften red with any glow or gradient — `effects.luminescence: none` and `gradients.*: none` are absolute; red here must read as flat pigment, not a lit-up brand color.

### secondary (`#1040A0` Bauhaus blue)
- When to use: the second department/voice — secondary buttons (`.bk-btn-secondary`), the metal-workshop card bar, structural dividers.
- Surface area: equal footing with red in the triad — this theme, unlike many others, treats primary/secondary as co-equal ideological colors, not a main/supporting hierarchy.
- Don't: don't demote blue to a "muted" or supporting role — the Bauhaus triad is presented as three equals (Rot/Blau/Gelb), not a primary with two accents.

### accent (`#E8C800` raw yellow)
- When to use: the third department/voice — accent buttons (`.bk-btn-accent`), the print-workshop card bar. Needs dark text for contrast (per `textOnPrimary`/`text` pairing conventions).
- Surface area: equal to red/blue in the triad, not a minor highlight.
- Don't: don't use yellow as a status/warning color primarily — it has its own dedicated `warning` (`#C08000`, a distinct ochre) — yellow here is a primary ideological color first.

## When To Use
- Design history, education, or institutional-archive content — the theme's own voice (Weimar workshop catalogue, German labels, real Bauhaus pedagogy references) is built for exactly this register.
- Content wanting "form follows function" austerity with genuine period authenticity, not a generic "geometric shapes" aesthetic.
- Brutalist-leaning product/portfolio sites that want flat, unapologetic primary-color blocking without softness.

## When NOT To Use
- Playful, consumer, or shape-system-driven content — for that register, [[bauhaus-geometry]] (same triad, `playful`/`educational` personality, 16-shape semantic system) is the better-fitting sibling theme.
- Any content needing gradients, glow, or soft elevation — this theme has none of those by design (`elevation: layered` refers to shadow offset stacking, not blur-based depth).
- Fast, snappy interaction feel — `motion.feel: instant` with `durationSlow: 180ms` and `easing: linear` is deliberately blunt, not springy or delightful.

## How To Use — Full Potential
- Lead with `.bk-header`'s combination: a full-width color bar (`.bk-header-bar`) + large display heading with one word in red (`.bk-display-red`) + a right-aligned year/date marker (`.bk-header-year`) — this exact "institutional letterhead" composition is the theme's strongest opening.
- Use `.bk-card-bar`'s flat top-edge color stripe (not a full-card tint) to assign each card to one triad color — this is the theme's native way of categorizing content by department/type without relying on icons.
- Keep body copy in genuine period or institutional voice where possible — the theme's effect depends partly on content, not just chrome; generic marketing copy undersells it.
- If only one thing: pair a 900-weight League Spartan headline with a 300-weight Archivo body paragraph directly beneath it — the weight contrast alone signals "Bauhaus typographic ideology."

## Apply-Mode Notes
- Step 4a: treat primary/secondary/accent as three co-equal ideological colors (per the "Rot/Blau/Gelb" framing), not a primary-dominant hierarchy — don't apply the generic ">60% primary" rule here.
- Step 4d/4j: this theme has zero gradients and zero glow by design — preserve flat color blocking and offset shadows only; don't introduce softness during harmonize.
- If the target already carries [[bauhaus-geometry]]'s shape-badge system, don't merge the two themes' voices — konstrukt is institutional/historical, geometry is playful/educational; pick one register per project.
