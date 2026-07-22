# Apply Mode: HTML/CSS Implementation

Only invoked from `modules/apply-mode-restructure.md` when the target is an actual HTML/CSS file, after the content-mapping judgment (§2 of that file) is already decided. This file covers the mechanical CSS/markup work only.

## Signature markers

Layout restructures markup, not just variable values — unlike theme-factory, one marker isn't enough to detect state cheaply. Use both:

- CSS comment above the structural `:root` block: `/* Layout: <name> - applied by obs-layout-factory */`
- `data-layout="<name>"` attribute on `<body>` (or `<main>` if the file has no wrapping body content to mark) — for fast, markup-side detection without parsing CSS.

**Detection**: grep the target for `applied by obs-layout-factory`. Found → **Path R**. Not found → **Path F**.

## Structural token block (grid/spacing only — never color, font, shadow-color, or gradient)

```css
/* Layout: <name> - applied by obs-layout-factory */
:root {
  --layout-columns: <N>;
  --layout-gutter: <value>;
  --layout-max-width: <value>;
  --layout-margin-inline: <value>;
  --layout-baseline: <value>;
  --layout-space-1: <v>; --layout-space-2: <v>; --layout-space-3: <v>;
  --layout-space-4: <v>; --layout-space-6: <v>; --layout-space-8: <v>;
}
```

Use `grid-template-areas` on the container where practical — named areas keep the region-to-CSS mapping legible and match `composition.regions` ids directly (e.g. `grid-template-areas: "masthead masthead" "lead rail" "river rail";`).

## Critical: coexistence with theme-factory

Before injecting anything, grep the target for `applied by obs-theme-factory`.

- **If present**: reuse its existing `--space-*`/`--radius-*` tokens for spacing/shape decisions instead of declaring a parallel `--layout-space-*` scale — one file should not carry two competing spacing systems. Do not edit, remove, or reorder anything inside the theme-factory `:root` block. Any new region (pull quote wrapper, callout, sidebar) introduced during restructuring must reference the existing `var(--color-*)`, `var(--font-*)` tokens, never hardcoded values, so the current theme continues to skin the new structure automatically.
- **If absent**: declare the `--layout-*` namespaced tokens above. The separate namespace guarantees zero collision if theme-factory is applied afterward.
- Recommended (not enforced) order when starting from bare content: apply layout-factory first (it changes markup/regions, which theme-factory never touches), then theme-factory to skin it. Applying theme-factory first is also safe given the rule above.

## Path R: re-layout (marker found)

1. Locate the existing `/* Layout: ... */` `:root` block and `data-layout` attribute.
2. **Same region set as the new archetype** → fast path: update `grid`/`spacing` token values and `regionSpans` in place via `Edit`. Update the signature comment and `data-layout` value to the new name. Never rewrite the whole file.
3. **Different region set required** → structural surgery: still via targeted `Edit` calls region-by-region, never a full-file rewrite — locate each affected region's markup and adjust individually.
4. Leave any theme-factory `:root` block completely untouched.

## Path F: first apply (marker absent)

1. Audit the target: existing sectioning (headings, images, lists, tables, blockquotes), and whether theme-factory is present (decides the token-namespace strategy above).
2. Use the region assignment already decided in `apply-mode-restructure.md` §2 — this file doesn't re-decide content mapping, only implements it.
3. Inject the structural token block + CSS Grid rules (`grid-template-areas` preferred over float/absolute-position hacks).
4. Add semantic region wrappers with `data-region="lead|river|rail|sidenote|footer|exhibit|masthead"` attributes matching the region ids used, for traceability and for Path R to find later.
5. Implement the selected editorial devices (from `apply-mode-restructure.md` §2 step 4) as real markup: `<blockquote>` for pull quotes, `<aside>` for sidebars/sidenotes, an `<ol>`/`<ul>` endnote list for footnotes.
6. Add signature comment + `data-layout` attribute.

## Verification before reporting

- Every `data-region` referenced in CSS `grid-template-areas` actually exists in the markup.
- No inline hardcoded color/font values were introduced while restructuring (that would violate the theme-factory boundary even in a bare file — leave those decisions to theme-factory or the file's existing style).
- Breakpoints in `grid.breakpoints` are implemented as real `@media` rules, not just documented in the preset.

Return control to `apply-mode-restructure.md` §5-6 for the anti-pattern audit and report — this file does not produce its own separate report.
