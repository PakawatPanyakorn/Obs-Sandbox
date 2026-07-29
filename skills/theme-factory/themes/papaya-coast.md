# papaya-coast

Late-afternoon light on a rental dock — bright, warm, and lit by the sun, not by a screen.

## Core Concept

Papaya Coast's whole bet is "bright without going neon." The page background is a two-layer atmosphere — a vertical sky-to-sand `linear-gradient` with two soft white cloud blobs floating near the top — rather than a saturated mesh or a dark canvas with glowing accents, which is how most "bright/colorful" themes in this library (`acid-garden`, `ultraviolet-rave`, `synthwave-84`) get their energy. `effects.luminescence` is `"none"` and every glow token is `"none"` on purpose: warmth here comes from color temperature and a single warm-tinted shadow (`--shadow-colored`, orange at 30% opacity), not light emission. `aesthetic: "editorial"` rather than "playful" is also deliberate — the type hierarchy (Lilita One display, Barlow body) and flat, ungradiented cards are closer to a travel-poster layout than a kids'-app one, even though the palette is playful.

## Color Role Guidance

### primary (#FF8A4C)
- When to use: the one booking/reserve CTA per view (`.pc-btn-primary`) and the "Out Now" status badge — primary means "this thing is actively happening," not just "brand color"
- Surface area: buttons and the gradient hero band (`--gradient-hero` reuses the same sky-to-sand family, so primary orange itself stays confined to foreground elements)
- Don't: use primary as a large background fill — the whole page-level warmth already comes from the gradient; a primary-colored panel on top of it would compete instead of layering

### secondary (#2FBFB0)
- When to use: the second-tier action (`.pc-btn-secondary`, "Check Tide Times") and "Reserved" status — turquoise reads as water/availability information, distinct from orange's "action happening now" role
- Surface area: one button, badge fills at ~18% opacity
- Don't: pair secondary as a card background; like primary, it's a foreground/accent role only in this theme

### accent (#FF5C8A)
- When to use: sparingly — "Closing Soon" urgency badge and the accent gradient bar (`--gradient-accent`, turquoise→hibiscus) as a decorative divider only
- Surface area: smallest of the three chromatic roles — a badge and a thin bar, never a button
- Don't: use accent for a primary or secondary action; in this palette it signals urgency/highlight, not a normal interactive state

## When To Use
- Travel, resort, rental, or outdoor-recreation content — the `.pc-card-grid` pattern (tag + icon + concrete named item + status) is built for "what's available right now" listings: rentals, tours, ferry schedules, court/room bookings
- Light-mode consumer products wanting warmth and brightness that still reads as daytime/editorial rather than app-store-playful — the Lilita One + Barlow pairing carries more poster-editorial weight than a typical rounded-sans "fun app" theme
- Content with a real time/tide/schedule dimension — `warning`/`error` badges (`Closing Soon`, `Sold Out`) assume genuinely time-sensitive states exist

## When NOT To Use
- Dark-mode contexts — the entire effect is a daylight sky-to-sand gradient; there is no dark variant and inverting it would destroy the concept rather than adapt it
- B2B/financial/technical content — the poster display type and photographic imagery expectation (`imageStyle: "photographic"`) fight data-dense or trust-driven interfaces
- Alongside `cloud-candy` in the same project — both are bright/warm light themes with rounded pill buttons; stacked together they blur into one undifferentiated "colorful app" register instead of two distinct products

## How To Use — Full Potential
- The body-level three-layer background (`radial-gradient` clouds over the `linear-gradient` sky-to-sand) is the single most identifying visual — it must render at the page level, not be cropped into a hero box; a version with only a solid sky-blue background loses the "5pm boardwalk" read entirely
- `.pc-card` deliberately has no gradient and only a hairline border (`--color-border`) plus a very light shadow — resist adding a gradient card background "to match the hero," the flat cards are what keep the theme editorial instead of decorative
- If you only do one thing: use the `--shadow-colored` warm orange shadow on the single primary CTA per screen — it's the one place the theme allows a colored glow-adjacent effect, and it's what makes the button read as "sun-warmed" rather than just orange

## Apply-Mode Notes
- Skip glow/glass harmonize steps entirely — both are `none` by design; the theme's only "effect" is the warm-tinted `--shadow-colored`, which should not be treated as a glow token during harmonize
- Step 4a's primary-fill-percentage rule applies loosely here: primary is confined to buttons/badges by design, so if harmonize finds primary exceeding ~10-15% of a page's surface area, that's a real signal something has been filled solid that should instead show the sky-to-sand background through
- The page-level gradient background is structural, not decorative — when re-theming a page that previously had a solid or dark background, this is one of the few themes in the library where adding a body-level gradient (rather than keeping color changes confined to components) is correct and expected
