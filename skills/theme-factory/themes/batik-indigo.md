# batik-indigo

A dye studio's working journal — rice-paper ivory, a single unbroken indigo line, and the fine crackle a resist leaves behind.

## Core Concept
The theme commits to one material metaphor and follows it through every token: `background.patternType: crosshatch` is two layered 45°/135° hairlines at 4% opacity, standing in for the crackle network wax leaves in real resist-dyed cloth, not a decorative pattern chosen for its own sake. Borders on cards, section dividers, and the header all render dashed (`border: 1px dashed var(--color-border)`) to suggest hand-stitching or a wax-drawn line — the one deliberate break from a plain hairline. Fraunces' warm optical-size quirks (`.bi-display`) sit against Source Serif 4's calmer long-form body, and every shadow is warm-brown-tinted (`rgba(42,32,22,…)`, built from the ink color) rather than neutral black, so even elevation stays inside the dyed-fabric palette. The `crafted` aesthetic and `handmade` personality tag aren't just labels here — they're the reason nothing in this theme glows, gradients, or moves quickly.

## Color Role Guidance

### primary (`#22355C`)
- When to use: the "cured" indigo — primary CTA (`.bi-btn-primary`), section headings (`.bi-h2`), the `Made to Order` badge. Dark enough that `textOnPrimary` needs a genuinely light value, not the page's own ivory background color repeated.
- Surface area: buttons, headings, and the badge family — never a large background wash, since real indigo dye lives in the cloth's lines and edges, not flat fills.
- Don't: don't lighten primary for a "softer" variant — the theme's only tint of it is `primaryLight`, used exclusively as a badge background, not as a substitute mid-tone.

### secondary (`#B5533C`)
- When to use: the rust/terracotta counterpoint — `.bi-btn-secondary`, italic subheads (`.bi-h3`), card eyebrow tags (`.bi-card-tag`). Reads as the "warm" half of the palette against primary's "cool" half.
- Surface area: comparable to primary in weight, appearing in roughly the same proportion across a page rather than as a rare accent.
- Don't: don't use secondary and primary side-by-side as adjacent solid fills without the ivory ground between them — the two-color contrast is meant to read as dye-on-cloth, which needs the pale ground as breathing room.

### accent (`#D1A23C`)
- When to use: the turmeric "third dye" — decorative diamond motifs (`.bi-motif-row`), rare highlight moments. The theme's palette genuinely supports only these three chromatic roles plus status colors; there's no fourth hue held in reserve.
- Surface area: small and occasional — a few motif marks, never a button or large fill.
- Don't: don't promote accent to a button or badge color; in this theme it's closer to a decorative thread than a functional UI color.

## When To Use
- Craft, heritage, artisan-commerce, or slow-editorial content — the demo copy (wax-resist process notes, dye-vat studio log, commission form) names the genre directly.
- Long-session reading surfaces that want warmth without becoming twee — `line-height: 1.65` and Source Serif 4 are tuned for paragraphs, not just headlines.
- Projects wanting a textile/handcraft register that isn't already covered by the library's cottagecore (`moss-cottage`) or vintage-naturalist (`tobacco-road`) themes.

## When NOT To Use
- Fast-interaction dashboards or data-dense UIs — `motionFeel: subtle`, dashed borders, and serif type are built for contemplative reading, not scanning.
- Tech-forward or futuristic content — there is no glow, gradient, or glass anywhere in this theme by design; it will read as a mismatch immediately.
- Alongside `moss-cottage` or `tobacco-road` in the same project — see `design.notes`; all three occupy "warm earthy handcraft" and will blur together without a strong reason to keep them visually separate.

## How To Use — Full Potential
- Lead with `.bi-header`'s dashed bottom border plus the `.bi-motif-row` diamond marks — that combination reads as "hand-finished document" before a single word is read.
- Use dashed borders (`border-style: dashed`) on any structural divider — cards, section titles, the header — rather than solid hairlines; it's the theme's most consistent and most load-bearing visual signature.
- Keep shadows warm-tinted (`rgba(42,32,22,…)`), never neutral gray — swapping in a default black box-shadow is the fastest way to make this theme look like generic light-mode editorial instead of dyed cloth.
- If only one thing: switch a card or section border from solid to dashed in the secondary rust color — that single change is the fastest way to make a block read as batik-indigo.

## Apply-Mode Notes
- Step 4j (gradients/glow/effects): this theme has zero gradients, glow, or glass by design — skip that step's harmonize work entirely rather than introducing a "subtle" version of any of them.
- Step 4c (radius/borders): don't normalize the dashed borders to solid during harmonize "for consistency" — the dashed treatment is the theme's core structural signature, not an inconsistency to fix.
- `textOnPrimary` (`#FDF8ED`) is a distinct near-white, not the page background color repeated — if a target file already defines a "white" text token, check it isn't accidentally identical to the page background before reusing it here.
