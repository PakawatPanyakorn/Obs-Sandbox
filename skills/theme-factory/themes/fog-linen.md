# fog-linen

A room with one lamp on — the library's first theme that gets quieter the longer you look at it.

## Core Concept

Fog Linen commits to a single restraint: one hue (taupe-clay, ~30° warm neutral) carried at three lightness steps instead of three different colors. `primary` (#8B7E6A), `secondary` (#6E6255), and `accent` (#A69783) are the same family, not a triad — that's what `personality: ["calm", "soft", "warm"]` actually cashes out to in code, not just mood words — `calm` here means the hygge/unhurried register, carried by tonal restraint rather than by any single token. Elevation is `flat` by policy: every card in `.fl-card-grid` is a horizontal rule and baseline-aligned row, not a boxed panel, because a "quiet room" doesn't stack shadows to create depth — it uses whitespace and a 1px `--color-border` hairline instead. The only texture in the whole theme is a 4px diagonal crosshatch at 5% opacity, deliberately calibrated to be felt more than seen.

## Color Role Guidance

This theme genuinely only supports **one usable chromatic role**, expressed as three tints of it — treating primary/secondary/accent as independently assignable hues would break the concept.

### primary (#8B7E6A)
- When to use: the single CTA per section (`.fl-btn-primary`) and any "this is the active thing" marker (`.fl-badge-primary`)
- Surface area: small — text-weight or a 1px border, never a fill larger than a button
- Don't: use primary as a background fill or hero panel color; it exists to be the one warm note against greige, not a surface

### secondary (#6E6255)
- When to use: hover/pressed state for primary only (`.fl-btn-primary:hover`) — it is not an independent second brand color, it's "primary, darker"
- Surface area: interaction-state only, never a resting-state UI element
- Don't: assign secondary to a different UI role than primary "just to add variety" — that reintroduces the multi-hue palette this theme is built to avoid

### accent (#A69783)
- When to use: the lightest step of the same hue, for the `.fl-hue-steps` demonstration and any decorative touch that needs to sit closer to the background than primary does
- Surface area: minimal, ornamental only
- Don't: treat accent as a "pop" color — there is no pop color in this theme by design

## When To Use
- Slow-living, journaling, reading-tracker, or wellness content — the card list (`.fl-card-grid`) is built as a log/diary pattern, not a product grid
- Any B2C or personal-tool context that wants to read as calm and considered rather than energetic — `elevation: "flat"` and zero gradients mean the UI recedes and lets content lead
- Long-session reading or writing UIs where visual noise causes fatigue over time — `density: "spacious"` and `lineHeight: 1.65` are tuned for sustained reading, not scanning

## When NOT To Use
- Marketing/landing pages that need a hero moment — there is no `--gradient-hero`, no glow, no large color fill; a page built to convert in one screen will look inert here
- Dashboards needing fast state-scanning — with only one hue at three tints, status differentiation relies on `success`/`warning`/`error`, not brand color, so a UI with many simultaneous states will feel under-differentiated
- Youth/consumer-playful brands — pairs badly next to `cloud-candy` or similar high-energy themes in the same project; the flat/hairline system reads as a different product register entirely

## How To Use — Full Potential
- The `.fl-card-grid` log pattern (border-top container, each `.fl-card` a baseline-aligned row with a right-aligned `.fl-card-meta`) is the theme's signature move — use it for any list of dated/timed entries rather than falling back to a boxed card grid, which would fight the flat elevation policy
- `.fl-restraint-tile` in the last section is literally the theme explaining itself — if adapting this theme to a real product, keep that kind of explicit "here's what we chose not to do" framing out of production UI, but use its four callouts (one hue, flat elevation, no gradients, faint texture) as your checklist when extending the system
- If you only do one thing: hold the line on zero gradients and zero glow. The instant a `linear-gradient` appears on a button or hero, the theme stops being Fog Linen and becomes generic beige-minimal

## Apply-Mode Notes
- Skip harmonize steps for glow/glass/gradient entirely (this theme has none of the three, by design — not an oversight to "fix" during apply)
- Step 4a's ">60% primary → introduce a counterpoint" doesn't apply in the usual sense: this theme has no counterpoint hue to introduce. If a target page needs more than one visual weight, reach for `textMuted` and `border` (i.e., value/contrast) rather than a second hue
- When re-theming a page that previously had a bold multi-hue theme, expect to remove `box-shadow` on cards almost entirely, not just recolor it — `elevation: "flat"` is a structural change, not just a token swap
