# aeroglass

Glass panels catching light over a sky-blue-to-lime gradient — the specific optimism of early-2000s consumer tech that believed software should look like it was made of water and light.

## Core Concept

Aeroglass commits to one idea: every surface is a curved sheet of wet glass with a light source above it. That's what `.ag-header::before`'s top-anchored radial highlight and the `.ag-bubble` elements are doing — they're not decoration scattered for texture, they're a single consistent light source (upper-left) that every glossy surface in the page answers to. The **glassmorphism** aesthetic here is doing real work, not just a frosted-panel trend: it's paired with **glossy** and **chrome** personality tags because the glass is meant to look wet and reflective (hard specular highlights), not matte-frosted like a modern iOS sheet. **Optimistic** and **aquatic** show up in the copy register (weather, sync, storage — "always up to date") rather than in any literal color choice.

## Color Role Guidance

### primary (#2E8FD6)
- When to use: the sync/connect CTA (`.ag-btn-primary`), active status badges, progress fills
- Surface area: ~10-15% of viewport — one hero button plus badge accents, never a full-bleed panel
- Don't: use as a card background — at full saturation it fights the glass-panel surfaces, which need to stay near-white to read as "glass over blue sky," not "blue card"

### secondary (#8CC63F)
- When to use: the lime end of gradient accents (`.ag-card-meter span`, `.gradient-accent`) and the secondary action button
- Surface area: small — gradient endpoints and one button, never a large fill (it reads as a status-green clash otherwise, since `success` is also green-family)
- Don't: pair directly adjacent to `success` (#2E9E5B) in the same component — they're close enough in hue that a viewer will read them as the same signal

### accent (#F2924B)
- When to use: sparingly, as the one warm counterpoint — a single badge, an alert stripe, never a button
- Surface area: under 5% — this theme is intentionally cool-dominant (sky blue + lime), so warm coral is a controlled interruption, not a third co-equal brand color
- Don't: use for large buttons or hero gradients — that would turn "cool glass with one warm spark" into an even three-way split, which flattens the "sky" identity

## When To Use
- Sync/status/media-control dashboards where "everything is connected and up to date" is the actual message — the widget cards (Cloud Storage, Now Playing, Weather Orb) are built for exactly that content shape
- Consumer-facing settings or device-pairing screens wanting a warm, approachable register instead of flat enterprise SaaS blue
- Any surface that can genuinely support `backdrop-filter: blur()` — the theme's identity depends on visible glass, so it needs real content or color underneath the panels to blur

## When NOT To Use
- Dense data tables or admin back-ends — the glass/bubble decoration competes with information density instead of supporting it
- Dark-mode-only products — this theme has no dark variant by design; it's a fixed daytime-sky world, not a token set meant to invert
- Content wanting a serious/financial/enterprise register — the glossy chrome reads as consumer and playful-optimistic, not authoritative

## How To Use — Full Potential
- Lead with `.ag-header` and its three `.ag-bubble` elements — that combination (top specular highlight + floating bubble highlights) is what makes a page unmistakably Aeroglass rather than generic "light blue gradient"
- `.ag-card` relies on `.ag-card::before`'s `var(--gradient-card)` overlay to get its glass sheen on top of a solid surface — don't strip that pseudo-element when reusing the card pattern elsewhere
- If you only do one thing: apply the `.ag-btn-primary` gradient-button treatment (white-to-blue vertical gloss with an inset top highlight) to the primary CTA — it's the single most recognizable "Aero" signature, more so than the background itself

## Apply-Mode Notes
- Step 4j (gradient-text headline check) is moot here by design — `gradients.text` is explicitly `"none"` and the hero heading uses a soft `text-shadow` instead, specifically to avoid the gradient-fill-headline anti-pattern. Don't introduce one when applying this theme.
- Step 4a's primary-dominance rule needs a tighter cap than usual: keep primary under ~15% of viewport, since the theme's real identity signal is the *background* glass gradient, not a primary-color fill — over-using primary makes it read as a generic blue SaaS theme instead of Aeroglass specifically.
- This theme has no dark-mode token set (`:root[data-theme="dark"]` block) — if the target file has a mode toggle, either hide it or leave the existing dark tokens untouched rather than inventing a "dark glass" variant that isn't part of this preset's concept.
