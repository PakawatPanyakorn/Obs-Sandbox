# prussian-blueprint

A pre-CAD architect's working drawing — Prussian blue ground, white chalk-line UI, where the interface chrome itself IS the annotation system (leader lines, dimension ticks, callout bubbles), not decoration applied on top of it.

## Core Concept
Deep Prussian-blue canvas (`#003153`) under a genuine 3-layer hierarchical drafting grid — 8px sub-grid at 3.5% opacity, 40px medium grid at 8%, 160px major grid with dimension ticks at 15%. Share Tech Mono throughout (even the display face fallback) plus Rajdhani's condensed technical sans. `gradients.*: none`, `luminescence: none`, `borderRadius: 0px` absolute — this is a "line weights only" theme; every visual distinction comes from stroke opacity/width, never fill, blur, or color saturation shifts.

## Color Role Guidance

### primary (`#FFFFFF` chalk white)
- When to use: this is the "drawing" itself — text, primary UI, structural lines (`callout-marker`, `leader-label`, `annotation-grid`). Like `darkroom-safelight`, this theme inverts the usual convention: primary is neutral (white chalk), not a saturated brand hue.
- Surface area: everywhere the "drawing" lives — generous, expected, not restrained.
- Don't: don't treat primary as a "bold accent" needing its own saturated color — it's meant to read as chalk/pencil on blueprint paper, functionally monochrome against the blue ground.

### secondary (`#CC2222` annotation red)
- When to use: the "red pen" correction/flag color — `--shadow-colored` uses secondary red exclusively (`0 0 0 1px #CC2222`), marking revision or attention-needed elements.
- Surface area: small, deliberate — a red-ink annotation mark, not a broad UI color.
- Don't: don't use secondary for routine UI — reserve it specifically for "flagged/revised" semantic meaning, echoing how a red pen marks up a blueprint.

### accent (`#FFD700` drafting gold) — shares hex with `warning`
- When to use: measurement/dimension call-outs, or genuine warning states (they share one hex) — dimension ticks, a specific "measure this" or caution marker.
- Surface area: small — thin lines and markers, never a fill.
- Don't: don't use accent as decorative — its dual role with warning means it should always carry at least a hint of "pay attention to this measurement/issue."

## When To Use
- Architecture, engineering, CAD-adjacent, or technical-drafting content wanting genuine blueprint authenticity rather than a generic "blue and white grid" gesture.
- Products wanting an annotation-heavy UI language — leader lines, callout bubbles, dimension ticks as first-class interface elements, not afterthought tooltips.
- Content with real measurement/spec data that benefits from the theme's line-weight-only hierarchy system.

## When NOT To Use
- Any content wanting warmth, color richness, or soft shapes — zero gradients, zero radius, and a two-tone (white-on-blue) palette are severely restrained by design.
- Content without genuine annotation/callout needs — the leader-line/dimension-tick UI language is the theme's core value; without real spec/measurement content to annotate, it's just a blue grid.
- Light-mode or bright contexts — no light variant; the deep Prussian-blue ground is structural to the entire concept.

## How To Use — Full Potential
- Use `.callout-marker`/`.leader-label`/`.annotation-grid` as first-class UI components, not decoration — real leader lines pointing from labels to the elements they describe, in the style of an actual annotated drawing.
- Rely entirely on line weight and opacity (per the 3-layer grid's 3.5%/8%/15% opacity steps) to establish hierarchy — never reach for a fill color or shadow blur to differentiate importance.
- Reserve secondary red exclusively for flagged/revised content, mirroring a real blueprint's red-pen correction marks.
- If only one thing: add a callout marker with a leader line pointing to a labeled element — the single fastest way to make a page read as prussian-blueprint rather than a generic dark-blue theme.

## Apply-Mode Notes
- Step 4a: preserve primary-as-neutral-white — don't treat it as an opportunity to introduce a saturated "brand" color during harmonize; white chalk-on-blue is the entire premise.
- Step 4d/4j: zero gradients, zero radius, zero glow by design — any harmonize step touching hero/colored-section treatment must stay flat with hairline borders only.
- Line-weight hierarchy: when harmonizing a target's existing elevation/shadow system, replace blur-based shadows with the `0 0 0 1px rgba(255,255,255,*)` border-ring pattern this theme uses instead.
