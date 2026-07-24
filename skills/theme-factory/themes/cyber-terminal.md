# cyber-terminal

The archetypal green-on-black hacker terminal — CRT phosphor scanlines, monospace-only typography, and a palette so monochrome that `success` and `primary` are literally the same green.

## Core Concept
Near-absolute black canvas (`#000900`) with 4px horizontal scanline repeat (`patternType: lines-h`, opacity `0.025`) simulating a CRT phosphor display. Every font role — body, mono, *and* display — is the same monospace stack (JetBrains Mono/Cascadia Code); there is no separate display typeface, which is itself the point: a terminal has one typeface. `gradients.*` are entirely `none` except `text` (which is just a solid hex, not a gradient) — this theme is the most literal "no decoration" implementation in the catalog after `obsidian-mono`, but green instead of silver, and warmer/more alive due to consistent glow.

## Color Role Guidance

### primary (`#00FF41` phosphor green) — also `success`
- When to use: everything "on" — primary buttons, active state, and every success/confirmation signal. Primary and success share the exact same hex; there is no distinction between "the brand color" and "things going right" in this theme.
- Surface area: text color throughout is a slightly dimmer green (`text: #00CC33`) with primary reserved for emphasis, borders, and glow-bearing elements — don't use primary and body text interchangeably even though they're both green.
- Don't: don't introduce a separate "success" treatment distinct from primary — collapsing them is intentional; the terminal has one "everything is fine" signal color.

### secondary (`#00CCFF` cyan)
- When to use: a distinct data/link color against the green field — the only non-green, non-warning/error hue in the palette, useful for hyperlinks, secondary commands, or a "different data stream" signal.
- Surface area: sparing — this is the one place the monochrome-green premise is deliberately broken, so keep it rare enough to still register as a deviation.
- Don't: don't let cyan appear as often as green — it should read as "a different kind of information," not a co-equal palette member.

### accent (`#CCDD00` acid yellow-green) — also `warning`
- When to use: caution/attention states — accent and warning share the same hex, same pattern as primary/success. Use for alerts, flagged output, "pay attention here" moments.
- Surface area: small, sparing — like secondary, it's a deliberate one-note deviation from pure green.
- Don't: don't use accent for routine emphasis that primary/glow could handle — it should specifically mean "warning," not "slightly different green."

## When To Use
- Developer tools, terminal emulators, hacker/security-themed products, changelog/log-viewer UIs (the preset's own `sourceFile: docs/changelog.html` confirms this lineage).
- CLI-adjacent web products wanting authentic phosphor-terminal nostalgia rather than a generic "dark mode with green" gesture.
- Content that's genuinely monospace-appropriate — code, logs, command output — where a single fixed-width typeface throughout isn't a limitation.

## When NOT To Use
- Any content with real prose/reading needs — an entire page in monospace at `bodyWeight: 400` is a deliberate authenticity choice for terminal content, but actively hurts readability for long-form writing.
- Products needing a broad categorical color palette — success and primary being identical, and warning/accent being identical, leaves only 4 truly distinct hues (green, cyan, yellow-green, red) for the whole UI.
- Warm, human, or approachable branding — the entire aesthetic is deliberately cold, technical, and impersonal.

## How To Use — Full Potential
- Keep the scanline pattern visible at low opacity across the full page, not just a hero section — it's a body-level background (`background.type: pattern` applied globally), and the "CRT" read depends on it being everywhere, not localized.
- Use `--shadow-colored`'s combination of glow + 1px solid border (`0 0 24px rgba(0,255,65,0.5), 0 0 0 1px #00FF41`) for the single most active/focused element per view — it reads as "this is the terminal's current focus," similar to a cursor or active prompt.
- Apply `textShadow: 0 0 8px rgba(0,255,65,0.5)` to headings consistently — the soft glow is what separates "green terminal theme" from "theme with green text," and should appear on every heading, not just the hero.
- If only one thing: apply the phosphor glow text-shadow to monospace text on black — the single fastest, cheapest signal of cyber-terminal.

## Apply-Mode Notes
- Step 4b (font mapping): map ALL font roles (body, display, mono) to the same monospace stack — this theme has no separate display face, and introducing one during harmonize breaks the "one typeface" terminal premise.
- Step 4a: primary=success and accent=warning are intentional collapses — don't invent distinct success/warning colors during harmonize; reuse primary/accent exactly as the theme does.
- Step 4j: the scanline pattern is structural, not decorative — it should survive harmonize as a global body-level background, not get dropped or confined to one section.
