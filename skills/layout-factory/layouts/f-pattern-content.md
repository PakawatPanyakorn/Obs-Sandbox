# f-pattern-content

**Archetype:** f-pattern-content · **Family:** editorial-narrative

## Core Concept

A scannable list where the first entry gets full attention and every entry beneath it carries progressively less horizontal read-weight, modeled directly on F-pattern eye-tracking heatmaps: readers fully process the first entry (heading plus a complete excerpt — both horizontal "bars" of the F), then scan down the left edge reading headings alone with steadily shrinking excerpts (the vertical stroke), while a narrow right rail gets almost no engagement at all. The hierarchy mechanism is decay, not contrast — unlike most archetypes in this catalog, the "less important" entries aren't demoted by a design choice, they're modeled after documented reading behavior. The tell that someone got it wrong: every entry has an identically-sized excerpt (defeats the whole premise) or the rail carries something load-bearing (violates the one rule real eye-tracking data justifies).

## When To Use

- Blog archive pages, documentation search-results pages, and knowledge-base article listings — any page that is fundamentally a ranked or chronological list of scannable entries.
- Search-results and marketplace listing pages where relevance ranking should visually correlate with how much a reader will actually process each result.
- Status pages (via the text-heavy variant) that want an at-a-glance state summary before a fuller incident narrative.

## When NOT To Use

- Content where every entry is genuinely, deliberately equal in importance — a numbered legal document, a set of parallel product tiers. Starving later items of excerpt length there isn't modeling real behavior, it's just arbitrarily shortchanging them. Use `card-catalogue-index` or `feature-trio-grid` instead.
- Anything meant to be read cover-to-cover rather than scanned — `single-column-editorial` or `masthead-feature-river` fit a single narrative or size-hierarchy front page better than a decaying list.
- A right rail with content the product actually needs seen — this archetype's rail region is explicitly a low-attention zone by design; if something genuinely needs visibility, it doesn't belong there regardless of available space.

## Region / Component Guidance

- **`.lf-fp-header`** (`masthead`, spans `1 / 13`): title plus a search/filter control. The judgment call: keep it to one row — a second row of nav or category chips starts competing with the lead entry.
- **`.lf-fp-lead`** (`lead`, spans `1 / 10`): the only entry with a full multi-line excerpt (`<p>`). The judgment call: resist adding a supporting image here "to make it pop" unless the content genuinely has one — an empty visual slot is fine, a decorative one isn't.
- **`.lf-fp-entry`** (`river`, spans `1 / 10`, repeated): each subsequent entry's `<p>` should be visibly shorter than the one before it, down to heading-only by the fourth or fifth entry. The judgment call people get wrong most often: writing every entry's excerpt the same length "for consistency" — that erases the entire structural point.
- **`.lf-fp-rail`** (`rail`, spans `10 / 13`): filters, related links, or promo only. The judgment call: never place a primary CTA or exclusive content here — this region exists specifically to demonstrate that a visually-present zone can still be a functionally low-attention one.

## Content-Type Notes

**textHeavy**: the lead gets a full 2-3 line excerpt; each river entry drops roughly one line until entries carry only a heading and a one-line metadata stamp (date, read time). This is the archetype's native mode — a blog or docs archive.

**chartHeavy**: only the lead entry pairs its excerpt with a small inline thumbnail or sparkline (`.lf-fp-thumb`); every entry after it drops the visual and keeps only a shrinking text line, since real eye-tracking data shows visual elements past the second or third list position get skipped almost entirely.

**cardOrListHeavy**: entries become search results or directory rows with the same heading-plus-shrinking-excerpt shape; resist wrapping each row in a bordered card — a hairline top-rule between `.lf-fp-entry` rows carries the separation instead, matching `masthead-feature-river`'s river convention.

## Medium Notes

`mediaAdaptation.presentation` and `.print` are both genuinely weak fits here, more so than most archetypes — the decay curve this pattern models is a property of screen-relative scanning behavior specifically, not something that survives translation to a fixed page or a projected slide. Don't try to preserve the decay curve in those mediums; fall back to a plain list instead.

## Pairing Notes

- **moss-cottage** — reach for this for a warm, browsable index register (a field-guide or archive feel) where the scannable-list concept fits naturally.
- **chalk-press** — reach for this when the demonstration should be as close to "type weight alone carries the signal" as possible, with zero color or box cues.
- **titanium-cloud** — reach for this for the archetype's most literal real-world habitat: a developer-platform documentation search results page.
