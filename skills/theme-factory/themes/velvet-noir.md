# velvet-noir

Dark Art Deco maximalism — old gold and deep crimson on near-black plum, disciplined by geometric diamond-lattice precision rather than [[nocturne-nouveau]]'s organic florality (same "dark ornate luxury" territory, opposite geometric philosophy: Deco's rigid diamonds vs. Nouveau's flowing curves).

## Core Concept
Near-black plum canvas (`#1A1018`) under a genuine diamond crosshatch lattice (38px, muted gold), Playfair Display's ornate high-contrast serif against Cormorant Garamond's refined light body. `primary` and `warning` share one hex (`#C9A84C` old gold) — this theme's "brand color" doubles as its caution signal, an unusual pairing that works because gold's role throughout is ceremonial/precious rather than purely decorative. Like `crypt-scholastic`, `shadows.colored` uses a hairline border-ring (`0 0 0 1px var(--color-border)`) instead of glow — restrained elevation despite the maximalist label.

## Color Role Guidance

### primary (`#C9A84C` old gold) — also `warning`
- When to use: the dominant precious-metal signal — primary buttons (`--gradient-button`, gold gradient), gradient text (`--gradient-text`, gold-dominant 3-stop), the diamond lattice pattern color, headline glow (`textShadow: 0 0 30px rgba(201,168,76,0.3)`).
- Surface area: generous — gold anchors the visual system throughout, appropriate for large structural use, not just accents.
- Don't: don't introduce a separate warning color — the collapse with primary is intentional; gold already carries "attend to this" weight ceremonially.

### secondary (`#8B1A4A` deep crimson)
- When to use: the "velvet" note — one gradient stop (`--gradient-accent` runs crimson→gold), a rich jewel-tone counterpoint to gold's brightness.
- Surface area: moderate — deep and saturated, evoking velvet drapery against the gold ornament.
- Don't: don't push crimson bright or pink-leaning — it needs to stay deep and desaturated to read as "velvet," not "hot pink."

### accent (`#E8C96A` brighter gold)
- When to use: the "highlight" register of primary — a lighter gold for emphasis within gold-dominant compositions (gradient text's brightest stop).
- Surface area: small — a tonal lift within the gold family, not a separate hue.
- Don't: don't treat accent as chromatically distinct from primary — like several themes in the catalog, it's a value-shift of the same gold, not an independent third color.

## When To Use
- Luxury, nightlife, jazz-age/Art Deco revival, or "old Hollywood glamour" content wanting genuine geometric Deco precision.
- Dark-mode products wanting maximalist gold ornament without the softer, organic register of [[nocturne-nouveau]].
- Content that benefits from restrained elevation (hairline border-rings, not glow) despite an otherwise rich, ornate palette.

## When NOT To Use
- Playful, casual, or approachable branding — Playfair Display's high-contrast drama and the near-black plum base are formal and dramatic.
- Content already using nocturne-nouveau elsewhere in the same project — both are dark gold-forward luxury themes; mixing them risks visual confusion (pick geometric Deco vs. organic Nouveau, not both).
- Light-mode contexts — no light variant; the deep plum base is structural.

## How To Use — Full Potential
- Keep the diamond crosshatch lattice strictly geometric (rigid 45°/−45° diagonal grid) — this is what separates velvet-noir from nocturne-nouveau's more organic radial mesh; don't substitute a soft/curved pattern.
- Use the border-ring technique (`shadows.colored: 0 0 0 1px var(--color-border)`) for cataloged/structured panels — a restrained alternative to glow that keeps the maximalist palette from tipping into gaudiness.
- Apply gold's headline text-shadow glow (`0 0 30px rgba(201,168,76,0.3)`) consistently on major headings — subtle enough to read as ambient shimmer, not garish neon.
- If only one thing: apply the gold gradient text treatment against the diamond-lattice dark background — the fastest way to signal velvet-noir's Deco-specific luxury register.

## Apply-Mode Notes
- Step 4a: preserve primary=warning — don't introduce a separate warning color during harmonize; gold's ceremonial weight already covers that role.
- Step 4d/4j: use the hairline border-ring technique for "colored shadow," not a glow — this theme is maximalist in ornament but restrained in luminescence, a distinction worth preserving during harmonize.
