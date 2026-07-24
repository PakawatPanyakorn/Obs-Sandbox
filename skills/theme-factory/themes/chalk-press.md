# chalk-press

Brutally minimal editorial where typography alone carries the entire design — "pure ink on cream," no gradients, no glow, no radius, and only one color besides black and cream.

## Core Concept
Warm cream field-notebook canvas (`#F7F4EE`) with faint horizontal ruled lines (`patternType: lines-h`, 28px spacing, evoking broadsheet/notebook paper), Playfair Display at 900-weight for headlines against Crimson Pro serif body. The theme's radical simplification: `secondary` and `accent` are the *same* red (`#C41A1A`) — there is no third chromatic role. `shadows.colored: none` confirms color is never used for elevation or emphasis-via-glow; hierarchy comes entirely from type size/weight and the one red accent, per the theme's own notes ("typography does 100% of the visual work").

## Color Role Guidance

### primary (`#1C1916` near-black ink)
- When to use: this is the theme's dominant "color" — body text, headlines, structural borders. Unlike most themes, primary here is not a brand hue but literal ink.
- Surface area: everywhere text and structure live — this is correct and expected; don't try to introduce a separate "brand color" for primary actions where black ink already does the job.
- Don't: don't lighten or tint primary for "softer" UI states — the stark black/cream contrast is the point; a grayed-down primary undermines the "ink" premise.

### secondary / accent (`#C41A1A` editorial red — one color, two role names)
- When to use: the theme's *only* chromatic accent — a single pull-quote rule, one emphasized word, error states, the one "look here" signal per view.
- Surface area: minimal and precise — a thin rule, a small badge, a single highlighted figure. Never a fill of any real size.
- Don't: don't treat secondary and accent as two different colors to differentiate roles — they're deliberately identical; inventing a second red-adjacent hue to "separate" them breaks the theme's radical two-tone-plus-one-accent discipline.

## When To Use
- Literary, essay, long-form journalism, or field-notebook-style content where typographic hierarchy alone should carry meaning.
- Editorial products wanting a stark, confident, ink-and-paper feel without any decorative chrome (no cards with shadows-as-depth, no gradients, no icons needing color).
- Content genuinely built around reading, not scanning — dense body copy at `lineHeight: 1.7`, serif throughout.

## When NOT To Use
- Any content needing more than one chromatic accent or a real success/warning/error visual distinction beyond text — `success`/`warning` exist as tokens but the theme's design philosophy resists using them as prominent UI color (that would dilute the one-red-accent rule).
- Dashboard, data-viz, or card-grid-heavy layouts — the theme has no shadow-as-depth system (`elevation: subtle`, hairline-rule shadows only) and no card gradient; it will read as flat and under-designed in a context expecting visual layering.
- Playful or youthful branding — Playfair Display 900 + ruled-paper background reads as serious, literary, adult.

## How To Use — Full Potential
- Let type scale alone establish hierarchy — a huge Playfair Display headline next to small-caps Courier Prime metadata is the theme's primary structural tool; don't reach for color or boxes to create hierarchy that type weight/size should handle.
- Use the ruled-line background as a literal writing-surface cue — it's most effective behind body copy, not busy UI chrome; dense components will fight the faint horizontal rhythm.
- Reserve the red accent for exactly one thing per view (a pull-quote rule, one emphasized figure) — its power depends on scarcity, mirroring the theme's overall "one accent color" discipline.
- If only one thing: pair a 900-weight Playfair Display headline directly against small tracked-out Courier Prime mono metadata — this exact serif/mono contrast is the fastest way to signal chalk-press.

## Apply-Mode Notes
- Step 4a: don't introduce a distinct accent color separate from secondary — this theme deliberately collapses them into one red; keep that collapse during harmonize rather than inventing a second accent hue to satisfy a generic 3-role expectation.
- Step 4d/4j: zero gradients, zero glow, zero colored shadows — any hero/colored-section harmonize should use flat ink-on-cream with, at most, a hairline rule shadow (`--shadow-md`'s solid-color offset line, not a blur).
