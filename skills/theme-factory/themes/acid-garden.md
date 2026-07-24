# acid-garden

Chromatic overload used as a controlled instrument, not a mistake — three hues that "should never coexist" (hot magenta, electric blue, acid lime) held together by hard-edged offset shadows and rigorous rounded-pill geometry.

## Core Concept
A mint-cream canvas washed in a 4-layer radial gradient mesh, topped with a heavy geometric display face (Unbounded, 900wt) and dual/triple offset "sticker" shadows (`--shadow-colored: 6px 6px 0 #FF0099, -3px -3px 0 #0099FF`). The theme's discipline is that every clash is deliberate and repeated consistently (same three-hue rotation everywhere) rather than randomly colorful — it reads as "energetic disorder controlled with obsessive precision," not noise.

## Color Role Guidance

### primary (`#FF0099`)
- When to use: the loudest CTA and the color every gradient (`--gradient-text`, `--gradient-button`, `--gradient-hero`) resolves toward — `.tf-btn-primary`, `.tf-header h1`'s gradient-clip text.
- Surface area: large and confident — this theme wants primary visible, not restrained; hero headline, main CTA, card accent dots (`.pulse`).
- Don't: don't apply primary as a flat, shadowless fill — every primary surface in this theme carries `--shadow-colored` or a gradient; a flat magenta block reads as an unfinished import from a different theme, not as this one.

### secondary (`#0099FF`)
- When to use: the second voice in every multi-color composition — `.tf-btn-secondary`, the counter-shadow color in `--shadow-colored`'s offset, the middle stop in `--gradient-text`.
- Surface area: buttons, tags (`.tf-tag-blue`), the second offset shadow layer — always paired with primary, rarely solo.
- Don't: don't let secondary appear without primary or accent nearby — this theme's whole effect depends on the three-hue rotation being visible together, not spread thin across unrelated sections.

### accent (`#AAFF00`)
- When to use: the "shock" note — third gradient stop, third shadow offset, the lime tag (`.tf-tag-lime`). It's what turns a magenta/blue duo into the theme's signature trio.
- Surface area: small, sharp hits — never a large fill (acid lime at scale reads as a warning color, not a brand color).
- Don't: don't substitute accent for success/warning states — the theme already has dedicated `success`/`warning`/`error` slots; accent is purely decorative chromatic punctuation.

## When To Use
- Fashion, motion-design, or creative-studio portfolios that want to signal "unafraid of color" as a positioning statement — the theme's own demo copy ("we design things that shouldn't work — and they do") is the target voice.
- Youth-skewing consumer brands, event/festival microsites, anything where "loud" is the point, not a risk.
- Content that can carry offset "sticker" shadows and rounded-pill buttons without looking like a mismatched sticker sheet — needs genuinely playful copy to match the chrome.

## When NOT To Use
- Any B2B, financial, healthcare, or trust-signaling context — the deliberate clash (`shadows.colored`, the 4-layer gradient mesh) reads as unserious by design; that's the whole point, and it cannot be dialed back without becoming a different theme.
- Long-form reading content — `headingWeight: 900` and gradient-clipped text (`-webkit-background-clip: text`) at body-copy scale hurts legibility fast; this theme is built for short, punchy surfaces, not paragraphs.
- Accessibility-sensitive contexts without a hard look at contrast — `textOnPrimary: #EDFCE8` on `#FF0099` and gradient text clipping both need explicit verification per use, they aren't guaranteed-safe combinations.

## How To Use — Full Potential
- Lead with `.tf-header`'s full combo: `--gradient-hero` background, `border-image: var(--border-gradient) 1` top strip, and gradient-clipped `<h1>` text — this three-layer stack (gradient bg + rainbow top edge + gradient text) is the theme's signature move and reads as generic "colorful theme" if any one layer is dropped.
- Use `.tf-card::before`'s 4px rainbow top strip on every card, not just the hero — it's what makes a card grid read as "this theme" rather than a random light theme with bold colors.
- Pill-shaped buttons (`--radius-button: 999px`) paired with `--shadow-colored`'s dual offset are the theme's button signature — a square/rounded-rect button with a single drop shadow undersells it.
- If only one thing: apply `--gradient-text` + `-webkit-background-clip: text` to one headline — it's the fastest, cheapest way to make a page unmistakably acid-garden.

## Apply-Mode Notes
- Step 4a (color distribution) should target genuine 3-way rotation, not a 60/30/10 primary-dominant split — this theme is built around primary/secondary/accent appearing together in the same shadow/gradient stacks, so the generic ">60% primary → introduce counterpoint" framing undersells how much secondary/accent presence this theme actually wants.
- Step 4j (gradients/glow/effects) is unusually load-bearing here — don't treat `--gradient-hero`/`--gradient-text`/`--shadow-colored` as optional polish; skipping them is the single most common way an apply of this theme ends up looking like a generic light theme with the wrong hex codes.
- Step 4h (contrast) needs explicit re-verification wherever gradient-clipped text or `textOnPrimary` on raw `primary` is introduced — this theme's high-chroma pairings aren't guaranteed WCAG-safe out of the box.
