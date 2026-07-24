# slide-rule-of-thirds

**Archetype:** slide-rule-of-thirds · **Family:** grid-discipline

## Core Concept
A single slide's visual anchor occupies one-third of the frame; supporting text occupies the remaining two-thirds. This archetype's entire reason to exist is replacing the centered-title-plus-bullet-list slide — the single most common bad slide pattern. The imbalance is the message: the 1/3 visual gives the eye an anchor before it reads, and the 2/3 width structurally caps how much text can fit, which is exactly what prevents "five bullets, none of them the point."

## When To Use
- A single-argument slide in a talk — one claim plus one or two sentences of reasoning ("why we chose X").
- "Here is the one result that matters" slides in a data readout or board deck — one exhibit, one interpretation, never a data table repeating the chart's own numbers.
- A roadmap, feature-launch, or "what shipped this quarter" slide built around one featured thing plus a short supporting list.

## When NOT To Use
- Anywhere the body copy needs more than ~40-60 words or more than 2-4 bullet lines to make its point — that's two slides, never smaller type or a fifth bullet.
- Content wanting two charts shrunk into the one-third visual slot to fit more data — that's the dashboard-trope this archetype is built to avoid; one exhibit per slide, always captioned and interpreted in the body.
- A body region that wants to become a mini card grid of its own — it stays a plain rule-and-whitespace list, the same card-grid-default discipline layout-factory applies everywhere, even inside this archetype's supporting region.

## Region / Component Guidance
- **lead** (1/3, `1 / 5`): the visual anchor — the one image, chart, diagram, or big stat this slide is actually about. Never a decorative stock photo filling empty space; if there's nothing real to show, use the textHeavy adaptation (minimal icon/stat) instead. Carries any figure-number tag overlaid at the bottom of the visual pane itself — there's no vertical room to stack a caption beneath it in a fixed 16:9 frame.
- **body** (2/3, `5 / 13`): one headline plus a short list (2-4 lines) or 40-60 words of prose — never both at once. Two-thirds width at slide-reading distance is deliberately too narrow for five bullets; if content needs more room, that's a second slide, not smaller type. Carries at most one stat callout/pull quote per slide.

## Content-Type Notes
- **textHeavy**: visual third becomes a minimal diagram, icon, or single oversized stat instead of a photo — the eye still gets an anchor without a real image. Body caps at one short headline plus 3-4 lines of prose, no bullet list at all. Don't let the body creep past ~40-60 words to compensate for a thin visual.
- **chartHeavy**: visual third becomes the single chart/exhibit the slide exists to show, captioned like a numbered figure; body holds the headline finding plus one or two numbered takeaways.
- **cardOrListHeavy**: visual third becomes a single flagship item's image/icon; body becomes a short list of 3-5 items, name plus one line each — since two-thirds width at reading distance can't hold full descriptions.

## Medium Notes
- Presentation: this composition IS a slide master, not an adaptation of one — lead bleeds to the frame edge at full slide height, no letterboxing inside the slide; body is vertically centered.
- Print: one slide equals one page in a printed handout; aspect-ratio stays locked at 16:9 regardless of paper orientation, centered with even letterboxed margins rather than stretched to fill a taller sheet.
- Markdown: degrades to an image reference (or fenced quote/code block standing in) followed by a short paragraph or 2-4 item list — reading order survives but the 1/3:2/3 ratio itself is lost; note it in a caption if the proportion matters to the argument.

## Pairing Notes
- `synthwave-84` — bold, confident visual-anchor register: hot-pink primary and neon glow shadows give the lead third real presence at glance-from-the-back-of-the-room scale.
- `ultraviolet-rave` — an even more maximalist register (4-layer UV radial glow, Megrim geometric display), proving the archetype survives an extremely loud visual anchor without the 2/3 text region getting overwhelmed.
