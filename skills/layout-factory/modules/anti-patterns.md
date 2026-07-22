# Anti-Slop Tells — Quick Reference

Run this checklist both at **create-time** (before writing a preset) and **apply-time** (before finalizing a restructure). Silently fix violations before showing the result.

## Critical — uniform card grids as default

| Tell | Fix |
|------|-----|
| 3-up/4-up icon-card grid used as the default composition regardless of content | Choose an archetype from `shared-composition-archetypes.md` that matches the content's actual shape. |
| Every "feature" or section wrapped in an identical bordered/shadowed box | Reserve boxes/borders for content that's a genuinely distinct unit (callout, stat, quote). Use whitespace + type hierarchy as the primary structuring tool elsewhere. |
| All cards same size and shape, no exceptions | Establish explicit size hierarchy tied to importance (see `shared-composition-archetypes.md` → hierarchy notes per archetype). Vary at least one dimension across any set of 3+. |
| No distinction between primary and secondary content — identical treatment throughout | Identify the 1-2 most important elements and give them structural dominance: larger span, isolated zone, earlier position. |
| A parallel set of items (features, findings, links) defaults to boxes because "that's what lists of things look like" | Consider a plain list, a table, a river, or a timeline before reaching for cards. Cards are one option, not the default. |

## Critical — no editorial structure

| Tell | Fix |
|------|-----|
| Long-form text (>~400 words) with zero pull quotes | Extract at least one quotable statement, placed per the archetype's `editorialFeatures.pullQuotes` convention. |
| Tangential or supporting info folded into the main flow instead of a sidebar/callout | Route asides, definitions, stats, citations to a rail or callout region. |
| Sourced claims cited only as inline parenthetical, no footnote/sidenote structure | Use the archetype's citation convention — endnote, sidenote, or footnote. |
| No section-break treatment — every heading transitions identically | Vary top-level section transitions per the archetype (rule, numeral, drop cap, deliberate whitespace jump). |
| Everything stacked as equal-weight blocks top to bottom, no designed reading order | Define an explicit `readingOrder` and at least one asymmetric emphasis. |

## Major — no grid discipline

| Tell | Fix |
|------|-----|
| Inconsistent gutter/margin values between sections (e.g. 24px here, 31px there) | Derive every spacing value from the preset's declared `spacing.scale`; snap outliers to the nearest step. |
| Elements not aligned to the shared column/baseline grid even though each looks fine in isolation | Verify every region's start/end aligns to a grid column line; verify vertical rhythm is a multiple of `baselineUnit`. |
| No consistent `maxWidth`/margin system across the page or document | One container `maxWidth` + `marginInline`, enforced throughout. |
| Grid just collapses to a single stacked column at small breakpoints with no deliberate adaptation | Define an explicit adapted composition per breakpoint (`grid.breakpoints`), not a naive collapse. |

## Major — generic dashboard look on non-dashboard content

| Tell | Fix |
|------|-----|
| Stat tiles / icon+number cards used to summarize a report or article's findings | State metrics in running text or as a numbered/captioned exhibit — unless the content is a genuine live dashboard. |
| "3 big numbers in a row" opener on a document meant to be read | Replace with a lead paragraph or masthead treatment. |
| Sidebar filter/nav rail bolted onto a document with no navigable sub-views | Only use `dashboard-with-rail` when content has genuine navigable facets. |
| Icon+label micro-cards decoratively summarizing prose content | Drop the icons; let typographic hierarchy carry the summary. |

## Cross-cutting — medium mismatch

| Tell | Fix |
|------|-----|
| Presentation content forced into a dense web layout with small text and many regions | Cross-check `mediaAdaptation.presentation` notes; presentation regions should be fewer and larger than a web/report layout. |
| Long-form article compressed into slide-style bullet fragments | Cross-check the target's actual output medium before finalizing regions — don't reuse a web region map for a slide deck outline. |
| A preset's `mediaAdaptation` field for the current target medium is empty or was never consulted | Read the field before restructuring. If genuinely absent for this medium, write reasonable adaptation notes into the preset rather than skipping the check. |
