# Theme Doc Template

Every theme preset gets a companion `themes/<name>.md` file, written when the theme is created (Create Mode step 5) and consulted again during Apply Mode. Its job is to capture judgment calls that the theme's JSON data cannot express on its own — not to restate `description` or `design.notes` in different words.

**Before writing one:** read the target theme's `.html` file in full — the JSON block *and* the rendered markup/CSS. Component-level guidance ("which section unlocks full potential") requires citing real class names that exist in the file, not generic advice that could apply to any theme.

**Bar for acceptance:** if a sentence in the doc would be equally true of a different theme with the names swapped, it's too generic — rewrite it with something specific to this theme's actual palette, effects, or component treatment.

## Sections (use this exact structure)

```markdown
# <name>

<one-sentence restated concept — the felt experience, not a copy of `description`>

## Core Concept
2-4 sentences: what makes this theme distinct, what "world" it evokes, what single idea it commits to. Reference specific `design.aesthetic`/`design.personality` values but explain *why* they combine the way they do in this theme, not just list them.

## Color Role Guidance
### primary (<hex>)
- When to use: <concrete trigger — CTAs, active nav, the one data series that matters>
- Surface area: <e.g. "5-10% of viewport — buttons and one accent line, never a background fill">
- Don't: <concrete misuse to avoid for THIS theme specifically>

### secondary (<hex>)
- When to use / Surface area / Don't — same structure

### accent (<hex>)
- When to use / Surface area / Don't — same structure

If the theme's palette genuinely only supports 2 usable chromatic roles (e.g. primary and accent are close variants of one hue), say so explicitly instead of forcing a 3-way split that doesn't exist in the data.

## When To Use
- Bulleted, concrete: content types, project genres, moods this theme is built for. Ground each bullet in something about *this* theme's actual construction (its background type, its typography pairing, its effects), not a generic "good for dashboards" line.

## When NOT To Use
- Bulleted, concrete: content/genres where this theme actively fights the content — explain the specific friction, not just "not a good fit."

## How To Use — Full Potential
- Which components/sections most showcase this theme, and why — cite actual class names from the preset's own HTML (e.g. `.tf-gradient-hero`, `.tf-badge-*`, `.tf-cards`).
- One "if you only do one thing" recommendation — the fastest way to make a page unmistakably read as this theme.

## Apply-Mode Notes
- Anything Path F/Path R harmonize steps (4a-4k in `modules/apply-mode-token-harmonize.md`) should weight differently for this theme specifically — e.g. "skip 4j entirely, this theme has zero gradients/glow by design" or "step 4a's >60%-primary rule doesn't apply, this theme only has 2 usable roles."
```

## Relationship to shared modules

- `modules/shared-color-slots.md` / `modules/shared-design-dna.md` define the *vocabulary* every theme is built from — read them for schema context, but don't restate their generic definitions here.
- `modules/apply-mode-token-harmonize.md` defines the *generic* harmonize rules that apply to every theme by default — this doc's Apply-Mode Notes section only needs to say something when this theme is an exception to those defaults.
