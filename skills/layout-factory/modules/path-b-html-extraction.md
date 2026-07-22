# Path B: HTML/CSS Extraction

Extract a composition archetype from an existing HTML/CSS file by mining structural signals directly from the markup and stylesheet, rather than visually.

## Signal-mining priority order

Read the file and check each of these, in order — earlier signals are more reliable than later ones:

| Priority | Source | What it tells you |
|---|---|---|
| 1 | `grid-template-columns` / `grid-template-areas` on a container element | Direct, authoritative column structure and named regions — use as-is |
| 2 | `max-width`, `margin-inline`/`margin: 0 auto`, container width on `.container`/`.wrapper`/`main` | Overall `grid.maxWidth`/`marginInline` |
| 3 | `@media` breakpoints and their column/width overrides | `grid.breakpoints` values |
| 4 | Flex layouts with explicit `flex-basis`/`width` splits | Implicit column structure when no CSS Grid is present |
| 5 | `column-count`/`columns` (CSS multicol) on text blocks | Multi-column reading flow (relevant to `two-column-academic`, `masthead-feature-river`) |
| 6 | Semantic HTML5 sectioning (`<aside>`, `<figure>`, `<blockquote>`, `<nav>`) | Implies `rail`, `exhibit`, pull-quote, and `masthead` regions respectively, even without explicit grid CSS |
| 7 | Existing spacing custom properties (`--space-*`, `--gap-*`, or repeated literal values) | `spacing.scale` — derive from the observed value set, snapping near-duplicates together |

## Steps

1. **Read the file.**
2. **Mine signals** in the priority order above; higher-priority signals override lower ones when they conflict.
3. **Map to `composition.regions` + `grid.regionSpans`** using the region-naming conventions in `modules/shared-grid-vocabulary.md`.
4. **Derive `spacing.scale`** from observed margin/padding/gap values — snap outliers to the nearest consistent step rather than preserving every literal value found.
5. **Detect existing editorial features** already present (pull quotes, sidebars, footnotes, captions) — read `modules/shared-editorial-devices.md` to name them correctly.
6. **Map to the nearest catalog archetype** — read `modules/shared-composition-archetypes.md`. Note hybrids rather than forcing a false match.
7. **Fill gaps with context** — read `modules/shared-signal-table.md` if the file's purpose/medium isn't obvious from the markup alone, or ask.
8. **Name** — ask if not provided.
9. **Anti-pattern gate** — read `modules/anti-patterns.md`. If the source file itself is a uniform card grid or other anti-pattern, do not extract that flaw as the preset's structure — either extract the underlying intent (what was this trying to organize?) or ask whether to proceed.
10. **Write** using `modules/preset-template.html`, `source: "html"`, `sourceFile: "<path>"` → update `index.html` LAYOUTS array.

## Notes

- If the file has a theme-factory signature (`applied by obs-theme-factory`), that's a color/type signal only — ignore it for structural extraction, but note in the new preset's `themeCompatibility.note` that the source already demonstrates safe coexistence.
- A file with no CSS Grid, no flex splits, and no semantic sectioning at all (e.g. everything in generic `<div>`s with inline styles) has no reliable structural signal to mine — fall back to Path C (ask, or describe what you can infer visually by reading the rendered layout structure from the markup order and text content alone) rather than inventing spans that aren't actually there.
