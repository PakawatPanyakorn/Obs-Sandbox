# hazard-ward

An incident-report form pretending to be clean, with one loud physical detail it can't hide.

## Core Concept
Hazard Ward is built around a single tension: a clinical, almost sterile flat surface (`design.aesthetic: technical`, `elevation: flat`, every gradient and glow `none`) interrupted by one unmistakably physical object — the `.hazard-band`, a real repeating 45° black/yellow stripe rendered at the very top of the page, styled after actual hazard tape. Everything else stays deliberately quiet: the global background is a barely-visible diagonal watermark stripe at `patternOpacity: 0.035`, present for texture but not competing with the band. The second signature device is the `.redact` class — a solid ink block with transparent text, used inline within headings and body copy (not just in a badges row) to make "this field is withheld" a first-class typographic move rather than a placeholder. Typewriter-adjacent monospace throughout (`Space Mono` display, `Courier Prime` body) reinforces the "typed incident report," not a designed brand.

## Color Role Guidance
### primary (`#16181A` ink) — also `text`
- When to use: the "ink" of the document — headings, the hazard-band's dark stripe, primary buttons, and body text all draw from the same near-black. Primary and text intentionally share the same hex; there's one ink color for the whole form, the way an actual typed/stamped document has one ink.
- Surface area: dominant — it's both the text color and the primary action color, appearing constantly, unlike a typical UI where primary is reserved for a handful of CTAs.
- Don't: don't introduce a second "text" color distinct from primary during harmonize — the single-ink-color premise is deliberate, mirroring `cyber-terminal`'s single-typeface premise but for color instead of font.

### secondary (`#F4C418` hazard-yellow) — also `warning`
- When to use: exactly the hazard-band stripe and the "Level 2" / caution-tier badges — secondary and warning share the identical hex, so "the tape" and "a caution state" are literally the same signal, see `.tf-badge-warning` in the preset HTML.
- Surface area: minimal outside the band itself — a small badge or tag here and there. If yellow starts appearing as a general accent, the "this specific thing is hazardous" signal gets diluted.
- Don't: don't use secondary as a friendly/cheerful highlight color — its only job is caution.

### accent (`#D1382C` alert-red) — also `error`
- When to use: escalation past caution — "Containment Breach," "Level 2 Alert," anything that's actively wrong rather than merely flagged. Accent and error share the identical hex, same collapse logic as secondary/warning.
- Surface area: rare, reserved for the single most severe state visible in a given view.
- Don't: don't use accent and secondary together as a two-color palette system the way a typical UI pairs brand colors — here they're both *severity levels* on the same scale (caution → alert), not parallel brand accents.

## When To Use
- Incident-tracking, safety-reporting, or ops tools that want real bureaucratic stakes — the `.redact` and `.hazard-band` components are built for content that genuinely has "withheld field" and "escalation" states, not decoration.
- Status/audit-log dashboards wanting a stark, unglamorous register distinct from the typical soft SaaS dashboard look.
- Content that can use the report-card vocabulary (`.report-card .report-id`, incident numbering) literally.

## When NOT To Use
- Warm or approachable branding — the entire palette is flat ink/paper/hazard-signal with zero softness, by design.
- Content without a real "something is wrong or withheld" dimension — the redaction and hazard-stripe gimmicks read as gimmicky rather than functional if there's nothing in the content that's actually being flagged or withheld.
- Long-form prose reading — `Courier Prime` at `lineHeight: 1.6` is tuned for short field-log lines and report copy, not extended narrative paragraphs.

## How To Use — Full Potential
- Keep `.hazard-band` at the very top of the page, full width, above the header — it only reads as "physical tape stuck across the top" if it's the first thing on the page, not embedded mid-content.
- Use `.redact` inline within real sentences (as in the `t-h1`/`t-body` type-scale examples: "Containment Holding at ████ Meters") rather than only in a dedicated badges row — the gimmick's power is that withheld information interrupts otherwise-normal reading, not that there's a separate "redacted things" section.
- Keep the global watermark stripe barely visible (`patternOpacity: 0.035`) — if it's turned up, it competes with the hazard-band for "the one bold pattern" role and the contrast that makes the band land gets lost.
- If only one thing: put the black/yellow hazard-band across the top of an otherwise flat, quiet page. That single interruption is the whole theme.

## Apply-Mode Notes
- Step 4a (primary/secondary/accent distribution): this theme collapses text=primary and warning=secondary and error=accent — three deliberate two-way ties, not three independent roles. Don't invent distinct values for text or the status colors during harmonize; reuse the existing hex values exactly.
- Step 4j (background/texture): the ambient watermark stripe must stay near-invisible (`~0.035` opacity) — it exists so the page isn't a flat solid color (satisfying the "no plain solid background" rule) without stealing visual weight from the hazard-band, which is the theme's actual focal pattern.
- Step 4h (elevation/shadow): keep `shadow-colored: none` and overall shadows flat/minimal — any added glow or colored shadow undercuts the "sterile clinical form" premise this theme depends on.
