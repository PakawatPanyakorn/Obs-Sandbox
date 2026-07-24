# vellum-codex

A medieval illuminated manuscript rendered with actual period-accurate pigments — ultramarine (historically the most expensive blue, ground from lapis lazuli), cinnabar red, and true gold leaf — not a generic "old book" palette.

## Core Concept
Warm parchment canvas (`#F4EDD8`) with fractal-noise grain simulating vellum/foxing texture, Uncial Antiqua's genuine manuscript-hand display face against IM Fell English's antique body serif at spacious density (`density: spacious`, `lineHeight: 1.8`) evoking hand-copied text with generous margins. `gradientBorder: linear-gradient(90deg, #1A2FA8, #D4A800, #A82020)` — ultramarine, gold, cinnabar — is a direct reference to illuminated capital letters and manuscript border decoration, the single place all three "pigments" appear together.

## Color Role Guidance

### primary (`#1A2FA8` ultramarine)
- When to use: the "most precious" pigment — primary buttons (`--gradient-button`, a deep blue gradient), the anchor of the gradient border. Historically, ultramarine was reserved for the most important figures/elements in a manuscript (often the Virgin Mary's robe) — use primary similarly, for the single most significant element per view.
- Surface area: moderate to generous — precious but not overused, consistent with how real illuminators rationed their most expensive pigment.
- Don't: don't dilute ultramarine into a pale blue — its value (both historically and in this theme) depends on saturation and depth.

### secondary (`#A82020` cinnabar red)
- When to use: rubrication — historically, red ink/pigment ("rubric") marked section headings and important instructions in manuscripts. Use secondary the same way: section markers, emphasis, the gradient border's third stop.
- Surface area: moderate — a genuine second pigment, used for structural emphasis (headings, markers) rather than large fills.
- Don't: don't use cinnabar as a general "warm accent" divorced from its rubrication role — it reads most authentically when marking structure (headers, section starts), echoing real manuscript rubrics.

### accent (`#D4A800` gold leaf)
- When to use: illumination — the brightest, most decorative pigment, gradient text (`--gradient-text`, gold-dominant 3-stop), the gradient border's middle stop.
- Surface area: small — gold leaf was applied sparingly and dramatically in real manuscripts (illuminated capitals, halos); mirror that scarcity here.
- Don't: don't confuse accent gold with `warning` (`#A07820`, a duller ochre) — accent is precious illumination, warning is a genuine caution state.

## When To Use
- Medieval, religious/sacred, historical, or rare-manuscript content wanting genuine period-pigment accuracy rather than generic "old paper" styling.
- Literary or archival editorial content that benefits from spacious, hand-copied-feeling typography and generous line-height.
- Content with a genuine "illuminated" moment to spotlight — a single hero heading, a decorated initial capital — where the gold/ultramarine/cinnabar combination can shine.

## When NOT To Use
- Modern, digital-native, or minimal content — the entire theme is built around manuscript-production authenticity.
- Content needing more than the 3-pigment discipline — a taxonomy needing 4+ distinguishable hues has nowhere to go without diluting the historical-pigment premise.
- Fast-paced or information-dense UI — `density: spacious` and generous line-height are built for slow, contemplative reading.

## How To Use — Full Potential
- Use the 3-color gradient border (ultramarine-gold-cinnabar) specifically on illuminated-capital-style elements — a large decorated first letter, a hero panel border — echoing real manuscript illumination rather than a generic UI border.
- Reserve cinnabar/secondary for rubrication — section headers and structural markers — rather than general emphasis, for historical authenticity.
- Keep gold leaf/accent rare and dramatic, applied to the single most "illuminated" moment per page.
- If only one thing: apply the gold gradient text treatment to a single major heading, framed by the tricolor border — the fastest way to evoke an illuminated manuscript capital.

## Apply-Mode Notes
- Step 4a: map secondary/cinnabar specifically to headers and section markers (rubrication), not general accent use — this is a more historically specific role than a typical "secondary" color.
- Step 4j: zero glow/luminescence by design — this theme's richness comes from pigment saturation and the tricolor border, not light effects; don't add glow during harmonize.
