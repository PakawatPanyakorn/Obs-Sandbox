# slide-master-deck-grid

**Archetype:** slide-master-deck-grid · **Family:** grid-discipline

## Core Concept
Operates one level up from a single slide: it defines the title-zone and footer/citation-zone margins that stay pixel-identical across every slide in a deck, regardless of which per-slide content archetype (`slide-rule-of-thirds`, `poster-broadside`, a plain list) fills the body zone in between. The consistency itself is the deliverable, not any one slide's content shape. The masthead/footer being pixel-identical everywhere is the whole point here — not the uniform-grid anti-pattern it would be elsewhere, because the body zone is free to diverge structurally slide to slide.

## When To Use
- Board decks, keynote talks, thesis-defense decks carrying a long-form narrative across many slides.
- Quarterly business reviews or data-heavy pitch decks built around a handful of key exhibits, each getting a numbered figure treatment.
- Roadmap decks, org/team slides, feature-comparison decks organized as a set of comparable items across many slides.

## When NOT To Use
- Anywhere the instinct is to resize the masthead or footer to make room for a busy chart — if an exhibit needs more room, split it across two slides; shrinking the fixed zones breaks the one guarantee this archetype makes.
- Body-zone lists that want to become a uniform icon-card grid — the fixed masthead/footer already supply the deck's consistency; the body doesn't need to add more sameness on top of it.
- A single standalone slide or one-off visual — this archetype's value is entirely about consistency *across* a multi-slide deck; on one slide it's just unnecessary structure.

## Region / Component Guidance
- **masthead** (title zone, fixed): same height, same type treatment, same position on every slide in the deck — this is the fixed part, establishing "you're still in this deck" before the eye drops into the body.
- **body** (content zone, varies per slide, ~flex: 1 of the slide box): the only region a per-slide archetype is free to reshape — prose, a chart, a list, a rule-of-thirds split. This is where structural variety belongs.
- **footer** (page number/citation zone, fixed): carries the slide number and a running citation or confidentiality line — position never moves, only the numbers increment.

## Content-Type Notes
- **textHeavy**: body zone becomes a single flowing block of prose per slide — a condensed opening statement or finding, not a full paragraph. Don't cram a full paragraph at illegible size; a deck's body zone always compresses, regardless of content type.
- **chartHeavy**: body zone hosts one dominant captioned exhibit per slide, numbered like a figure, following whichever per-slide archetype the content calls for. Only the single most important slide's exhibit gets the theme's hero shadow/gradient; the rest stay flat.
- **cardOrListHeavy**: body zone becomes a numbered agenda, roadmap, or comparison list, rule-separated and sized by actual content length. Don't turn it into a uniform icon-card grid.

## Medium Notes
- Presentation: this archetype IS the slide master — apply it directly as the master/theme layer in the presentation tool (PowerPoint slide master, Keynote master, Google Slides theme). It only ever owns the margins; the body zone is populated per-slide by whatever archetype that slide needs.
- Print: each slide becomes one landscape page; masthead becomes a running header, footer becomes a running footer (page number + citation) — the same page-master concept a print document uses, one slide per page.
- Markdown: one H2 per slide (masthead title), body content beneath in whatever form fits, and a trailing citation line per slide standing in for the footer — the fixed pixel position becomes a fixed textual convention instead.

## Pairing Notes
- `vault-theorem` — wealth-management "institutional allocation framework" with tiered navigation is exactly the authoritative, unchanging title/body/footer zoning a board or LP deck needs slide after slide.
- `thermal-fade` — its numbered TXN stamp and literal transmission-log discipline mirror a deck's numbered-slide, fixed-footer-citation discipline line for line.
