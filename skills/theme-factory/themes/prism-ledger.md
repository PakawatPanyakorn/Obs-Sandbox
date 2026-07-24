# prism-ledger

Finance/accounting editorial luxury — forest green, amber, and magenta-rose prismatic gradients on warm pearl, disciplined by "no glow, editorial restraint" and genuine ruled-ledger/newspaper-column structure.

## Core Concept
Warm pearl canvas (`#F8F2EA`) with a fine 45° diagonal stripe pattern in forest green plus a 2-layer radial mesh (green + magenta), Playfair Display's ultra-bold 900-weight italic-capable display against Lora's warm italic body. Explicitly `luminescence: none` — per the theme's own notes, "no glow — editorial restraint" is a *design decision*, distinguishing prism-ledger from more maximalist prismatic themes like [[meridian-capital]] or [[nocturne-nouveau]]: same instinct toward tricolor gradients, but grounded entirely in flat, print-like restraint instead of glow or backdrop blur.

## Color Role Guidance

### primary (`#1A5C3A` forest green)
- When to use: the "ledger" anchor — primary buttons (`--gradient-button`, green-only gradient), the first stop in every multi-color gradient, structural trust signal (evokes accounting-ledger green).
- Surface area: generous — green leads visually, appropriate for headers, buttons, and the diagonal stripe pattern itself.
- Don't: don't add glow or backdrop blur to primary elements — this theme's discipline is explicitly glow-free; a lit-up green button contradicts the "editorial restraint" premise.

### secondary (`#C88020` amber)
- When to use: the middle gradient stop (`--gradient-text` runs green→amber→magenta), a warm mid-tone counterpoint between the cooler green and the hot magenta.
- Surface area: moderate — bridges the palette in gradients more than standing alone as a solid fill.
- Don't: don't treat secondary as interchangeable with `warning` (`#A86018`, a duller amber) — secondary is decorative/editorial, warning is a genuine caution state.

### accent (`#C83078` magenta-rose)
- When to use: the boldest, most "prismatic" note — gradient endpoints, the third stop in the tricolor border, a jolt of color against the otherwise warm, paper-toned palette.
- Surface area: small — the rarest of the three roles; its punch depends on scarcity.
- Don't: don't scale magenta to the same frequency as green — it should feel like a deliberate flourish, not a co-equal palette member.

## When To Use
- Finance/accounting editorial, annual reports, or "money as narrative" content wanting luxury without glow-driven flashiness.
- Content that benefits from genuine ledger/newspaper structure — ruled lines, multi-column layout, pull-quote sections (per `design.notes`).
- Print-adjacent or PDF-exportable content — since the theme has zero glow/blur/backdrop-filter dependency, it degrades perfectly to print.

## When NOT To Use
- Any content wanting glow, luminescence, or glassmorphic depth — those effects are explicitly absent by design; forcing them in breaks the theme's "editorial restraint" identity.
- Minimalist single-accent contexts — this is a genuine 3-hue gradient system; a project wanting one quiet accent color should look elsewhere.
- Digital-native, app-like UI wanting motion-heavy feedback — `motion.feel: subtle` and print-like flatness suit editorial reading, not interactive dashboards.

## How To Use — Full Potential
- Use the 3-stop gradient text (`green→amber→magenta`) on major headlines — it's the theme's signature prismatic move, achieved entirely through flat gradient-clipped text with zero glow.
- Lean on the diagonal stripe + radial mesh combination as the page's ambient texture — subtle enough to read as fine paper texture, not a loud pattern.
- Reserve the full tricolor gradient border for one ceremonial element (a pull-quote frame, a key figure) — consistent with the theme's overall discipline of restraint even within its prismatic identity.
- If only one thing: apply the 3-stop gradient-clipped text treatment to one Playfair Display headline — the fastest way to signal prism-ledger's "prismatic but restrained" identity.

## Apply-Mode Notes
- Step 4j: this theme is explicitly glow-free — never add glow, backdrop blur, or luminescent shadows during harmonize, even to "enhance" the gradient effects; flatness is the point.
- Step 4d: any hero/colored-section gradient should stay in the green→amber→magenta family — a single-hue treatment undersells the theme's prismatic identity, while adding a 4th hue breaks its discipline.
