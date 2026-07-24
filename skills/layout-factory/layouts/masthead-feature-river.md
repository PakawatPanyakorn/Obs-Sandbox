# masthead-feature-river

**Archetype:** masthead-feature-river · **Family:** editorial-narrative

## Core Concept
A formal, bold nameplate identifies the page, one dominant feature story owns the top, and a genuine river of 6-10 small briefs flows beneath it in true CSS multi-column text flow with column rules — never a stacked list, never a grid of boxes. Where `magazine-well` pairs a lead with a small quiet well of 3-5 peers, this archetype exists for when there are too many small items for a well to hold and they need to flow, newspaper-front-page style.

## When To Use
- Weekly digests, editorial newsletters, briefing memos — one big story and many small textual updates that genuinely need to flow rather than stack.
- Weekly metrics recaps or briefing decks with one headline finding and many small KPIs beneath it, each still numbered and interpreted like a figure.
- Release-note digests, link roundups, "everything else we shipped" sections with eight or more small items.

## When NOT To Use
- Content with only 3-5 secondary items — a river needs enough entries to actually flow; use `magazine-well` instead below that count.
- Anywhere the temptation is to pad every brief to identical length to make columns balance — that raggedness is the point; forcing uniform length erases the "river," not "list" read.
- Chart-heavy briefs risking bare numbers with no interpretation — that's the dashboard-trope this skill exists to avoid, not this archetype.

## Region / Component Guidance
- **masthead** (`1 / 13`): bold, centered, formal publication nameplate — unlike `magazine-well`'s quiet identity strip, this region is meant to be read, not skipped.
- **lead** (`1 / 13`): the dominant feature — full-width image, drop cap opening, largest headline on the page. Carries the page's one pull quote (large italic, left rule, bold — same scarcity rule as magazine-well: exactly one, never one per river brief).
- **river** (`1 / 13`): a dense multi-column flow of 6-10 briefs of varying length, separated by column rules, never boxed. Only the lead ever receives shadow/surface/gradient treatment; river items stay flat regardless of theme.

## Content-Type Notes
- **textHeavy**: lead drops its image, leads with a longer opening paragraph carrying a drop cap; river becomes short prose briefs (1-3 sentences each, varying length) flowing through real CSS columns. Don't pad briefs to equal length just to balance columns visually.
- **chartHeavy**: lead pairs with one large captioned exhibit (same scarcity rule as magazine-well's lead); river becomes a dense flow of small captioned stat briefs — mini exhibit, one-line label, one-line interpretation, several per column, each numbered like a figure.
- **cardOrListHeavy**: lead becomes the flagship item with an outsized description; river becomes a dense flowing list of smaller items (headline + one line each), ordered by importance, with varying line counts so columns break unevenly rather than reading as a matched set of boxes.

## Medium Notes
- Print: broadsheet/letter page — masthead across the top of page 1, lead beneath it, river runs as true newspaper columns (3-4) at the bottom, continuing to page 2 if needed; column-rule prints as a hairline.
- Markdown: masthead becomes a title plus italic dateline; lead becomes H1 + opening paragraphs; river becomes a flat H3 list, one per brief, single column — the multi-column flow doesn't survive, so brief order and relative length carry hierarchy instead.
- Presentation: masthead becomes the title slide's identity strip (or drops if the deck has its own title master); lead becomes the opening slide; river collapses to one "Agenda"/"Overview" slide with each brief as a single bullet line, ranked and trimmed to what's worth a line.

## Pairing Notes
- `soviet-agitprop` — constructivist propaganda posters ARE front-page composition: bold nameplate, one dominant image, dense columns of smaller notices beneath; hard offset shadows read as press-run authority on the lead.
- `prism-ledger` — its own component set literally is a broadsheet: centered masthead with volume/issue dateline, two-column feature spread, ruled ledger — the closest real-world referent to this archetype in the library.
- `riso-proof` — a risograph zine front page is this archetype in miniature; misregistration shadows and strict 3-ink discipline give the river a distinct small-press identity, different from prism-ledger's polished broadsheet.
