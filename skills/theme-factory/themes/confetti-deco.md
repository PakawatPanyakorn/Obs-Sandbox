# confetti-deco

A cream terrazzo slab flecked with pop-pink, mint, and butter-yellow chips, cut into square-cornered paper shapes that cast a hard flat shadow instead of a soft one.

## Core Concept

Confetti Deco is Memphis-Milano postmodernism run through a market-stall lens: **playful** in palette, but structurally closer to a cut-paper sticker than a rounded toy. The `.cd-swatch`, `.cd-card`, and `.cd-btn` elements all share the same construction — a 3px black border (`--color-border`) plus a hard, zero-blur offset shadow (`--shadow-md: 4px 4px 0 #17161A`) — which is what separates **terrazzo/confetti** from the softer pastel-blob world of `cloud-candy`. The ten fixed confetti dots in the page background aren't a repeating pattern; they're placed once, irregularly, the way real terrazzo chips fall in a poured slab. Bangers' comic-poster inline stroke gives the display type the same "printed poster, slightly imperfect" energy as the squiggle dividers, rather than a clean geometric sans.

## Color Role Guidance

### primary (#F2417A)
- When to use: the main CTA (`.cd-btn-primary`), the "New Drop" badge, price emphasis
- Surface area: 10-15% of viewport — one button plus a couple of tags, never a full card fill
- Don't: use as a large background block — at that scale it competes with the terrazzo confetti dots, which already carry pink as one of four scatter colors

### secondary (#FFD93D)
- When to use: the secondary action button and one confetti scatter color
- Surface area: small, high-contrast pops — text on yellow needs to stay dark (`--color-text`), never `textOnPrimary`
- Don't: pair yellow text on a light cream background — it's the one combination in this palette that fails the 4.5:1 contrast rule

### accent (#3EC6BE)
- When to use: card tag chips (`.cd-card-tag`) and one confetti scatter color
- Surface area: small labels only — this is a cooling counterpoint to the pink/yellow warmth, not a third equal brand color
- Don't: use accent and secondary together on the same element — both are light/mid-value and the contrast between them reads as muddy rather than crisp

## When To Use
- Market-stall, indie-craft, or zine-adjacent retail content where "handmade and slightly crooked" is a feature, not a bug — the product cards (tote, coasters, zine) are built for exactly that inventory shape
- Playful consumer content that wants postmodern/Memphis energy without going fully rounded-pastel-toy (that's `cloud-candy`'s territory) — pick this when the brand needs a harder, more graphic edge
- Poster, flyer, or event-microsite content where a hard offset shadow and squiggle divider can carry real visual weight

## When NOT To Use
- Alongside `cloud-candy` or `bauhaus-geometry` in the same project — all three sit in adjacent playful/geometric territory and would blur together; pick one
- Dense dashboards or data tables — the confetti scatter and 3px borders on every element get visually loud fast at high information density
- Trust-driven B2B/financial content — the hand-cut, deliberately-imperfect construction reads as craft-fair, not credible-institution

## How To Use — Full Potential
- Lead with the `.cd-squiggle` SVG directly under the hero heading and the confetti-dot background together — that pairing (hand-drawn line + terrazzo scatter) is the fastest way to read as Confetti Deco rather than generic Memphis
- `.cd-card` and `.cd-btn` both depend on the same offset-shadow formula (`border` + `box-shadow` with matching hex, zero blur) — keep that formula consistent across any new component, since a blurred shadow on just one element breaks the "cut paper" illusion
- If you only do one thing: give every interactive surface a 3px solid black border plus a 4px hard offset shadow that lifts by translating -2px/-2px on hover (see `.cd-btn-primary:hover`) — that single treatment is the theme's signature more than any individual color

## Apply-Mode Notes
- Step 4a's primary-dominance rule applies loosely here — this palette leans on four roughly-equal scatter hues (pink/yellow/mint/ink) rather than one dominant primary, so "introduce a counterpoint above 60%" rarely triggers; watch instead that no single confetti hue creeps past ~15% of viewport.
- Step 4j (gradient/glow check) can be skipped entirely — `gradients` and `effects.glassBlur`/`glowBlur` are all `none`/`0` by design; this theme has zero soft effects, only hard flat ones.
- When harmonizing borders (step 4d-ish), don't soften the 3px black border to a hairline — a thin border on this theme reads as an unfinished version of `bloc-brutus`/`bauhaus-konstrukt` rather than as Confetti Deco's own cut-paper identity.
