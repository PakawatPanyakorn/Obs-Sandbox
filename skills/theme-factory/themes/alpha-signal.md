# alpha-signal

A Bloomberg-terminal trading dashboard rendered in an unexpected register — fresh mint and teal instead of black-and-green, with an elegant italic serif body voice cutting against the industrial condensed-caps data chrome.

## Core Concept
A 24px teal grid (`background.patternType: grid`) on pale mint, topped by a full-bleed dark-teal header bar (`.header-bar`) with a solar-yellow bottom border. The theme's tension is deliberate: Bebas Neue condensed all-caps (`.hero-title`, `.section-title`, `.sig-ticker`) for data/structure elements, paired with Crimson Pro 300-weight italic serif (`.hero-sub`, body copy) for narrative elements — "industrial confrontation meets elegant explanation."

## Color Role Guidance

### primary (`#0A7060` deep teal)
- When to use: authority/trust signals — the header bar background, primary CTA (`.btn-primary`), "BUY" signal accents (`.sig.buy::before`), headline numerals that read as good news.
- Surface area: large structural fields (header, hero gradient) are fine for this theme — teal is meant to feel institutional and load-bearing, not a small accent.
- Don't: don't use teal for a "sell"/negative reading — that role belongs to secondary/error; teal is reserved for authority and buy-side signal.

### secondary (`#FF4E3A` coral)
- When to use: urgency and "sell" signals (`.sig.sell::before`, `.sig-action.sell`) — the theme's stated role is "coral urgency."
- Surface area: badges, sell-signal markers, secondary buttons (`.btn-secondary`) — pointed, not diffuse.
- Don't: don't pair coral with buy-side/positive data — it will read as a false alarm against the theme's own signal-color convention (buy=success green, sell=coral/error).

### accent (`#FFD600` solar yellow)
- When to use: "conviction"/attention markers — the live-status pill (`.status-live`), the header's bottom border stripe, hold-signal markers (`.sig.hold::before`), Calmar-ratio-style secondary metrics.
- Surface area: thin strokes and small high-contrast chips — a full yellow fill anywhere but a badge/pill reads as a warning state, competing with `warning` (`#CC8800`).
- Don't: don't conflate accent with the dedicated `warning` token — they're deliberately close in hue family but distinct roles (accent = conviction/live, warning = caution).

## When To Use
- Financial/trading dashboards, quant strategy reports, backtest logs — the `.strategy-table`, `.stats-strip`, and `.signal-grid` components are purpose-built for exactly this content shape.
- Any data-dense "terminal" product that wants to avoid the black/green Bloomberg cliché without losing the density and authority.
- Content with real buy/sell/hold-style categorical signals that benefit from the success/error/warning-mapped `.sig` border convention.

## When NOT To Use
- Casual consumer content or anything needing warmth — the condensed all-caps Bebas Neue + monospace ticker vocabulary reads as clinical/urgent by design.
- Long-form narrative writing beyond short italic pull copy — `.hero-sub`'s italic serif is meant for a single dek-length sentence, not paragraphs of body text.
- Content without genuine quantitative/tabular data — `.strategy-table` and `.stats-strip` are the theme's centerpiece; without real numbers to fill them, the theme has nothing to anchor its density to.

## How To Use — Full Potential
- Lead with the `.header-bar` + `.stats-strip` combination — full-bleed dark-teal bar with a live-status pill, immediately followed by a 5-column stat strip with colored deltas (`.up`/`.down`). This one-two is the theme's strongest opening and establishes the "live terminal" read instantly.
- Use the `.sig` grid's left-border color convention (`.sig.buy/.sell/.hold::before`) for any categorical signal list, not just trading tickers — it's a reusable, theme-native pattern for status-at-a-glance.
- Keep Bebas Neue confined to numerals, tickers, and short headers; let Crimson Pro italic carry any explanatory sentence — mixing the two the wrong way (long condensed-caps paragraphs, or serif numerals) breaks the theme's core contrast.
- If only one thing: pair a Bebas Neue stat value (`.stat-val`) with a Share Tech Mono label (`.stat-label`) above it — this two-font stat block is the fastest way to make a page read as alpha-signal.

## Apply-Mode Notes
- Step 4b (font mapping) needs care here — this theme uses three distinct font roles (`fontFamily` serif body, `fontFamilyDisplay` condensed sans, `fontFamilyMono` terminal mono), not the usual two; make sure numerals/labels get mono or display, not body serif, or the "terminal" read collapses.
- Step 4a color distribution should follow the buy/sell/hold convention (success=buy, error=sell, warning=hold) rather than a generic primary/secondary split when the target file has any categorical status data — this theme already has an opinionated mapping built in.
