# tobacco-road

A naturalist's field journal — aged vellum with SVG foxing-noise grain, tobacco/vermillion/amber ink tones, EB Garamond unified across every text role, "only ink on vellum."

## Core Concept
Aged-paper canvas (`#F2E4C4`) with genuine fractal-noise grain simulating foxing (age spots) on real vellum. EB Garamond serves as both display AND body font — per `design.notes`, "unified," evoking a single handwritten/typeset journal voice rather than a designed display/body contrast. `luminescence: none` and `gradientBorder: none` keep effects restrained; the gradients that do exist (`--gradient-hero`, `--gradient-button`, `--gradient-text`) are all tonal, staying within the tobacco-brown/vermillion earth-tone family rather than introducing unrelated hues — consistent with "ink on vellum," not a modern multi-color brand gradient.

## Color Role Guidance

### primary (`#5C3D11` tobacco brown)
- When to use: the dominant "ink" tone — primary buttons (`--gradient-button`, a brown-only tonal gradient), structural text, the base of the earthy triad.
- Surface area: generous — tobacco brown anchors the visual system, appropriate for large use as the theme's core ink color.
- Don't: don't push primary toward a cooler or more saturated brown — the warmth and desaturation are what read as "aged," not modern.

### secondary (`#8B2500` vermillion) — shares hex with `error`
- When to use: a bold accent ink — one gradient stop (`--gradient-text` runs vermillion→amber, `--gradient-accent` runs brown→vermillion), a naturalist-journal "red ink" annotation color. Secondary and error share this hex.
- Surface area: moderate — a genuine second ink color, bolder than primary but still within the earthy palette.
- Don't: don't treat secondary as purely decorative — since it doubles as `error`, using it heavily for non-error emphasis may create ambiguity; reserve its boldest applications for genuinely important marks.

### accent (`#C8860A` amber)
- When to use: the brightest ink in the palette — gradient endpoints, a warm highlight against the aged paper.
- Surface area: small — a highlight note, not a fill.
- Don't: don't confuse accent with `warning` (`#B87010`, a similar but distinct duller amber) — accent is decorative/journal ink, warning is a genuine caution state.

## When To Use
- Natural history, field-journal, vintage-literary, or archival naturalist content — the theme's own vocabulary (aged vellum, foxing, naturalist aesthetic) is literal.
- Long-form editorial content benefiting from unified Garamond typography and generous line-height (`1.72`) for genuine readability.
- Content wanting warmth and age without glow, gradient maximalism, or modern digital polish.

## When NOT To Use
- Modern, digital-native, or tech-forward content — every choice (aged paper texture, unified serif, tonal-only gradients) resists a contemporary read.
- Content needing crisp, high-contrast, or vibrant color — the entire palette is deliberately warm, desaturated, and paper-toned.
- Dark-mode contexts — no dark variant; the aged-vellum base is structural.

## How To Use — Full Potential
- Use EB Garamond for literally everything, including what would normally be a display face elsewhere — the "unified voice" is a deliberate simplification that reads as authentic field-journal writing, not an oversight to "improve" with a separate display font.
- Keep the fractal-noise grain visible across the full page — it's what sells "aged vellum" over "beige background," and should feel like paper texture throughout, not a hero-only effect.
- Reserve tonal (single-hue-family) gradients for hero/button treatments — introducing an unrelated cool hue into any gradient breaks the "ink on vellum" restraint.
- If only one thing: apply the noise-grain aged-paper background behind Garamond body text — the fastest way to signal tobacco-road's naturalist-journal register.

## Apply-Mode Notes
- Step 4b (font mapping): map both display and body font roles to the same serif (EB Garamond) — introducing a separate display face during harmonize breaks the "unified voice" premise.
- Step 4d: any hero/section gradient should stay tonal (within the brown/vermillion/amber family) — avoid introducing a cool or unrelated hue even for visual variety.
