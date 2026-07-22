# Shared Composition Archetypes

Master catalog for Path C (named-archetype requests, e.g. "give me a Swiss grid layout") and for mapping extracted structures (Path A/B) onto a recognizable pattern. Each entry gives the `archetype` id, `family`, structural summary, typical regions/hierarchy, and a one-line note on how it adapts across mediums. Use these as the seed for `composition`, `grid`, and `mediaAdaptation` fields when authoring a preset.

Families: `grid-discipline` (structure-forward, disciplined column math) · `editorial-narrative` (reading-order and story-forward) · `dashboard-legitimate` (genuinely navigable/data-facet content) · `data-dense-report` (exhibits + commentary, analytical).

---

## 1. `swiss-international-grid` — Swiss / International Typographic Style grid *(grid-discipline)*

Strict modular column grid (often 6 or 12 col), flush-left ragged-right sans type, grid-locked photography, asymmetric but disciplined placement, minimal ornament, generous whitespace used structurally not decoratively. Regions: `masthead`, `lead`, `body`, occasional `exhibit`. Hierarchy via scale and position, never boxes/shadows. Adapts to presentations as a strict title/body/footer margin system repeated per slide; to print as a classic modular grid with consistent margins.

## 2. `single-column-editorial` — Single-column editorial *(editorial-narrative)*

One constrained-width reading column (~65-75ch), generous top/bottom margins, optional drop cap on the opening paragraph. Regions: `masthead` (title/byline), `body`, occasional `sidenote` in the margin if width allows. The classic essay/long-form article layout — minimal chrome, all hierarchy from type scale and whitespace. Adapts to markdown almost natively (it *is* markdown's default shape); to presentations as a title-slide + one-idea-per-slide sequence.

## 3. `magazine-well` — Magazine well *(editorial-narrative)*

A large lead image/feature dominates the upper zone; secondary stories arrange in a "well" beneath, text wrapping in multiple columns around it. Regions: `lead`, `well` (containing several smaller `river` entries), `rail` optional. Hierarchy is explicit: one dominant story, several smaller ones clearly subordinate by size. Adapts to reports as an executive-summary-dominant cover with supporting sections below; to web as a homepage/landing hero + content well.

## 4. `split-hero` — Split-hero *(grid-discipline)*

Page/screen bisected into unequal halves (e.g. 60/40 or 55/45) — one side visual/image, the other text/CTA. Never centered, never 50/50. Regions: `lead` (dominant half), `body` (secondary half). Simple but disciplined — the asymmetry itself is the structuring device. Adapts to slides as a two-zone slide master (visual anchor + text); to print as a facing-page spread.

## 5. `dashboard-with-rail` — Dashboard-with-rail *(dashboard-legitimate)*

Main content area plus a persistent narrow side rail (nav/filters/metadata). Stat modules are confined to the rail or a clearly bounded summary zone — never scattered as cards through the body. Regions: `rail`, `body`, optional `exhibit` zones within body. Use only when content has genuinely navigable facets (filters, sections, live data) — otherwise this is the "generic dashboard on a document" anti-pattern. Rarely adapts well to print/slides; flag as HTML/web-primary in `mediaAdaptation`.

## 6. `masthead-feature-river` — Masthead + feature + river *(editorial-narrative)*

Newspaper front-page pattern: identity masthead band at top, one dominant feature story, a "river" of smaller headlines/briefs flowing below in multi-column text. Regions: `masthead`, `lead`, `river`. Strong, explicit hierarchy — this archetype exists specifically to avoid uniform-weight content. Adapts to reports as title block + executive summary + supporting sections; to slides as title slide + agenda/overview slide.

## 7. `asymmetric-split` — Asymmetric split (rule-of-thirds) *(grid-discipline)*

Unequal column widths — one dominant content zone (~2/3), one narrow marginalia zone (~1/3). Never 50/50. Regions: `body` (2/3), `rail` (1/3, for citations/related/notes). Simple, robust, and hard to make look generic because the ratio itself creates deliberate imbalance. Adapts to nearly every medium — the ratio idea translates directly to slide layouts and print margins.

## 8. `tufte-sidenote` — Tufte-style sidenote layout *(data-dense-report)*

Main text column plus a wide right margin reserved for sidenotes, citations, and small figures, each aligned to the paragraph that cites it (Edward Tufte's handout/book convention). Regions: `body`, `sidenote`. This is the strongest available alternative to inline footnotes AND to a generic sidebar — the sidenote is paragraph-anchored, not just column-anchored. Adapts to markdown as inline footnote-style asides if true sidenotes aren't supported by the renderer; to web via `float`/grid-column sidenotes; poor fit for slides.

## 9. `data-dense-report-grid` — Data-dense report grid (exhibit + commentary) *(data-dense-report)*

Numbered/captioned exhibits (charts/tables) interleaved with tight running commentary — Bloomberg Businessweek / analyst-report register, explicitly not KPI tiles. Regions: `body`, repeated `exhibit` blocks each with a caption/number, occasional `sidenote` for citations. The defining discipline: every chart/table is numbered and captioned like a figure, never a floating card. Adapts directly to presentations (one exhibit + commentary per slide) and print (classic analyst-report layout).

## 10. `two-column-academic` — Two-column academic/journal layout *(grid-discipline)*

Balanced twin text columns, running headers/footers, figures spanning both columns when they need width. Regions: `masthead` (title/authors/abstract, full width), `body` (two-column), `exhibit` (full-width when large). Classic journal-paper register — signals rigor and density. Poor fit for slides; strong fit for print/PDF.

## 11. `marginalia-annotated` — Marginalia / annotated document *(data-dense-report)*

Main text plus an inline annotation column, like a critical edition or a heavily glossed manuscript — built for review/commentary documents (feedback on a draft, annotated proposal). Regions: `body`, `sidenote` (annotation-focused, denser and more frequent than Tufte's citation-oriented sidenote). Adapts to markdown as inline blockquote comments if a true two-column layout isn't available.

## 12. `bento-mosaic` — Bento / modular mosaic *(grid-discipline)*

Deliberately varied-size grid cells — not uniform — sized by genuine content importance. Explicitly distinguished from the uniform-card-grid anti-pattern: this archetype is only valid when cell size actually maps to a real hierarchy signal (importance, recency, data density), never applied decoratively to make content "look organized." Regions: several `exhibit`/`lead`/`river` cells of genuinely different `columnSpan`s. Adapts to web/slides; awkward in single-column markdown (degrade to a sequential list ordered by the same hierarchy).

## 13. `timeline-river` — Timeline / chronological river *(editorial-narrative)*

Vertical or horizontal timeline structure organizing entries by date/sequence, alternating emphasis left-right (or above-below) to avoid monotony. Regions: repeated `river` entries anchored to a spine, occasional `lead` for a pivotal entry. Good fit for case studies, changelogs, project retrospectives. Adapts to markdown as a chronological heading sequence; to slides as one slide per era/phase.

## 14. `card-catalogue-index` — Card-catalogue / index layout *(grid-discipline)*

Structured list/table-like reference layout (directory, glossary, index) — alignment and rules carry the structure, no boxes or shadows. Regions: `body` organized as a dense aligned list/table, optional `rail` for an alphabetic/category jump-nav. The deliberate anti-card answer for genuinely list-shaped content (the one case where a "grid of items" is legitimate — but expressed as rows/columns of a real table, not decorative cards). Adapts to markdown natively as a table; to web as a real `<table>` or definition list.

## 15. `poster-broadside` — Poster / broadside *(grid-discipline)*

Single dominant typographic statement; hierarchy driven entirely by scale contrast, not boxes. Regions: `lead` only, or `lead` + minimal `body`. For cover pages, section dividers, title slides — not for content-dense pages. Adapts directly and strongly to slide title/section-divider slides; poor fit for continuous reading content.

## 16. `cover-and-contents` — Cover + contents *(editorial-narrative)*

Two-page/two-screen pairing: full-bleed title/cover treatment (see `poster-broadside`) followed by a structured contents/table-of-contents page. Regions: page 1 = `lead` (full-bleed), page 2 = `body` organized as a numbered/sectioned index. Purpose-built for reports and decks that need a formal opening. Adapts to slides as title slide + agenda slide; to print as literal cover + TOC pages.

## 17. `masonry-photo-essay` — Masonry photo-essay *(editorial-narrative)*

Variable-height image blocks with cutline captions, non-uniform sizing driven by each image's actual aspect ratio and narrative weight — not a feature-icon grid. Regions: repeated `exhibit` entries of varying `columnSpan`/height, each captioned. For photo essays, case-study galleries, visual portfolios. Weak fit for markdown/print without real image support; strong fit for web.

## 18. `slide-rule-of-thirds` — Slide rule-of-thirds content layout *(grid-discipline)*

Presentation-specific: a visual anchor occupies roughly one third of the slide, supporting text/bullets occupy the remaining two-thirds (or vice-versa) — replaces the generic centered bullet-list slide. Regions: `lead` (visual, 1/3), `body` (text, 2/3). This is the default single-slide content archetype layout-factory should reach for instead of a centered bullet list. `mediaAdaptation.presentation` is this archetype's primary reason to exist; HTML/print notes are secondary.

## 19. `z-pattern-landing` — Z-pattern landing composition *(grid-discipline)*

Layout following the natural Z eye-scan path (top-left → top-right → bottom-left → bottom-right) — for landing/marketing pages needing directed attention flow toward a single action. Regions: `masthead` (logo top-left, CTA top-right), `lead` (visual + supporting copy along the diagonal), `body` (closing CTA bottom-right). Web-primary; doesn't translate meaningfully to print/slides — note this plainly in `mediaAdaptation` rather than forcing a fit.

## 20. `slide-master-deck-grid` — Slide-master deck grid *(grid-discipline)*

Presentation-native grid discipline applied across an entire deck: consistent title-zone, body-zone, and footer/citation-zone margins on every slide, regardless of that slide's content archetype (which might itself be `slide-rule-of-thirds`, `poster-broadside`, etc. per-slide). Regions: `masthead` (title zone, fixed position across deck), `body` (content zone, varies per slide), `footer` (page number/citation, fixed). This is the deck-level meta-grid, not a single-slide content pattern — pair it with a per-slide archetype for actual content layout.

---

## Choosing among archetypes (Path C decision aid)

When the request gives real signal, match on:
- **Content shape**: single narrative → `single-column-editorial`/`masthead-feature-river`; parallel findings/exhibits → `data-dense-report-grid`/`bento-mosaic`; chronological → `timeline-river`; reference/lookup → `card-catalogue-index`.
- **Medium**: presentation-first requests should default to `slide-rule-of-thirds` (per-slide) + `slide-master-deck-grid` (deck-level), not a web archetype squeezed onto slides.
- **Family balance when seeding**: prefer covering multiple families over picking near-duplicates within one family.

When the request gives no signal at all, do not default to a card grid or a dashboard — default to `single-column-editorial` or `asymmetric-split`, the two archetypes least likely to misfire on unknown content.
