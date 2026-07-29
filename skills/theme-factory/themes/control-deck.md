# control-deck

A cream laminate control panel with burnt-orange switches and a VU meter that actually reads a signal — 1970s hardware, not a screen pretending to be one.

## Core Concept

Control Deck's governing rule is: every affordance is a physical object, never a flat digital control. `.cdk-toggle` is built from a rectangular well (`--shadow-inset`) with a sliding knob (`.cdk-toggle::after`), not a modern rounded switch — that's the difference between **analog/tactile** and the glowing-neon **retro-futurism** of `neon-foundry` or `synthwave-84`. There's no glow, no glass, no gradient background anywhere in this theme (`effects.glowBlur: 0`, `gradients.hero: none`) — the only atmosphere comes from a barely-there wood-grain stripe (`repeating-linear-gradient` at 95deg, 7px pitch) and hard mechanical bevels. Teko's ultra-condensed uppercase numerals were chosen specifically because they read as scoreboard/gauge digits, reinforcing that this is instrumentation, not branding.

## Color Role Guidance

### primary (#C1552C)
- When to use: the "Engage" action, active-state toggles, primary status badge
- Surface area: 10-15% — one hero button and a handful of active-state accents, never a large panel fill
- Don't: use primary for the VU meter's "everything is fine" segments — that's `accent` (green)'s job; mixing the two roles blurs "this is the main action color" with "this is a status reading"

### secondary (#5B4636)
- When to use: the dark wood/metal panel-brown surfaces — secondary button, the toggle's track color
- Surface area: moderate — it's the "chassis" color, so it can appear wherever a switch or knob needs a housing
- Don't: use secondary as body text color — at this darkness it's meant for small hardware elements, not paragraph-scale content (contrast is fine but the visual role reads as "component," not "text")

### accent (#7A9B57)
- When to use: VU-meter segments (`.cdk-vu span`) and "nominal" signal readings specifically
- Surface area: small, functional — it should always mean "reading is fine," never used decoratively
- Don't: reuse accent green for a generic "success" badge if `success` (#4F8B3B) is also present in the same view — the two greens are close enough that using both roles side by side reads as a mistake, not two distinct signals

## When To Use
- Analog instrumentation, flight-sim/space-console, or any dashboard content with genuine sensor-style readings (fuel, signal strength, gauge values) — the panel cards are built around real numeric readouts, not decorative stats
- Retro hardware or synth/audio-equipment product content wanting a warm 1970s console feel distinct from `prussian-blueprint`'s cold CAD linework or `neon-foundry`'s dark neon industrial register
- Compact, information-dense layouts — `density: compact` and the condensed Teko display are built to hold a lot of small readouts without feeling sparse

## When NOT To Use
- Any content wanting glow, gradient, or glass depth — this theme has zero soft effects by design; retrofitting glow onto it collapses the "real hardware" premise
- Consumer/friendly-brand contexts — the uppercase condensed type and functional-only color system read as instrument panel, not approachable product
- Dark-mode-only products — this is a fixed daylight cockpit-cabin palette with no dark variant; it doesn't invert cleanly because the "cream laminate" identity depends on a light base

## How To Use — Full Potential
- Lead with `.cdk-toggle` and `.cdk-vu` together in a status card — that combination (physical switch + live meter) is what makes a page unmistakably Control Deck rather than generic "brown industrial theme"
- Keep all headings uppercase via the global `h1, h2, h3, h4` rule — Teko's condensed caps are doing real identity work here; lowercase headings would make it read as a generic technical sans instead
- If you only do one thing: build one `.cdk-toggle` with the inset-well + sliding-knob construction exactly as specced — it's the single most recognizable "hardware, not software" signal in the whole theme

## Apply-Mode Notes
- Step 4j (glow/gradient check) can be skipped entirely — this theme has no gradients beyond the single button gloss and no glow/glass effects by design; don't add any when harmonizing.
- Step 4a's primary-dominance rule needs a functional-color caveat: `accent` (VU green) must stay reserved for signal readings and never get pulled in as a general decorative color, even if primary usage is otherwise low — its meaning is semantic, not just chromatic balance.
- This theme has no dark-mode token set — if the target file has a light/dark toggle, leave existing dark tokens alone rather than inventing a "night console" variant; the wood-grain/cream identity is a fixed daylight-cabin choice.
