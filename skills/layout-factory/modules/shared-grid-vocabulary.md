# Shared Grid Vocabulary

Reference for filling `grid`, `spacing`, and `composition.regions` in a preset, and for estimating grid structure from a screenshot (Path A) or existing markup (Path B).

## Grid types

| `grid.type` | What it means | Use when |
|---|---|---|
| `column` | Fixed N-column grid (typically 12), content spans a range of columns | Most web/report/dashboard layouts — the default working assumption |
| `modular` | Grid of both rows and columns forming true modules (a true 2D grid, not just column tracks) | Bento/mosaic layouts, poster grids, exhibit-heavy reports |
| `baseline-only` | No column grid — a single flowing column governed purely by vertical rhythm | Single-column editorial, essay layouts |
| `freeform-grid-anchored` | Elements placed by designed intent rather than strict tracks, but still snapped to a baseline/margin system | Poster/broadside, cover pages, asymmetric editorial spreads |

## Column math

- **12-column grid** is the default assumption for web/report layouts — divides cleanly into halves, thirds, and quarters.
- **Narrower grids** (4, 6, 8 columns) suit denser or more restrained compositions (academic journals, Swiss grid work).
- `regionSpans` use CSS grid-line syntax: `"1 / 9"` means "start at line 1, end at line 9" (spans columns 1-8 of a 12-column grid — i.e., 2/3 width).
- Never assign every region an equal span on a content set that isn't genuinely equal in importance — that's the uniform-card-grid tell (`anti-patterns.md`).

## Gutters and margins

- `gutter`: the space *between* columns. Typically 16-32px for web; wider (24-40px) for print-density report layouts; narrower (12-16px) for dense dashboards.
- `marginInline`: the space *outside* the grid, between the grid and the viewport/page edge. Common values: `5vw` for web, fixed page margins (e.g. `1in`, `72px`) for print/PDF targets.
- `maxWidth`: caps total grid width so lines don't over-extend on wide viewports. ~1200-1280px is typical for web; ~65-75ch for a single reading column regardless of container width.

## Baseline grid / vertical rhythm

- `baselineUnit`: the atomic vertical spacing unit (commonly 4px or 8px). All vertical spacing (line-height, margins, section gaps) should resolve to a multiple of this unit — this is what "grid discipline" means vertically, not just horizontally.
- `spacing.scale`: an explicit ordered list of allowed spacing values (e.g. `[4, 8, 12, 16, 24, 32, 48, 64]`), each a multiple of `baselineUnit`. Every spacing decision in a preset or an applied restructure should snap to a value in this list — this is the single biggest lever against "inconsistent gutters" (an anti-pattern gate item).
- `rhythm`: usually expressed as a multiple of body line-height (e.g. "1.5× body line-height between paragraphs, 3× between sections") — ties spacing decisions to the type scale rather than arbitrary pixel values.

## Breakpoints

- Define at least `sm` (mobile/narrow), `md` (tablet/half-width), `lg` (full desktop/print width) in `grid.breakpoints`.
- Each breakpoint should specify its own `columns` and `gutter` — and ideally a note on which regions collapse, reorder, or hide. A layout that just naively drops to `column-count: 1` at every breakpoint has failed the grid-discipline anti-pattern check.
- For non-web/print targets, breakpoints are less relevant — note in `mediaAdaptation.print` how the composition adapts to fixed page dimensions instead.

## Region-naming conventions

Use these consistent region `id` values across presets so apply-mode can reason about them generically:

| Region id | Typical role |
|---|---|
| `masthead` | Identity/title/nav band at the top |
| `lead` | The single dominant feature — biggest visual/textual weight |
| `river` | A flowing sequence of secondary content (briefs, headlines, entries) |
| `rail` | Narrow persistent sidebar — nav, filters, marginalia, citations |
| `well` | A contained zone where secondary content pools beneath a lead feature |
| `body` | Primary running text column |
| `sidenote` | Narrow margin column paired paragraph-by-paragraph with `body` |
| `footer` | Closing band — citations, colophon, page number, not a link sitemap |
| `exhibit` | A numbered/captioned chart, table, or figure, distinct from running commentary |

Not every archetype uses every region — pick only the ones the composition actually needs.
