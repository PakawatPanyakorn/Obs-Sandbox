# nordic-noir

A cold Scandinavian case-file register — the theme reads like a detective's desk at 2am, not a brand.

## Core Concept
Nordic Noir commits to a single idea: everything is slate-blue-gray and quiet except the one thing that needs your attention, which is alarm-red. The palette is deliberately narrow (`aesthetic: editorial`, `personality: moody, calm, utilitarian`) — no secondary decorative hues, no gradients anywhere (`gradients.*` are all `none`), and the only texture is a body-level CCTV-static grain (`background.patternType: noise`, blended with `background-blend-mode: overlay` rather than a flat opacity layer) plus a soft radial vignette. The typography pairing reinforces the procedural tone: `Barlow Condensed` (display) is a condensed industrial grotesk more at home on a case-file spreadsheet than a magazine masthead, paired with the plain, systematic `IBM Plex Sans` for body copy and `IBM Plex Mono` for case numbers and timestamps.

## Color Role Guidance
### primary (`#4C6B7A` fjord blue-gray)
- When to use: secondary actions, active nav, links — the "this is interactive" signal that isn't urgent.
- Surface area: moderate — it's the second-most-visible color after text, appearing on secondary buttons and interactive chrome, but never as a page-wide fill.
- Don't: don't use primary where accent belongs — primary reads as "normal operation," not "this needs a decision."

### secondary (`#6F7F74` moss gray-green)
- When to use: a quiet third tone for less-important UI — ghost states, muted tags, borders that need to read as slightly warmer than pure gray-blue.
- Surface area: sparse — mostly borders and low-emphasis text, rarely a fill.
- Don't: don't pair secondary directly against primary as a two-color system; both are desaturated enough that they need text/border weight to stay distinguishable, not hue alone.

### accent (`#B3372C` alarm red) — also `error`
- When to use: exactly one job — flagging the thing that broke the case open, or the thing that's wrong. `accent` and `error` share the identical hex; see `.case-card.flagged`'s top-border and `.case-tab.unresolved` in the preset HTML for the two canonical uses.
- Surface area: deliberately rare — the whole theme's tension depends on red being scarce. If more than one element per view uses it, it stops reading as a flag and starts reading as decoration.
- Don't: don't introduce a separate error color during harmonize — accent IS error here, the same collapse pattern `cyber-terminal` uses for primary/success.

## When To Use
- Investigative journalism, true-crime editorial, detective fiction sites — the `.case-card`/`.case-number` pattern in the HTML is literally a case-file card, not a generic content card wearing dark colors.
- Noir-toned game UI or interactive fiction wanting a genuinely cold, procedural register rather than a generic "dark mode."
- Any dashboard or log-viewer content where "one alarm color, otherwise quiet" is the actual information architecture (incident flags, audit trails).

## When NOT To Use
- Warm, human, or approachable branding — every color in the palette is desaturated and cool on purpose; forcing warmth in fights the concept.
- Content needing more than one or two simultaneous "urgent" states — accent/error being one hex means there's no way to distinguish "flagged" from "broken" without adding text.
- Bright/playful/youth-oriented products — the grain and vignette read as surveillance-footage mood, which will feel like a bug, not a feature, outside noir-adjacent content.

## How To Use — Full Potential
- Keep the grain+vignette body background global, not confined to a hero — it's set on `body` via `--bg-image` with two comma-separated layers (turbulence noise + radial vignette) and `background-blend-mode: overlay, normal`; confining it to one section breaks the "this is CCTV footage" premise the same way `cyber-terminal`'s scanlines need to stay page-wide.
- Use `.case-card`'s `border-top` as the flag mechanism (`.flagged` swaps it to accent-red) rather than inventing a new "urgent card" variant — it's the cheapest, most legible way to mark one card as different from its neighbors.
- The `.rec-dot` pulse (small accent-colored dot with a slow opacity animation, `@keyframes rec-pulse`, disabled under `prefers-reduced-motion`) is the single fastest way to signal "this is live/being watched" — use it sparingly, next to a title or status line, never as decoration on multiple elements at once.
- If only one thing: put the grain+vignette background on the page and set exactly one element to accent-red. That contrast — quiet field, one red flag — is the whole theme.

## Apply-Mode Notes
- Step 4a (primary/secondary/accent distribution): this theme only has two truly distinct chromatic roles doing real work — primary (interactive) and accent (alarm), since accent and error are intentionally the same hex. Don't invent a third meaningfully-different hue during harmonize; secondary should stay a quiet desaturated variant, not a competing accent.
- Step 4j (background/texture): the grain+vignette pair is structural (global body background), not decorative — preserve both layers and the `overlay` blend mode; dropping the blend mode turns "CCTV static" into "dirty screen."
- Step 4b (fonts): keep the condensed-display / plain-body split (`Barlow Condensed` / `IBM Plex Sans`) — collapsing to a single typeface would lose the "official report typed up after the fact" register that the condensed face provides in headings.
