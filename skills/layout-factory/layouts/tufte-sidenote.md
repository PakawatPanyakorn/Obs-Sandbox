# tufte-sidenote

**Archetype:** tufte-sidenote · **Family:** data-dense-report

## Core Concept
A justified reading column paired with a permanent right-margin column where every citation, definition, and small figure lives in the exact row of the paragraph that calls for it — row-locked via a shared CSS grid row, never floated to the nearest free space and never folded into an inline parenthetical. This is the precision end of a spectrum shared with two sibling archetypes: `asymmetric-split`'s rail runs independently alongside a *section* (not row-locked), and `marginalia-annotated`'s gloss column free-flows in document order so several entries can stack beside one dense paragraph. Only this archetype pins exactly one row per paragraph.

## When To Use
- Research writeups, technical explainers with citations, annotated specs, close-reading essays — content where a citation belongs precisely beside the sentence it supports.
- Technical reports building an argument in the body while carrying methodology notes, data-source citations, and secondary corroborating series in the margin.
- Annotated bibliographies, spec comparisons with sourced claims, review write-ups citing an external benchmark per item.

## When NOT To Use
- Content wanting frequent claim-level commentary that clusters unevenly (several notes on one contentious paragraph, none on others) — that free-flowing density belongs to `marginalia-annotated`, not this archetype's strict per-paragraph row lock.
- Anywhere the instinct is to attach a note to every paragraph out of habit — an unused margin for several consecutive rows is expected and correct; forcing a note onto every row turns citation into decoration.
- Chart-heavy content wanting to move the primary chart into the sidenote column because there's a slot free — a body-width exhibit demoted to margin width becomes illegible and reads as an afterthought.

## Region / Component Guidance
- **body** (`1 / 9`): the primary reading column carrying the argument — full sentence-level prose, headings, the one pull quote (which never spans into the sidenote gutter), and the one body-width primary exhibit in chart-heavy content.
- **sidenote** (`9 / 13`): a paragraph-anchored margin column for citations, definitions, and small figures. Shares a CSS grid row with the specific paragraph it annotates — never a free-floating column of its own, empty for any paragraph with nothing to cite. Not a generic sidebar: it carries no navigation or filters, only paragraph-anchored citations.

## Content-Type Notes
- **textHeavy**: most paragraphs carry zero or one sidenote; a handful carry two stacked notes separated by a hairline rule. Notes stay 1-3 sentences so they never outgrow their anchored row.
- **chartHeavy**: body keeps the one primary body-width exhibit carrying the main finding; margin hosts small supporting figures instead (a corroborating series, a source citation, a methodology note) — never a shrunk copy of the main chart.
- **cardOrListHeavy**: comparable items become short numbered entries in the body column; each entry's sidenote carries its source, benchmark, or one-line spec instead of a rating badge or tag row. Don't turn the sidenote column into a second set of mini-cards — keep notes plain, unboxed text.

## Medium Notes
- Print: this is the archetype's native medium, unchanged from Tufte's own handouts — recto/verso margins swap so the sidenote column always falls on the outer edge of the spread; figure/section numbering can run continuously or restart per page.
- Markdown: true side-margin notes don't render flat — degrade to inline footnote-style asides (`[^1]`-style reference marker, note text collected as a numbered list at section end), never as an inline parenthetical, which is the exact anti-pattern this archetype replaces.
- Presentation: poor fit — a slide has no sustained paragraph flow to anchor a note to; collapse sidenotes to a short numbered endnote list on a dedicated closing slide instead of forcing them onto the slide margin.

## Pairing Notes
- `vellum-codex` — illuminated manuscripts are the historical ancestor of the margin note; the theme's antiquarian register and IM Fell English body face read as scholarly apparatus, not decoration.
- `darkroom-safelight` — its frame-number, contact-sheet motif and chemical monospace notation already read as lab-notebook annotation, a natural register for methodology notes and source citations.
- `argent-vigil` — its own type sample names "marginalia, footnotes, the scribe's quiet hand" for small muted text outright, a heraldic-archive voice suited to citation-dense writeups.
