# embassy-gold

Institutional gravitas meets Art Deco precision — a navy/gold/ivory triad tight enough to read as a chancery or private bank, built on a literal drafting-board grid rather than decorative Deco flourish.

## Core Concept
Warm ivory canvas (`#F0EBE0`) with a thin 48px gold-tinted architectural grid ("drafting board precision meets embassy hall"), Cormorant Garamond's refined display serif for authority against Libre Franklin's clean 300-weight sans for legibility. `gradientBorder: linear-gradient(90deg, #1E3A5F, #D4AF37, #1E3A5F)` — navy-gold-navy, symmetric — is the theme's signature "decorative gold rule between sections," a very specific Deco device distinct from a generic accent border. Every shadow carries a hairline border ring (`0 0 0 1px rgba(200,190,168,*)`) alongside its blur, giving surfaces a bordered, engraved-plaque quality even at rest.

## Color Role Guidance

### primary (`#1E3A5F` deep navy)
- When to use: institutional authority — primary buttons (`--gradient-button`, a navy-only gradient, deliberately not gold), headers, the base of the navy-gold-navy border rule.
- Surface area: generous — navy is the theme's structural anchor, appropriate for large surfaces (headers, primary UI) not just accents.
- Don't: don't substitute gold for navy in primary-button contexts — the theme explicitly keeps CTAs navy, reserving gold for the *text* gradient and decorative rule, a deliberate separation of "action color" from "ornament color."

### secondary (`#B8860B` dark goldenrod)
- When to use: a deeper, more muted gold than accent — text-gradient start (`--gradient-text` runs goldenrod→gold), the "ornamental but structural" gold tone.
- Surface area: moderate — rules, borders, gradient starts; less flashy than accent's brighter gold.
- Don't: don't conflate secondary with accent even though both are gold — secondary is the muted/structural gold, accent is the bright/decorative gold; they play different registers in gradients.

### accent (`#D4AF37` bright gold)
- When to use: the brightest ornamental note — text-gradient endpoint, the center stop of the navy-gold-navy border rule, the "precious metal" flourish.
- Surface area: small and precise — thin rules, gradient highlights, never a fill.
- Don't: don't use accent gold as a background fill or large surface — its entire value is as a thin, precious accent line, consistent with real Art Deco gold leaf detailing.

## When To Use
- Law firms, private banks, embassies, luxury institutions, or "old money" corporate branding wanting authority without coldness.
- Content that benefits from a genuine navy/gold/ivory triad with Deco-precision geometry (thin grids, symmetric gold rules) rather than a generic "gold accent on dark" luxury cliché.
- Formal editorial or annual-report-style content needing high hierarchy clarity (`hierarchyClarity: high`) with restrained ornament.

## When NOT To Use
- Casual, playful, or youth-oriented branding — the theme is built entirely around institutional formality.
- Content needing rounded, soft, approachable UI — `borderRadius: 0px` and hairline-bordered shadows throughout are deliberately crisp and architectural.
- Dark-mode contexts — there's no dark variant; the ivory/navy/gold triad depends on the light, paper-like base.

## How To Use — Full Potential
- Use the symmetric navy-gold-navy gradient rule (`gradientBorder`) as a section divider, not a generic border — it's a specific Deco device (echoing decorative metal inlay strips) and reads as "designed," not just "styled," when used exactly for that purpose.
- Keep primary buttons navy and reserve the gold gradient for headline text only — this action/ornament split is what keeps the theme feeling institutional rather than "gold-heavy luxury generic."
- Let the thin architectural grid background remain visible across full-page reading surfaces — it's what grounds the Deco ornament in genuine precision/drafting-board logic rather than decoration for its own sake.
- If only one thing: apply the navy-gold-navy gradient rule as a divider between two content sections — the single fastest, most recognizable signal of embassy-gold.

## Apply-Mode Notes
- Step 4a: keep primary (navy) as the action color and secondary/accent (gold tones) as ornamental/text-gradient roles — don't swap gold into CTA buttons during harmonize, that inversion breaks the theme's action/ornament discipline.
- Step 4d: any section-divider harmonize should use the navy-gold-navy symmetric gradient rule specifically, not a generic single-color border.
