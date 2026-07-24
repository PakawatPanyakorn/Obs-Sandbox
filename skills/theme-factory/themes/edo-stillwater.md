# edo-stillwater

Ukiyo-e woodblock formality rendered as ink on handmade paper — Prussian blue (gunjō) against cool washi, with the literal laid-and-chain-line texture of real Japanese papermaking, not a generic "Japanese-inspired" pastiche.

## Core Concept
Cool washi-paper canvas (`#EAECF0`) with an authentic `washi-laid` pattern — horizontal laid lines every 24px, vertical chain lines every 72px, replicating the bamboo-mold impression of handmade kozo paper. Cormorant Garamond's refined display serif against Libre Baskerville body evokes "Hiroshige stillness." Despite `luminescence: none` and no glow anywhere, the theme does have a genuine 3-stop hero gradient (`#1E3A5F → #2B4F7A → #3A6490`, all Prussian-blue tones) — the only gradient permitted is a tonal deepening within one hue family, never a multi-hue blend.

## Color Role Guidance

### primary (`#2B4F7A` Prussian blue / gunjō)
- When to use: the dominant ink tone — hero gradient, primary buttons (`--gradient-button`, blue-only gradient), headline text-gradient (paired with accent jade).
- Surface area: generous — this is the theme's core "ink" color, appropriate for large structural use, not a restrained accent.
- Don't: don't lighten primary into a pastel — gunjō blue's depth is the point; keep it saturated and dark even in supporting UI.

### secondary (`#4A6E9A` lighter gunjō)
- When to use: a tonal step lighter than primary — secondary buttons, supporting UI that should feel like the same ink at lower concentration, not a different color.
- Surface area: moderate — reads as "primary, one wash lighter," maintaining the single-hue-family discipline.
- Don't: don't treat secondary as chromatically distinct from primary — they're the same blue family; use secondary specifically where a lighter *value* of the same ink is wanted.

### accent (`#5A8878` celadon jade)
- When to use: the one genuine hue departure — gradient endpoints (`--gradient-text`, `--gradient-accent` both run blue→jade), a single moment of "misty mountain" green against the dominant blue.
- Surface area: small — a counterpoint note, not a co-equal color; the theme's stillness depends on jade staying rare.
- Don't: don't scale jade up to primary's frequency — its value is specifically as the *one* departure from blue, evoking distant landscape rather than becoming a third busy color.

## When To Use
- East Asian art/culture content, calligraphy, tea/ceremony, minimalist Japanese-aesthetic products wanting genuine material authenticity (real washi paper construction) over generic "zen" cliché.
- Formal, contemplative editorial content — long-form writing benefits from the theme's restraint and generous line-height (`1.72`).
- Content wanting a cool, composed, "still water" register — distinct from warmer minimalist themes.

## When NOT To Use
- Energetic, playful, or maximalist content — every design choice (single-hue-family palette, subtle shadows, no glow) is built around stillness and restraint.
- Content needing more than 2 chromatic roles (blue-family + jade) — this theme's whole discipline is its narrow palette; forcing in a third independent hue breaks the "gunjō ink + one accent" premise.
- Fast, punchy interactions — `motion.feel: subtle`, `durationSlow: 500ms` is tuned for calm, deliberate transitions.

## How To Use — Full Potential
- Lead with the 3-stop tonal hero gradient (`#1E3A5F → #2B4F7A → #3A6490`) — this single-hue deepening, not a multi-color blend, is what keeps the theme feeling like ink rather than a modern brand gradient.
- Reserve celadon jade exclusively for the blue→jade gradient pairing (`--gradient-text`, `--gradient-accent`) — introducing it as a standalone fill color outside that pairing dilutes its "distant landscape" role.
- Let the washi laid/chain-line background remain visible at low opacity across full-page reading surfaces — it's a paper-grain effect meant to be felt more than seen, and works best behind generous whitespace, not busy UI.
- If only one thing: apply the single-hue-family gradient (primary→secondary tonal shift) to one hero or headline element — the fastest way to signal ink-on-paper depth without introducing a second hue.

## Apply-Mode Notes
- Step 4a: keep primary/secondary within one hue family (both Prussian blue, different values) — don't treat secondary as an opportunity to introduce a distinct color during harmonize.
- Step 4d: any hero/colored-section gradient should stay single-hue-family (tonal) unless specifically transitioning to accent jade — multi-hue gradients elsewhere break the ink-wash discipline.
