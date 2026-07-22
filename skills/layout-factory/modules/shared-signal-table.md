# Shared Signal Table

Maps loose user language to a starting archetype + notable editorial devices. Used by Path C when the user describes a feel rather than naming an archetype directly, and by Path A/B when confirming a match. Always cross-check the mapped archetype's full entry in `shared-composition-archetypes.md` before committing — this table is a starting point, not a lookup that skips judgment.

| User says (or content evokes)... | Map to archetype | Notable devices to consider |
|---|---|---|
| "like the Economist / a broadsheet" | `masthead-feature-river` | Section breaks by rule, numbered exhibits if data-heavy |
| "like a McKinsey/BCG deck" or "consulting report" | `data-dense-report-grid` (report body) + `slide-rule-of-thirds` (if slides) | Numbered exhibits, captions, minimal prose |
| "like a Stripe/Linear docs page" | `single-column-editorial` or `asymmetric-split` (body + rail nav) | Sidebar for nav, callouts for warnings/tips |
| "like an academic paper" | `two-column-academic` | Footnotes, numbered sections/figures |
| "Tufte-style" / "handout-style" / "data-dense but readable" | `tufte-sidenote` or `data-dense-report-grid` | Sidenotes, captioned exhibits |
| "Swiss" / "clean grid" / "International Typographic Style" | `swiss-international-grid` | Minimal devices — let the grid and type carry it |
| "magazine" / "editorial spread" | `magazine-well` | Pull quotes, captions |
| "newspaper front page" | `masthead-feature-river` | Section breaks, river entries |
| "dashboard" / "analytics view" (genuinely navigable data) | `dashboard-with-rail` | — (rail carries the nav/filter role; avoid decorative stat tiles regardless) |
| "landing page" / "marketing page" | `z-pattern-landing` or `split-hero` | Minimal devices — hierarchy from scale/position, not editorial devices |
| "essay" / "long-form article" / "just let me write" | `single-column-editorial` | Pull quotes, drop cap, section breaks |
| "timeline" / "changelog" / "history of X" | `timeline-river` | — |
| "glossary" / "directory" / "reference list" | `card-catalogue-index` | Numbering if long enough to need cross-reference |
| "photo essay" / "gallery" / "portfolio" | `masonry-photo-essay` | Captions on every exhibit |
| "title slide" / "section divider" / "cover" | `poster-broadside` (single) or `cover-and-contents` (paired) | — |
| "annotated" / "review with comments" / "critical edition" | `marginalia-annotated` | Sidenotes (annotation-dense) |
| "bento" / "mosaic" / "varied grid" (genuine hierarchy, not decorative) | `bento-mosaic` | — |
| No signal at all — user just says "layout" or "make it look better" | `single-column-editorial` or `asymmetric-split` (see decision aid in `shared-composition-archetypes.md`) | Ask what medium and content shape before over-committing to devices |

## Resolving ambiguity

If a description maps to more than one plausible archetype (e.g. "data-dense but readable" could be `tufte-sidenote` or `data-dense-report-grid`), prefer:
- `tufte-sidenote` when citations/sources are a major component and margin space is available.
- `data-dense-report-grid` when charts/tables dominate over prose citations.

If the description names an archetype not in this table verbatim, check `shared-composition-archetypes.md` directly — the table only covers common loose phrasing, not the full catalog.
