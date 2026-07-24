# magazine-well

**Archetype:** magazine-well · **Family:** editorial-narrative

## Core Concept
A dominant lead feature commands the top of the page; three to five secondary stories pool in a multi-column well beneath it, clearly subordinate by size. Size contrast alone communicates "this is the story that matters, these are supporting" — no color, no boxes. Well entries are NOT cards: no border/shadow/rounded corners, separated by whitespace and a hairline rule only, sized slightly by content length rather than forced uniform.

## When To Use
- Essays, briefs, narrative reports, opinion pieces — content that's prose top to bottom, with one piece genuinely more important than the rest.
- Analyst notes, quarterly reviews, research summaries organized around a handful of key results where one finding deserves top billing.
- Homepages, portfolio indexes, product/feature roundups — a set of comparable items with one that deserves the flagship spot.

## When NOT To Use
- Content where nothing is actually more important than anything else — inventing a "lead" from equally-weighted items is decorative, not structural; use a plain list or a peer-weighted archetype instead.
- Chart-heavy content where the temptation is a bare stat number in the well — that's the dashboard-trope this archetype is most exposed to drifting into; every exhibit needs a figure number, caption, and interpretation.
- Component libraries or UIs that genuinely need card-shaped boundaries — if so, keep borders hairline with no shadow and vary at least one dimension; identical rounded-shadow boxes in a uniform grid is the exact anti-pattern this archetype replaces.

## Region / Component Guidance
- **masthead** (`1 / 13`): small, quiet — never competes with the lead.
- **lead** (`1 / 13`): the dominant feature — full-width image, large headline, opening paragraph. Carries the page's one pull quote (large italic serif, left rule, no quotation marks, mid-way through the story).
- **well** (`1 / 13`, holds 3-5 entries in a row): secondary stories, each roughly a third the lead's visual weight. Never cards — whitespace and hairline rule separation, size varies slightly with actual content length.

## Content-Type Notes
- **textHeavy**: lead drops the image, becomes an opening paragraph (or two) at the largest type size instead; well entries stay text-only, a short heading plus one or two sentences, no thumbnails. Don't invent an image just to fill the lead — an empty visual slot is fine, a decorative one isn't.
- **chartHeavy**: lead becomes the single most important finding paired with one large captioned exhibit; well entries become 3-4 smaller captioned exhibits, each numbered, each with one line of interpretation. This is the variant most likely to drift into a dashboard — the discipline that prevents it: every chart is numbered, captioned, and carries a sentence of commentary, no exceptions.
- **cardOrListHeavy**: lead becomes the single flagship item (featured link, product, case study) with an outsized description; well entries become secondary items in a list, sized by actual content length, never forced into a uniform 3-up box grid.

## Medium Notes
- Print: lead spans the top of the first page; well entries flow as a 3-column band beneath, same page if it fits, else continuing to page 2.
- Markdown: lead as H1 + image + opening paragraph; well entries as H2 subsections beneath — size contrast is communicated via a longer opening paragraph for the lead and one short paragraph each for well entries, not markdown formatting alone.
- Presentation: lead becomes a title/hero slide; each well entry becomes its own single-idea slide, in order, following `slide-rule-of-thirds` internally.

## Pairing Notes
- `chalk-press` — its own description says "typographic hierarchy does all the work," this archetype's exact philosophy; brutally minimal editorial with an editorial-red accent.
- `tobacco-road` — field-journal naturalist aesthetic reads as long-form editorial content; distinct warm-vintage register from chalk-press despite both being light/paper-toned.
- `obsidian-mono` — dark austere counterpoint to the two light themes above, proving the archetype isn't tied to a light "newspaper" palette; "silence as design" suits a single dominant lead.
