# cloud-candy

A prize wall you want to touch — glossy pink, hard-pop shadows instead of glow, and a lilac room that never goes fully quiet.

## Core Concept

Cloud Candy commits to one idea: soft edges, hard consequences. Every corner is `--radius-button: 999px` or a fat 24px card radius, and the primary button doesn't glow like most "playful" dark-mode themes — it pops off the page with a flat 8px offset shadow (`--shadow-colored`) that compresses to 4px on press, like a real sticker peeling and reseating. That's the `personality: ["soft", "colorful", "warm"]` tags made literal: `soft` isn't a mood word here, it's a shadow value — the sticker-peel offset is where it lives. The three-blob radial-gradient mesh behind everything (pink top-left, mint top-right, butterscotch bottom-center) keeps the lilac canvas from reading as flat digital pastel — it's meant to feel like light through a candy-shop window, not a Figma fill.

## Color Role Guidance

### primary (#E85A96)
- When to use: the one claim/CTA action per view (`.cc-btn-primary`) and card accent tags (`.cc-card-tag`)
- Surface area: buttons and small tag labels only — never a large fill. The button gradient (`--gradient-button`) is the biggest primary-colored surface in the whole preview
- Don't: use primary as a card or section background — it's built to sit on the pale lilac ground, not replace it

### secondary (#2FAE96)
- When to use: the second-tier action (`.cc-btn-secondary`, "Spin the Wheel") and its own offset shadow tone (`#1E7E6C`) — secondary gets the same hard-pop treatment as primary, not a flatter one
- Surface area: one secondary button per action row, plus badge fills at 16% opacity (`.cc-badge-secondary`)
- Don't: pair secondary and primary directly adjacent at full saturation in the same card — let lilac/mint background separate them

### accent (#E8A93C)
- When to use: "new drop" signaling (`.cc-badge-accent`) and the accent gradient bar (`--gradient-accent`, butterscotch→pink) as a decorative divider
- Surface area: small — a badge, a thin gradient bar, never a button fill of its own
- Don't: use accent for a primary CTA; it reads as a status/highlight color, not an action color, in this palette

## When To Use
- Kids'/family products, rewards or loyalty programs, arcade or prize-redemption flows — anything with a literal "collect and claim" loop, which this theme's card grid and badge set are built around
- Light-mode consumer apps that want warmth without going saccharine-generic — the hard-pop shadow and flat (non-glowing) surfaces keep it from reading as a template pastel gradient hero
- Illustrative/emoji-forward content — `imageStyle: "illustrative"` is a real constraint here, not a placeholder value

## When NOT To Use
- B2B, financial, or trust-driven content — the pill buttons and offset "sticker" shadows actively undercut credibility signals
- Dense data or dashboard UIs — `hierarchyClarity: "medium"` and `density: "spacious"` mean this theme spends space generously; it will fight a compact table or multi-column report
- Dark-mode contexts — there is no dark variant by design; the whole effect depends on a pale lilac ground catching colored light

## How To Use — Full Potential
- The `.cc-btn-primary` hard-pop shadow (`0 8px 0 #C43F76` collapsing to `0 4px 0` on `:hover`) is the single most identifying detail — get that right before anything else, since a soft blurred shadow there would make it look like a generic rounded-button theme instead of Cloud Candy specifically
- `.cc-card:hover` adds a slight `rotate(-1deg)` alongside the lift — lean into small asymmetric rotation on interactive elements elsewhere (a badge, a sticker icon) rather than perfectly straight grids, it reinforces the "physical sticker" read
- If you only do one thing: apply the three-blob radial-gradient body background (`--gradient-hero` is for the header only; the page-level mesh is the separate `background-image` stack in `body`) — a flat solid lilac page immediately reads as "generic pastel," the mesh is what sells the room

## Apply-Mode Notes
- `--gradient-text` is intentionally `none` — this theme never puts a gradient fill on headline text (anti-pattern gate). Do not add one during harmonize step 4j; leave headline text solid `--color-text`
- Skip glow-related harmonize steps entirely (4h or equivalent) — `glowSm/Md/Lg` are all `"none"` by design; the "pop" is a hard offset shadow, not a blur, and adding blur/glow to primary elements will fight the sticker concept
- This theme only has 2 fully independent chromatic roles for large surfaces (primary pink, secondary teal-mint) — accent butterscotch is deliberately minor/decorative, so step 4a's ">60% primary → introduce a counterpoint" should route the counterpoint to secondary, not invent a third major fill from accent
