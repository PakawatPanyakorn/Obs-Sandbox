# z-pattern-landing

**Archetype:** z-pattern-landing · **Family:** grid-discipline

## Core Concept
A directed eye-path, not a content hierarchy — logo to nav CTA to a diagonal sweep of supporting content to a single bottom-right closing CTA, built to convert attention into one click, not to be read start-to-finish. Every element besides the closing CTA is deliberately quieter than it: the nav CTA is outline-only and small, the lead's supporting visual gets flat surface treatment. This archetype measures success by clicks on one button, not by how thoroughly the page gets read.

## When To Use
- SaaS waitlist pages, single-offer landing pages, beta-signup pages — anything pitching one product in prose before asking for the click.
- Metrics-led landing pages: "we cut load time 80%" pitches, funding/traction one-pagers, investor-facing product pages built around a single number.
- Feature-comparison or "why choose us" landing pages, pricing-adjacent one-pagers with a handful of concrete benefits building the case toward one CTA.

## When NOT To Use
- Print, presentation, or markdown targets — none of these translate meaningfully (see Medium Notes); don't force the Z eye-path metaphor onto a medium with no scroll-driven viewport.
- Content wanting the closing CTA to turn into a stat tile ("bigger number = more conversions") — that's the dashboard-trope anti-pattern; the CTA stays a verb-led button, the number stays in the captioned exhibit.
- A benefit list that wants to grow into a uniform icon-card 3-up grid — that competes with the CTA for attention; keep it a plain rule-separated list so the closing CTA remains the only button-styled element on the page.

## Region / Component Guidance
- **masthead** (`1 / 13`): logo left + lightweight nav CTA right — the Z-path's top bar. The nav CTA here is deliberately the QUIET call-to-action (outline style, no hero treatment); full visual weight is reserved for the closing CTA.
- **lead** (`1 / 13`, internally split 1-7 copy / 8-12 visual): the diagonal sweep zone — supporting headline/copy plus one supporting visual, staggered (visual offset downward via margin) so the eye physically traces the diagonal instead of just asserting it in prose. Carries the page's one social-proof testimonial pull quote.
- **body** (`7 / 13`): the closing call-to-action, bottom-right — the destination the whole page has been steering toward. This region, not the lead's visual, carries the archetype's hero shadow/gradient treatment; the CTA button is the single most visually weighted element on the page.

## Content-Type Notes
- **textHeavy**: lead drops its visual slot entirely — the diagonal is carried by copy alone, ending in a short proof line nudged toward the bottom-right. Don't invent a product screenshot just to fill the visual slot.
- **chartHeavy**: lead's visual becomes a single captioned proof exhibit (growth curve, before/after, traction chart) standing in for the product shot — still only one exhibit, this archetype has no well to hold a second.
- **cardOrListHeavy**: lead's copy column gains a short 3-item benefit list (hairline-rule separated) to build the case — still one diagonal sweep, the list is a supporting device inside the lead, not a second competing block of cards.

## Medium Notes
- Presentation: does not translate meaningfully — a slide deck has no scroll-driven Z eye-path; forcing this into a slide master just produces a hero slide followed by a CTA slide, a different pattern wearing this one's name. Use a picture-and-message or divider-slide pattern instead.
- Print: does not translate meaningfully — print has no single click to convert on, and the diagonal eye-path only exists inside a viewport with known edges. Use `single-column-editorial` or `asymmetric-split` for anything meant to be printed.
- Markdown: does not translate meaningfully — markdown has no positional eye-path, only linear flow. Don't force the metaphor; write it as prose with one clear call-to-action link instead.

## Pairing Notes
- `solarpunk-utopia` — an optimistic, CTA-driven landing-page register with its own pill-button, gradient-CTA convention, a direct fit for a single-action conversion page.
- `eigenvalue` — its own asymmetric hero panel and live signal readouts already read as a confident single-CTA fintech/quant-product landing page, a register distinct from solarpunk-utopia's soft optimism despite sharing this archetype.
