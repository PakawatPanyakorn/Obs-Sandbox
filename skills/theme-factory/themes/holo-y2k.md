# holo-y2k

A pearl-lavender profile page with exactly two holographic moments, not a hundred — the discipline that separates a real Y2K sticker board from a generic gradient-mesh hero.

## Core Concept
The theme's central bet is restraint against its own reference material: real early-2000s holo stickers are loud everywhere, but a page that's loud everywhere reads as the generic "AI aurora blob mesh" tell instead of anything Y2K-specific. So the background stays a near-solid pearl (`#F6F1FB`) with fine grain and one soft 2-stop sheen (`background.notes` documents this choice explicitly), and the actual 3-stop violet→cyan→pink gradient (`--gradient-button`/`--gradient-text`/`gradientBorder`) is rationed to exactly two places: the primary CTA and the wordmark chip. Lilita One's bold rounded-slab caps give headlines a bubble-letter, poster-sticker weight; Quicksand's soft geometric body keeps paragraphs legible. `borderStyle: subtle` and `radius-card: 20px` complete the "everything is a rounded sticker" feel without needing every surface to glow.

## Color Role Guidance

### primary (`#9B5DE5`)
- When to use: the CTA gradient's anchor stop, `.hy-h3`/subheads, the `New Sticker` badge. It's the "main" holo hue.
- Surface area: buttons and small accents — never a full-section fill; at page scale this violet reads flat and loses the iridescent effect that only shows up in a gradient or small chip.
- Don't: don't use primary alone as a hero background — that's exactly the generic-gradient-hero pattern this theme is built to avoid. Pair it with the other two stops or don't use it as a fill at all.

### secondary (`#38BDF8`)
- When to use: the middle gradient stop and its own badge (`Trade Pending`) — the "cooler" counterpoint to primary and accent.
- Surface area: comparable to primary, always appearing alongside it in the gradient rather than as an independent flat fill on its own.
- Don't: don't strand secondary as the only accent on a page — it's built to be one-third of a trio, not a standalone brand color.

### accent (`#FF6FB0`)
- When to use: the gradient's warm end, card tags (`.hy-card-tag`), the featured-card foil border (`.hy-card--featured::before`).
- Surface area: small text and thin foil borders — like primary, a full accent-pink background fill undersells the theme's iridescent premise.
- Don't: don't apply accent as a solid badge or button fill on its own; it only reads as "holo" in combination with the other two hues.

## When To Use
- Consumer/social products, rewards or collectible UIs, playful profile pages — the demo content (sticker board, guestbook, trade status) names the genre directly.
- Any page that wants a Y2K-nostalgic, sticker-sheet feel without becoming a literal blob-mesh gradient background.
- Light-mode-only consumer surfaces that want one concentrated moment of iridescence rather than constant shimmer.

## When NOT To Use
- B2B/financial/trust-driven content — the bubble-letter display face and holo foil read as consumer-playful, not credible for enterprise or money contexts.
- Dark-mode products — this theme has no dark variant; the pearl ground and dark-plum text are load-bearing to the "holographic sticker on paper" read.
- Pages that already have a strong gradient hero elsewhere in the brand — stacking this theme's restrained 2-stop grain with another gradient-heavy hero doubles up on a look this theme specifically tries not to be.

## How To Use — Full Potential
- Lead with `.hy-header`'s `.hy-wordmark` chip — a small pill with the gradient clipped to text — paired with a plain-ink `<h1>` right below it. That contrast (one tiny holo moment, one solid headline) is the theme's whole thesis in miniature.
- Use `.hy-card--featured`'s foil-border technique (gradient background + mask composite for a thin ring) on exactly one "hero" item per collection grid — it marks something as special specifically because the other cards stay plain.
- Keep badges as tinted pill fills (`.hy-badge-*`, colored text on a ~12% opacity wash), never solid holo-gradient fills — that would spend the theme's one bold gesture on five small chips instead of one CTA.
- If only one thing: apply `--gradient-button` to a single pill-shaped CTA with `box-shadow: var(--shadow-colored)` — that's the fastest way to make an element unmistakably read as holo-y2k without touching anything else.

## Apply-Mode Notes
- Step 4a's `>60%-primary` rule doesn't map cleanly here — think of primary/secondary/accent as three inseparable stops of one gradient, not three independently distributable roles; don't split them across unrelated page regions.
- Step 4j (gradients/glow) needs the opposite of the usual caution: don't remove the gradient entirely during harmonize (that would generic-ify the theme into "pastel SaaS"), but also don't spread it beyond the CTA/wordmark — the two-place rule is the theme's core discipline, not an arbitrary limit.
- Text-on-color is dark plum (`#2B1F3D`), not white — if a harmonize step defaults to white text on a primary/accent fill, that's a contrast regression specific to this theme's mid-brightness palette.
