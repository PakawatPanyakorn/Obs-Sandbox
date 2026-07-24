# obsidian-mono

Dark colorless minimalism where restraint itself is the design move — every element earns its space because nothing else is competing for attention.

## Core Concept
A near-absolute-black canvas (`#131313`, deliberately not `#000000`) with a single silver accent and zero chromatic interference — `gradients` and `effects.luminescence` are all `"none"` by design, not by omission. The theme's entire personality lives in typographic contrast instead: a light-weight display serif (Cormorant, 300wt, `.tf-header h1`) set against a mono label system (JetBrains Mono, `.tf-kicker`/`.tf-section-title`), not in color or effect. "Silence is not emptiness" — the theme's own copy states the thesis directly.

## Color Role Guidance

### primary (`#ADADAD`)
- When to use: the one interactive action per view — primary button fill (`.tf-btn-primary`), the active/emphasized figure, a single accent underline. In this theme primary reads as "the thing that's alive" against an otherwise inert palette.
- Surface area: small and precise — button fills, `.t-mono`/`.t-h2` accent text, one icon or border on the emphasized element. Never a section background or fill.
- Don't: never tint a whole panel or hero with primary — it collapses the "silence" premise the theme is built on. Don't use it for two unrelated meanings in the same viewport; it reads as one signal, not a color family.

### secondary (`#757575`)
- When to use: outline/subordinate buttons (`.tf-btn-secondary`, e.g. "Inspect" vs. "Execute"), anything that should read as present but not the point.
- Surface area: text and border color only, never a fill.
- Don't: don't let secondary and `textMuted` (`#606060`) collide in the same component — they sit only 9% apart in lightness, so pick one role per element rather than mixing them as if they were distinct hues.

### accent (`#D8D8D8`)
- When to use: hover/active escalation of primary only (`.tf-btn-primary:hover`) — accent is primary's brighter register, not a third independent color.
- Surface area: hover states, the single brightest text moment on a page.
- Don't: don't introduce accent as a standalone badge/tag color — badges here (`.tf-badge-*`) differentiate by border hue (primary/success/warning/error), and accent isn't one of them; treat it purely as primary's escalation.

This theme effectively supports **2 usable chromatic roles** in practice (primary/accent are the same hue at different lightness; secondary/textMuted sit close together) — don't force an artificial 3-way primary/secondary/accent split onto content that doesn't need it.

## When To Use
- Developer tools, CLI/API dashboards, "serious infrastructure" product surfaces — the mono-label + status-badge vocabulary (`.tf-badge-success/warning/error`) reads natively as system status.
- Portfolio or case-study pages where the work itself, not the chrome, should be the loudest thing on the page.
- Data-dense technical writing or terminal-adjacent UIs where color would read as noise rather than signal.

## When NOT To Use
- Marketing/landing pages needing a persuasive CTA color story — the theme structurally resists a "pop" color; there is no warm accent to reach for.
- Content with a genuine 4+-value status/category taxonomy — badges differentiate by border color alone (`.tf-badge-*` fill stays transparent/primaryLight), which caps out fast beyond the built-in success/warning/error/neutral set.
- Anything meant to feel warm, human, or approachable — the theme's entire point is austere precision; forcing warmth onto it (e.g. adding a gradient hero) is a violation of the preset, not a variation of it.

## How To Use — Full Potential
- Lead with the `.tf-header` treatment: a huge light-weight display serif headline (`.tf-header h1`, `font-weight: 300`) over a tiny tracked-out mono kicker line (`.tf-kicker`) — this scale/weight contrast is the theme's single best trick and should appear at least once per page, not just in the hero.
- Use `.tf-cards`' flush, `border-right`-divided layout instead of gapped/shadowed cards — the rule-divided card row (no gap, 1px border between cards) is what keeps the "silence" premise intact; a shadowed card grid here reads as generic and fights the theme.
- Let `.tf-badge-*` differentiate by border color with transparent fill — resist the urge to "make them pop" with background fills; the restraint is the point.
- If only one thing: use the mono-kicker + serif-headline pairing (`.tf-kicker` + `.tf-header h1`) somewhere prominent — it's the fastest way to make a page read as obsidian-mono at a glance.

## Apply-Mode Notes
- Harmonize steps 4d (colored sections) and 4j (gradients/glow/effects) in `modules/apply-mode-token-harmonize.md` should be **skipped, not adapted**, for this theme — `gradients.*` and `effects.luminescence` are `"none"` across the board by design; injecting a hero gradient or glow during apply is a violation of the preset, not a harmonization.
- Step 4a's generic ">60% primary usage → introduce a counterpoint" rule doesn't apply cleanly here — with only 2 real chromatic roles (see Color Role Guidance above), 2-role usage (primary for action, secondary for everything subordinate) is correct even at high primary-usage percentages.
