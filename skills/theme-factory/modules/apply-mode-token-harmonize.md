# Apply Mode Details

## Token Template

```css
/* Theme: <name> - applied by obs-theme-factory */
:root {
  --color-primary: <hex>;
  --color-primary-light: <hex>;
  --color-secondary: <hex>;
  --color-accent: <hex>;
  --color-bg: <hex>;
  --color-surface: <hex>;
  --color-surface-alt: <hex>;
  --color-text: <hex>;
  --color-text-muted: <hex>;
  --color-text-on-primary: <hex>;
  --color-border: <hex>;
  --color-success: <hex>;
  --color-warning: <hex>;
  --color-error: <hex>;

  --font-family: <v>;
  --font-family-mono: <v>;
  --font-family-display: <v>;
  --font-size-base: 16px;
  --font-weight-heading: <v>;
  --font-weight-body: <v>;
  --line-height: <v>;

  --radius: <v>;
  --radius-card: <v>;
  --radius-button: <v>;

  --shadow-sm: <v>;
  --shadow-md: <v>;
  --shadow-lg: <v>;
  --shadow-xl: <v>;
  --shadow-colored: <v>;
  --shadow-inset: <v>;

  --gradient-hero: <v>;
  --gradient-card: <v>;
  --gradient-button: <v>;
  --gradient-text: <v>;
  --gradient-accent: <v>;

  --glow-color: <hex>;
  --glow-sm: <v>;
  --glow-md: <v>;
  --glow-lg: <v>;
  --glass-blur: <Npx>;
  --glass-tint: <rgba>;
  --backdrop-filter: <v>;
  --text-shadow: <v>;
  --border-gradient: <v>;
  --noise-opacity: <0-1>;

  --bg-base: <hex>;
  --bg-image: <v>;
  --bg-size: <v>;
  --bg-position: <v>;
  --bg-repeat: <v>;

  --space-1: <v>;
  --space-2: <v>;
  --space-3: <v>;
  --space-4: <v>;
  --space-6: <v>;
  --space-8: <v>;
  --duration-fast: <v>;
  --duration-base: <v>;
  --duration-slow: <v>;
  --easing: <v>;
  --border-width: <v>;

  /* Remap file's shorthand vars → theme tokens (only include vars that exist in this file) */
  --bg: var(--color-bg);
  --card: var(--color-surface);
  --card2: var(--color-surface-alt);
  --border: var(--color-border);
  --accent: var(--color-primary);
  --text: var(--color-text);
  --muted: var(--color-text-muted);
  --green: var(--color-success);
  --red: var(--color-error);
  --yellow: var(--color-warning);
}
```

Common shorthand → token mappings:

| File var                            | Theme token                |
| ----------------------------------- | -------------------------- |
| `--bg`, `--background`, `--page-bg` | `var(--color-bg)`          |
| `--card`, `--surface`, `--panel`    | `var(--color-surface)`     |
| `--card2`, `--surface-alt`, `--alt` | `var(--color-surface-alt)` |
| `--border`, `--divider`             | `var(--color-border)`      |
| `--accent`, `--primary`, `--brand`  | `var(--color-primary)`     |
| `--text`, `--fg`                    | `var(--color-text)`        |
| `--muted`, `--subtle`, `--dim`      | `var(--color-text-muted)`  |
| `--radius`, `--rounded`             | `var(--radius-card)`       |

---

## Coexistence with layout-factory

A target file may already carry a `/* Layout: <name> - applied by obs-layout-factory */` marker with its own `--layout-*` token block, `data-layout`/`data-region` attributes, and `grid-template-areas`. Leave that block and those attributes untouched — every step above (4a-4k) only ever reads/writes `--color-*`, `--font-*`, `--radius-*`, `--shadow-*`, `--gradient-*`, `--glow-*`, `--glass-*`, `--bg-*`, and `--space-*`/`--duration-*` tokens, a disjoint namespace from `--layout-*`. If a future harmonize step needs to touch spacing or structural CSS properties (grid, position, region sizing), check for a `data-layout` attribute or `--layout-*` block first and skip those properties/selectors rather than overwriting them.

---

## Harmonize Steps

**4a. Color distribution** — if `primary` appears in >60% of colored elements, introduce `secondary`/`accent` as counterpoint.

| Element                        | Use                                                             |
| ------------------------------ | --------------------------------------------------------------- |
| Primary data / hero metric     | `primary`                                                       |
| Comparison / supporting series | `secondary` or `accent`                                         |
| Positive / gain                | `success`                                                       |
| Warning / at-risk              | `warning`                                                       |
| Negative / loss / error        | `error`                                                         |
| Chart grid lines               | `border` hex                                                    |
| Active tab/state               | `primary` full opacity                                          |
| Inactive/default               | `textMuted`                                                     |
| Badges/tags                    | Rotate `primaryLight`, `success`, `warning`, `error` by meaning |

**4b. Font** — if `font-family` on `body` is hardcoded, update to `var(--font-family)`.

**4c. Hardcoded text colors** — near-white (lightness > 70%) on light theme → `var(--color-text-muted)`. Near-black (< 15%) on dark theme → `var(--color-text)`. Use `replace_all: true`.

**4d. Colored sections** (hero, header, callout) — if section has dark gradient and new theme is light: replace with `linear-gradient(135deg, <primary> 0%, <darker-shade> 100%)`. Interior text → `var(--color-text-on-primary)`.

**4e. Semi-transparent overlays** — light theme: `rgba(0,0,0,X)` ok at ≤ 0.08. Dark theme: `rgba(255,255,255,X)` ok at low opacity. Flip direction if wrong for new mode.

**4f. JS/SVG hardcoded colors** _(mandatory on mode switch)_ — CSS vars can't reach `<script>`. Grep for:

```
stroke="#[0-9a-fA-F]{3,6}"   fill="#[0-9a-fA-F]{3,6}"
color:#[0-9a-fA-F]{3,6}      "#[0-9a-fA-F]{6}"
```

| Found type             | Replace with                          |
| ---------------------- | ------------------------------------- |
| Grid/axis lines        | `border` hex                          |
| Reference/guide lines  | `textMuted` hex                       |
| Primary data line      | `primary` or `accent` hex             |
| Status/scenario colors | theme `success`/`warning`/`error` hex |
| SVG text labels        | `textMuted` or `text` hex             |
| Fill on dark shape     | `#ffffff`; on light shape: `text` hex |

Use `replace_all: true`. Re-grep to confirm 0 old-theme hex values remain.

**4g. Opacity recalibration** — fill areas designed for dark bg are too faint on light:

- SVG fill area: `opacity 0.07` → `0.14`
- Result/verdict tint: `color+'0a'` → `color+'18'`
- Hover row: `rgba(accent, 0.04)` → `rgba(primary, 0.06-0.08)`

**4h. WCAG contrast** — verify all text-on-background pairings: ≥ 4.5:1 body text, ≥ 3:1 large text/UI components.

**4k. Background pattern** — if theme `background.type` is `pattern`/`noise`/`gradient`:

```css
body {
  background-color: var(--bg-base);
  background-image: var(--bg-image);
  background-size: var(--bg-size);
  background-position: var(--bg-position);
  background-repeat: var(--bg-repeat);
}
```

**4j. Gradients, glow, effects:**

- `--gradient-hero` → hero/header/navbar `background`
- `--gradient-button` → `.btn-primary` / CTA `background`
- `--gradient-text` → display headings with `background-clip: text`
- `--glow-md` → `box-shadow` on `.btn-primary` and key cards
- `--glass-blur` → panels: `background: var(--glass-tint); backdrop-filter: var(--backdrop-filter)`
- `--shadow-inset` → inputs, `textarea`, `select`, `.well`
- `--noise-opacity` (if > 0) → `body::after` fixed overlay

**4i. Design judgment** — if something looks obviously off but doesn't fit the above, fix it.

---

## Report Format

```
Applied theme <name> to <file>

Variables injected:  <N> CSS tokens in :root
Shorthand remapped:  <list of --var → token mappings added>
Font updated:        body font-family → var(--font-family)
Color repairs:       <N> hardcoded values replaced
Section fixes:       <selectors touched>
Gradient applied:    <e.g. hero → var(--gradient-hero)>
Effects applied:     <e.g. glow-md on .btn-primary>
JS/SVG audit:        <N> hex values replaced in <script> blocks
Opacity fixes:       <list>
Contrast verified:   All pairings >= 4.5:1 (>= 3:1 large text)

  aesthetic: <v>  ·  luminescence: <v>  ·  glass: <N>px  ·  density: <v>  ·  motion: <v>
```

Manual review needed: list anything unfixable — external stylesheets, canvas-drawn graphics, colors injected by third-party libraries.
