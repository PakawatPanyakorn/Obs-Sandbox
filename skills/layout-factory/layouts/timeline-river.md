# timeline-river

**Archetype:** timeline-river · **Family:** editorial-narrative

## Core Concept
A continuous vertical spine anchors chronological entries alternating left and right so the eye has to actually read each one rather than skim a flat scroll. Exactly one entry — chosen by narrative significance, not chronological position (it may fall mid-sequence) — breaks the alternation, spans near-full width, and is the only entry with surface fill, hero shadow, and hero gradient. A second enlarged entry would erase the hierarchy and flatten the page back into an undifferentiated list of boxes.

## When To Use
- Engineering retrospectives, project journals, changelogs, personal essay series told in chronological installments.
- Expedition/dive logs with a measurement at each stage, quarterly retrospectives with a metric per phase, before/after case studies charting a project's timeline.
- Product roadmaps, release histories, milestone indexes ordered by ship date, with one flagship release deserving outsized treatment.

## When NOT To Use
- Anywhere the instinct is to force every entry to the same visual weight because they're "all roadmap items" — only the pivotal entry earns extra size; sizing everything identically flattens hierarchy back into a uniform card grid.
- Content without genuine chronological structure — the spine and alternation only make sense for entries that are actually ordered in time.
- Chart-heavy content risking a floating number with no caption — every exhibit on the spine needs a caption and interpretation sentence, the dashboard-trope tell applies here too.

## Region / Component Guidance
- **masthead** (`1 / 13`): small, quiet — never competes with the pivotal entry.
- **spine** (`6 / 8`, not a content region): a continuous vertical rule the entries anchor to, running the full height of the sequence — centered on desktop, shifted to the left margin on narrow/print layouts.
- **river** (`1/6` left or `8/13` right, alternating, repeated): secondary entries in chronological order, alternating sides per entry — never all on one side. No border/shadow/rounded box, just a hairline node marker and text.
- **pivotal** (`2 / 12`, exactly one): the entry singled out at lead scale, chosen by significance not position. Carries the archetype's one reserved pull quote (never in a river entry, so its presence alone signals which entry is pivotal).

## Content-Type Notes
- **textHeavy**: entries drop any image/exhibit placeholder — each is a date label, heading, one or two sentences; pivotal entry gets a longer paragraph and the pull quote instead of a photo. Don't invent a photo/icon for every node just to fill space.
- **chartHeavy**: each river entry pairs a small captioned exhibit with one line of interpretation; pivotal entry gets the single largest exhibit on the page plus the pull quote, positioned wherever it falls chronologically rather than always first.
- **cardOrListHeavy**: entries become individual releases/milestones sized by actual content — most get one line, the pivotal entry (flagship release) gets an outsized description, never forced into uniform card boxes.

## Medium Notes
- Print: spine renders as a single rule down the page's left margin — centered alternation doesn't survive; river entries stack single-column, alternation expressed only as left/right indent. Pivotal entry keeps its border/shadow treatment as a printed box.
- Markdown: degrades to a strict sequence of H2/H3 headings, one per entry, opening with its date/sequence label — left/right rhythm is lost entirely, chronological order becomes the only remaining structural signal. Pivotal entry distinguished by an H1-level heading and a longer opening paragraph instead of side placement.
- Presentation: one slide per era/phase in strict chronological order; the pivotal entry gets its own emphasized slide (larger date treatment, full-bleed background) rather than sharing with river entries, and doesn't need to be first or last in the deck.

## Pairing Notes
- `biolumen-depths` — its own "scientific field log meets alien wilderness" register maps directly onto a dive/expedition log; teal glow node markers and mono depth-reading labels read as literal specimen timestamps.
- `copper-alchemist` — dark steampunk workshop journal; a mechanical invention log built entry-by-entry is a distinct, non-scientific chronological register, with copper accent nodes reading as ledger entries in an alchemist's logbook.
