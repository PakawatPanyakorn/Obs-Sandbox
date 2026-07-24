# eigenvalue

A quantitative-finance algorithm lab rendered in ice lavender and electric violet — a "blueprint" register (dot-grid, overlapping data panels) that reads as rigorous and light-mode-precise rather than the usual dark-terminal quant aesthetic.

## Core Concept
Ice-lavender canvas (`#EEF0FF`) under a 24px violet dot-grid with a subtle 2-layer gradient overlay (violet + cyan), Syne's ultra-bold (800wt) geometric sans display against Source Serif 4's refined 300-weight optical serif. The theme's distinguishing choice is doing "quant lab" in *light* mode with a blueprint dot-grid, when most technical/algorithmic themes default to dark terminal aesthetics — this makes it the light-mode counterpart to themes like `alpha-signal` or `cyber-terminal`.

## Color Role Guidance

### primary (`#5C2EFF` electric violet)
- When to use: the dominant analytical signal — primary buttons (`--gradient-button`, violet gradient), gradient text (`--gradient-text` here is a flat hex, not a multi-stop gradient — restraint compared to other maximalist violet themes), dot-grid pattern color.
- Surface area: generous — violet anchors the entire visual system, from background dots to buttons to shadow tints (`--shadow-colored`).
- Don't: don't confine primary to small accents — this theme wants violet felt throughout, including the subtle background pattern.

### secondary (`#00D4CC` neon cyan)
- When to use: the analytical counterpoint — one gradient stop in `--gradient-accent` (violet→cyan), the second background gradient layer, data-visualization contrast against violet.
- Surface area: moderate — a genuine second voice, used more assertively than a typical "quiet secondary."
- Don't: don't let cyan and violet blend into a single visual mass — keep them as distinct data-channel colors (e.g., two different series in a chart), not merged into one blob.

### accent (`#A8FF20` acid lime)
- When to use: the rare third note — appears in the 3-color gradient border (`--border-gradient: violet, cyan, lime`) as the sharpest, most attention-grabbing stop.
- Surface area: minimal — lime is the least-used color in the palette; reserve it for a genuine "flag this" moment.
- Don't: don't use lime as a general accent color at the same frequency as secondary — its value depends on rarity against the cooler violet/cyan field.

## When To Use
- Quantitative finance, algorithmic trading, data-science, or research-lab dashboards wanting a light-mode technical register instead of dark terminal chrome.
- Content benefiting from an "asymmetric blueprint" layout — overlapping data panels rather than a uniform grid (per `design.notes`).
- Products wanting Syne's ultra-bold geometric display for short technical headlines paired with genuinely readable serif body text for analysis/explanation.

## When NOT To Use
- Dark-mode-only product contexts — this theme's entire identity is being a *light* quant-lab theme; forcing it dark loses the differentiator.
- Warm, human, or narrative-driven content — the dot-grid blueprint and ultra-bold geometric type are clinical and precise by design.
- Simple, uniform card-grid layouts — the theme's own notes call for "asymmetric overlapping data panels," which a plain uniform grid undersells.

## How To Use — Full Potential
- Use the 24px dot-grid + gradient-mesh background combination consistently across the full page — it's what gives the light canvas technical rigor instead of reading as a generic pastel theme.
- Reserve the 3-color gradient border (violet→cyan→lime) for the single most important panel or callout per view — it's the one place all three roles appear together and loses impact if used broadly.
- Lean into Syne 800's extreme geometric weight for short data labels/headlines, and let Source Serif 4's light weight carry actual analysis prose — the pairing is what makes this theme feel both rigorous and readable.
- If only one thing: apply the violet dot-grid pattern behind a Syne 800 headline — the fastest way to signal "quant lab," light-mode edition.

## Apply-Mode Notes
- Step 4k (background pattern): the dot-grid + gradient mesh is structural, not decorative — preserve it as a body-level background during harmonize rather than confining it to a hero section.
- Step 4a: keep accent lime genuinely rare — don't distribute it evenly with secondary cyan even if the target file has multiple data series/categories needing color.
