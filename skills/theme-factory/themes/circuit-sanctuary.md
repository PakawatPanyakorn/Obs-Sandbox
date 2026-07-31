# circuit-sanctuary

A PCB fiberglass board rendered as a UI, not a cyberpunk neon dashboard — the difference is restraint.

## Core Concept
Circuit Sanctuary takes the literal geometry of a printed circuit board — a fiberglass substrate, copper traces, solder-pad vias — and makes it the actual page structure rather than a decorative skin. The body-level background (`background.patternType: grid`) is two `linear-gradient` line layers forming a real trace grid, with a third `radial-gradient` layer dropping a via-dot at every intersection, offset by half the grid pitch (`background-position: 0 0, 0 0, 12px 12px`). `design.personality: industrial, analytical, glowing` is the key distinction from a neon-cyberpunk treatment: `effects.luminescence` is only `subtle`, not `medium`/`strong` — this is quiet hardware reverence, closer to a well-lit workbench than a synthwave dashboard. The all-monospace pairing (`Fira Code` display, `IBM Plex Mono` body) reflects how PCB silkscreen text actually looks — technical labeling, not a friendly UI voice.

## Color Role Guidance
### primary (`#39D97A` trace green) — also `success`
- When to use: anything "live" or "connected" — primary buttons, active nets, and every continuity/OK signal. Primary and success share the exact hex, mirroring a real multimeter continuity test where "the trace is green" and "the circuit is fine" are the same fact.
- Surface area: moderate — body text uses a dimmer tint (`text: #D7F2DF`) while primary itself is reserved for buttons, active states, and the background grid lines.
- Don't: don't invent a separate success color during harmonize — the collapse is the point, matching `cyber-terminal`'s primary/success pattern but grounded in a literal continuity-test metaphor instead of "the terminal says OK."

### secondary (`#C98A4B` copper)
- When to use: the material color — anything meant to read as physical metal rather than active signal: labels, secondary buttons, borders that need warmth against the cool green field.
- Surface area: moderate, mostly on buttons and the "Order Board" / component-reference actions in the preset HTML.
- Don't: don't use copper for anything that needs to look "electrically active" — that's primary's job; copper is inert material, not signal.

### accent (`#FFE15C` solder-gold)
- When to use: the smallest, most precise mark — literally the via-dot in the background pattern and the `.board-card::after` corner dot marking a through-hole test point.
- Surface area: minimal by design — a single small dot per card, never a fill or a large surface. Solder pads on a real board are small and precise; the accent should stay that way.
- Don't: don't scale accent up into a button or banner color — its entire visual logic depends on being a small precise mark, not a bold color.

## When To Use
- Hardware/maker/IoT product sites, electronics documentation, robotics portfolios — anywhere the content is genuinely about physical circuits.
- Developer tools for embedded/firmware work wanting a technical register distinct from the generic "dark mode IDE" look.
- Content that can use the `.board-card` / continuity-badge (`tf-badge-success` "Continuity OK", `tf-badge-error` "Short Detected") vocabulary literally, not as a metaphor stretch.

## When NOT To Use
- Consumer-friendly or warm branding — the palette and monospace-everywhere typography are deliberately unglamorous and technical.
- Content wanting a loud neon-cyberpunk register — `effects.luminescence: subtle` and the complete absence of any gradient (`gradients.*` all `none`) mean this theme underperforms next to `synthwave-84` or `cosmica` if what's wanted is maximalist glow.
- Dense long-form prose — monospace body text at `lineHeight: 1.65` is tuned for short technical labels and card copy, not paragraphs of narrative writing.

## How To Use — Full Potential
- Keep the trace-grid + via-dot background global on `body`, not confined to a hero — like `cyber-terminal`'s scanlines, the "this is a real board" read depends on the pattern being everywhere, not a decorative header banner.
- Use `.board-card::after` (the small accent-gold dot, top-right of every card) consistently — it's the cheapest, most legible "this card is a board section" signal, and should appear on every card, not just some.
- Reserve `--shadow-colored` (green glow + 1px solid border) for exactly one "currently active" element per view, the same restrained-emphasis pattern `cyber-terminal` uses — see the "Power Rail" tile in the Effects section of the preset HTML.
- If only one thing: render the trace-grid+via-dot background at body level and use trace-green only for things that are actually "on" or "connected." That distinction — quiet copper-and-fiberglass field, green means live — is the whole theme.

## Apply-Mode Notes
- Step 4a (primary/secondary/accent distribution): primary=success is intentional (continuity metaphor) — don't invent a separate success color. Accent should stay confined to small precise marks (via-dots), not scaled into a fill; if the target page needs a bold third color, look to secondary (copper) first.
- Step 4j (background/texture): the trace-grid+via-dot pattern is structural, not decorative — preserve it as a global body-level background rather than confining it to one section.
- Step 4h (glow/luminescence): keep glow at `subtle` — this theme is adjacent to neon-cyberpunk territory (`synthwave-84`, `cosmica`, `ultraviolet-rave`) but deliberately underplays it; resist the temptation to intensify glow during harmonize just because the palette has a bright green in it.
