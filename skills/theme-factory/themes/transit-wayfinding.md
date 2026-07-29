# transit-wayfinding

A metro system's own signage language borrowed for the screen — flat, rule-bound, and legible from across a platform.

## Core Concept
Built on the Vignelli premise that a system earns trust by being boringly consistent: one grotesque-adjacent display face (Jost) for every label, a faint cobalt-tinted survey grid under an off-white ground (`background.patternType: grid`), and zero shadows beyond the barest card separation (`shadows.elevation: subtle`, `colored`/`inset` both `none`). Route identity is carried by a small circular `.tw-dot` chip beside each title — deliberately not an asymmetric colored side-border, which would read as a generic "accent card" rather than an actual line marker. The `flat` aesthetic and `systemic`/`confident` personality come from restraint: no gradients, no glow, one 4px rule under the header and nothing else competing for weight.

## Color Role Guidance

### primary (`#1E4FD6`)
- When to use: the default/first line — `.tw-btn-primary`, the `On Time` badge, Line 4's dot. Cobalt is dark enough to always pair with white text (`--color-text-on-primary`).
- Surface area: primary actions and the single most-referenced route; should feel like "the line you'd take by default."
- Don't: don't use primary as a background wash behind large text blocks — reserve it for buttons, dots, and badge fills.

### secondary (`#FF6A13`)
- When to use: the second line and its actions — `.tw-btn-secondary`, the `Boarding` badge, Line 9's dot. Note this button uses dark text (`var(--color-text)`), not white — safety orange at this brightness fails contrast with white but passes cleanly with near-black.
- Surface area: comparable weight to primary but never in the same button row competing for the same action.
- Don't: don't copy the `--color-text-on-primary` token onto a secondary-filled element without checking contrast first — that pairing is exactly the mistake this theme's construction avoids.

### accent (`#E0122B`)
- When to use: the third line, and doubles as the semantic error/alert color (`colors.error` is the same hex) — Line 2's dot, the `Suspended` badge, service disruption text. This overlap is intentional: in real transit systems, red already means "alert," so reusing it for both the line color and the error state is authentic, not a shortcut.
- Surface area: sparing — one line marker, one alert badge type. If a project needs red for a fourth unrelated purpose, that's a sign this theme's 3-line palette has run out of room.
- Don't: don't introduce a fourth accent hue for a fourth line; the theme's chip system was built and tested against exactly three route colors.

## When To Use
- Status/ops dashboards, changelog or incident pages, and any docs site that wants calm systemic clarity over a "friendly SaaS" look.
- Content with genuine multi-line/multi-category structure where a small colored dot per category is more honest than a fourth chromatic role.
- Projects that want a flat, shadow-light alternative to the library's glass and neon themes.

## When NOT To Use
- Warm/approachable consumer branding — the grotesque display face, 4px black-adjacent header rule, and total absence of glow read as institutional, not friendly.
- Content needing more than three genuinely distinct categorical colors — the palette and its dot-chip system are scoped to three lines by design.
- Dark-mode-only products — this theme has no dark variant; its off-white ground and near-black rules are load-bearing to the signage read.

## How To Use — Full Potential
- Lead with `.tw-header`'s 4px `border-bottom: solid var(--color-text)` plus the `.tw-line-row` of dot-chips — that pairing is what makes a page read as a transit system rather than a generic flat-design site.
- Use `.tw-dot` + `.tw-card-head` on any list of categorized items, not just literal transit lines — the pattern generalizes to any "which bucket does this belong to" UI.
- Keep badges as tinted-background/colored-text pills (`.tw-badge-*`), never solid-fill-with-white-text — the tint approach is what keeps `secondary`'s orange legible without a separate override.
- If only one thing: add a `.tw-dot` colored chip beside a heading and set the section's border-bottom to a bold `var(--color-text)` rule — that's the fastest way to make a block unmistakably read as transit-wayfinding.

## Apply-Mode Notes
- Step 4a's generic primary-distribution rule mostly holds, but treat `secondary` as needing its own contrast check rather than inheriting `--color-text-on-primary` — this is the one theme in the catalog where the two filled-button variants use different text colors on purpose.
- Step 4j (gradients/glow): every gradient and glow slot is `none` by design — do not add a hero gradient or button glow during harmonize, even a subtle one; flatness is the entire point.
- Step 4c (radius): buttons and badges are full-pill (`100px`) while cards and inputs stay near-square (`2px`) — don't average these into a single mid-radius value across all components.
