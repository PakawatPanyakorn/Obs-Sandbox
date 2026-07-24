# meridian-capital

Luxury investment bank meets editorial magazine — a cobalt/old-gold/rose-coral tricolor system on warm champagne, built for portfolio showcases and metric-dense financial storytelling rather than generic corporate blue.

## Core Concept
Warm champagne canvas (`#F4EDD8`) under a 3-layer radial gradient mesh (cobalt 12%, old gold 15%, rose-coral 9%), Cormorant Garamond's tall elegant 700-weight serif against Libre Franklin's light 300-weight sans. The theme's centerpiece is a genuine tricolor system: `--gradient-text` runs cobalt→purple→gold (3 stops), `gradientBorder` runs cobalt→gold→rose (all three roles together) — this is one of the few themes where all three chromatic roles are meant to appear combined in a single gradient, not just individually.

## Color Role Guidance

### primary (`#1A4BCC` cobalt blue)
- When to use: the "capital/institutional" anchor — primary buttons (`--gradient-button`, cobalt-only), the first stop in every multi-color gradient, structural trust signal.
- Surface area: generous — cobalt leads the visual hierarchy, appropriate for large structural elements as well as buttons.
- Don't: don't let cobalt appear without at least occasional pairing with gold — the theme's "investment bank meets editorial" identity depends on the cobalt/gold combination, not cobalt alone (which would read as generic corporate blue).

### secondary (`#D4A020` old gold)
- When to use: the "luxury/editorial" note — diagonal gold accent bars (per `design.notes`), the strongest layer in the background mesh (15%, the largest of the three), glow color (`--glow-color: #D4A020`).
- Surface area: substantial — gold gets the most background presence of the three colors and should be visually prominent, not a minor accent.
- Don't: don't under-use gold relative to cobalt — despite being named "secondary," it carries the theme's luxury signal and needs real visual weight.

### accent (`#E85C6A` rose-coral)
- When to use: the third, rarer counterpoint — gradient endpoint (`--gradient-accent`, cobalt→rose), a warm human note against the cooler cobalt/gold pairing.
- Surface area: smallest of the three — the background mesh gives it only 9% opacity, the lightest presence.
- Don't: don't scale rose-coral up to gold's visual weight — it's specifically the most restrained of the three roles.

## When To Use
- Investment/wealth-management, financial editorial, luxury portfolio-showcase content — the theme's own framing ("investment portfolio showcase," "overlapping metric cards") is literal.
- Content wanting genuine tricolor sophistication (cobalt+gold+rose together) rather than a single-accent luxury theme.
- Metric/data-dense financial storytelling that benefits from `--shadow-lg`/`xl`'s soft, editorial-magazine-style elevation.

## When NOT To Use
- Minimalist or restrained-palette contexts — this is a genuinely 3-color-plus-neutral system; content wanting a quiet 1-accent theme should look elsewhere in the catalog.
- Casual or youthful branding — Cormorant Garamond's tall serif and the champagne/cobalt/gold register are formal and "old money," not playful.
- Dark-mode contexts — no dark variant exists; the full effect depends on the warm champagne base.

## How To Use — Full Potential
- Use the full tricolor gradient border (`gradientBorder: cobalt→gold→rose`) on the single most prestigious element per view — a hero panel, a flagship metric card — since it's the one place all three colors combine and loses impact if spread across every component.
- Lead with the 3-layer radial gradient mesh as a body-level background, not confined to a hero — the "cobalt/gold/rose atmosphere" needs to feel ambient across the page, not localized.
- Reserve Cormorant Garamond for headlines/large figures and let Libre Franklin's light weight carry supporting metrics and body copy — the serif/sans contrast plus weight difference is what sells "editorial magazine," not just "finance."
- If only one thing: apply the cobalt→purple→gold gradient text (`--gradient-text`) to a key headline or figure — the fastest way to signal meridian-capital's luxury-finance register.

## Apply-Mode Notes
- Step 4a: give gold real visual weight, not a minor-accent treatment — it's the largest background-mesh layer and central to the "luxury" read; under-using it during harmonize is a common failure mode.
- Step 4j: preserve the tricolor gradient border for the single most important element — spreading it across many components dilutes what should be a rare, prestigious signal.
