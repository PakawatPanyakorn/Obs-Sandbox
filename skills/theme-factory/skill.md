---
name: theme-factory
description: Manage visual theme presets to extract, browse, delete, and apply.
---

# Theme Factory

Personal theme library. Extract from screenshots/HTML/text, manage named presets with live previews, apply to HTML files.

## Storage

Presets: `~/.claude/skills/theme-factory/themes/<name>.html`  
Gallery: `~/.claude/skills/theme-factory/index.html`

Each preset is both a live browser preview and a JSON data store (`<script id="theme-data">`).

## Activation

This skill activates **only** when:

- User invokes the `/theme-factory` slash command, **or**
- User message contains the word **"theme"** paired with an action word (see table below)

A message containing "theme" alone (no action) is **not** a trigger — do not activate.

---

## Step 1: Detect Intent

| Mode        | Trigger (must include "theme" + one of these, or slash command)                                                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **extract** | `theme extract` · `theme capture` · `theme save` · `theme design` · `theme create` · `create theme` · `design theme` · `make theme` · `new theme` · screenshot/HTML path + "theme" |
| **list**    | `theme list` · `list themes` · `show themes` · `browse themes` · `what themes`                                                                                                     |
| **delete**  | `theme delete <name>` · `delete theme <name>` · `remove theme <name>`                                                                                                              |
| **apply**   | `theme apply <name>` · `apply theme <name>` · `use theme <name>` · `theme <name> on <file>`                                                                                        |

Ambiguous (has "theme" but action unclear) → ask: "Extract/create, list, delete, or apply a theme?"

---

## Extract Mode

### Multi-theme detection

Count distinct themes before extracting anything.

| Source | Multi-theme signals                                                                                                     |
| ------ | ----------------------------------------------------------------------------------------------------------------------- |
| Image  | Light+dark variants side-by-side; theme-switcher UI visible                                                             |
| HTML   | Multiple `:root` blocks (`[data-theme="..."]`, `.dark`, `@media prefers-color-scheme`); `--*-light`/`--*-dark` var sets |
| Text   | User lists multiple palettes ("a light and dark version", "three themes: ocean, forest, sunset")                        |

**Single theme** → proceed.  
**Multiple** → present numbered list, wait for selection. "all" = extract each in sequence, one preset file per theme.

---

### Source detection

| Source    | Signal                                     | Path   |
| --------- | ------------------------------------------ | ------ |
| Image     | `.png/.jpg/.jpeg/.webp/.gif`; "screenshot" | Path A |
| HTML file | `.html/.htm`; "from this HTML/page/file"   | Path B |
| Text      | No file path; describes theme in words     | Path C |

---

### Shared: 14 color slots (all paths)

| Slot            | Capture                                                         |
| --------------- | --------------------------------------------------------------- |
| `background`    | Dominant page/canvas color                                      |
| `surface`       | Card/panel (~3–5% lighter/darker than bg)                       |
| `surfaceAlt`    | Zebra rows, sidebar, modal (~8–10% shift from bg)               |
| `primary`       | Main brand/action — buttons, active nav, links                  |
| `primaryLight`  | Primary at ~25% opacity over white                              |
| `secondary`     | Supporting accent — pills, tags, secondary buttons              |
| `accent`        | Pop color — CTA highlights, progress bars                       |
| `text`          | Main body text                                                  |
| `textMuted`     | Captions, labels, placeholders                                  |
| `textOnPrimary` | Text ON primary (white or very dark based on primary luminance) |
| `border`        | Subtle separator / card outline                                 |
| `success`       | Status green                                                    |
| `warning`       | Status amber                                                    |
| `error`         | Status red                                                      |

Missing slots: derive from nearby slots using ratios above. Status colors: match saturation level of the found palette.

---

### Shared: Background analysis (all paths)

> **Scope:** Page canvas only — `body`, `html`, `.page`, `.layout`, `.wrapper`. Skip component-level patterns.

| Type        | Signals                       | Capture                                                                                                                          |
| ----------- | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| solid       | Uniform fill                  | `type: solid`, `baseColor: <hex>`, `image: none`                                                                                 |
| gradient    | Canvas shifts color           | `type: gradient`, full `linear-gradient(...)` as `image`                                                                         |
| lines-h     | Horizontal lines at intervals | `type: pattern`, `patternType: lines-h`; `repeating-linear-gradient(transparent calc(Npx - 1px), <color> Npx)`, `size: auto Npx` |
| dot-grid    | Regular grid of dots          | `type: pattern`, `patternType: dot-grid`; `radial-gradient(circle, <color> 1px, transparent 1px)`, `size: Npx Npx`               |
| grid        | Lines on both axes            | `type: pattern`, `patternType: grid`; `linear-gradient(...), linear-gradient(90deg, ...)`, `size: Npx Npx`                       |
| noise/paper | Fine grain over solid         | `type: noise`; `patternOpacity: <0–1>`                                                                                           |
| blueprint   | White/cyan lines on dark navy | `type: pattern`, `patternType: blueprint`                                                                                        |
| image       | Photographic fill             | `type: image`, `baseColor: dominant hex`                                                                                         |

Always write concrete CSS for `image`, `size`, `position`, `repeat` — never just a label.

---

### Shared: Effects (all paths)

Mine or infer concrete CSS values for each. Absent → `'none'` or `0`. Never omit.

| Effect          | Capture                                                                              |
| --------------- | ------------------------------------------------------------------------------------ |
| Hero gradient   | Full `linear-gradient(...)` for header/hero/navbar bg                                |
| Button gradient | Full gradient for CTA buttons                                                        |
| Card gradient   | Subtle gradient for card bg, or `none`                                               |
| Gradient text   | Gradient for `background-clip: text` on headlines                                    |
| Accent gradient | Decorative bars/dividers, or `none`                                                  |
| Glow            | `glowColor` hex + `glowBlur` px + sm/md/lg `box-shadow` values                       |
| Glass           | `glassBlur: Npx` + `glassTint: rgba(...)` + `backdropFilter: blur(Npx) saturate(N%)` |
| Gradient border | CSS gradient for `border-image`                                                      |
| Inset shadow    | Full `inset ...` box-shadow                                                          |
| Noise opacity   | `0–1` (0 if absent)                                                                  |
| Text shadow     | Full `text-shadow` for headings                                                      |
| Colored shadow  | Full tinted `box-shadow` on primary elements                                         |

---

### Shared: Design DNA (all paths)

| Dimension        | Values                                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| aesthetic        | minimal / corporate / editorial / playful / technical / brutalist / glassmorphism / neumorphic / material / flat |
| personality      | 2–4 adjective tags                                                                                               |
| density          | compact / comfortable / spacious                                                                                 |
| elevation        | flat / subtle / layered / dramatic                                                                               |
| borderStyle      | none / hairline / subtle / bold                                                                                  |
| motionFeel       | instant / subtle / expressive; estimate duration-fast/base/slow ms                                               |
| surfaceTexture   | flat / frosted / gradient / noise / none                                                                         |
| iconStyle        | outlined / filled / rounded / sharp / duotone                                                                    |
| hierarchyClarity | low / medium / high                                                                                              |
| spaceUnit        | nearest 4px or 8px multiple                                                                                      |
| notes            | Anything distinctive not captured above                                                                          |

---

### Path A: Image Extraction

1. **Read** the image (Read tool — Claude has vision)
2. **Multi-theme check** — if multiple, present list and wait
3. **Colors** — analyze visually for all 14 slots (shared color table)
4. **Typography** — serif/sans/mono feel; weight; density; choose a real matching font stack
5. **Shape** — map feel to px: sharp=0, subtle=4–6, rounded=8–16, very rounded=20+
6. **Background** — inspect canvas carefully before assuming solid (shared background table)
7. **Effects** — analyze visually (shared effects table)
8. **Design DNA** — assess overall language (shared DNA table)
9. **Context gap?** — if the image lacks sufficient detail for any dimension (typography unclear, background ambiguous, effects not visible, DNA hard to read), consult the **Path C signal table** (Tone/Style/Hue/Background/Typography/Shape/Mood signals) and use contextual clues from the image (color temperature, subject matter, overall mood) to resolve gaps the same way a text description would.
10. **Name** — ask "What would you like to name it?" (skip if auto mode or provided inline)
11. **Write** preset HTML (template below) → **update** `index.html` `THEMES` array (add new `{ filename, data }` object with the full theme JSON) → tell user preset path

---

### Path B: HTML Extraction

1. **Read** the file
2. **Multi-theme check** — look for multiple `:root` overrides, `[data-theme]`, `@media prefers-color-scheme`
3. **Mine colors in priority order:**

   | Priority | Source                                                        |
   | -------- | ------------------------------------------------------------- |
   | 1        | `:root { --color-* }` — use directly, resolve variable chains |
   | 2        | `body`, `header`, `.btn`, `.card` CSS rules                   |
   | 3        | Inline `style=""` on hero, navbar, CTA                        |
   | 4        | Tailwind/utility classes → map to hex                         |
   | 5        | External `<link>` — note existence, derive from inline clues  |

4. **Map** → 14 color slots; derive missing slots using shared ratios
5. **Background** — check `body`, `html`, `.page`, `.wrapper` background properties (shared table)
6. **Effects** — mine `box-shadow`, `backdrop-filter`, `background-clip`, gradients per selector (shared effects table)
7. **Typography** — `font-family`/`font-size`/`font-weight`/`line-height` on `body`/`:root`; mono from `code`/`pre`
8. **Shape** — `border-radius` from `:root`, `.card`, `.btn`
9. **Design DNA** — derive: density from padding/gap sizes; elevation from box-shadow frequency; motionFeel from transition durations (shared DNA table)
10. **Context gap?** — if the HTML source is sparse, missing font definitions, has no explicit effects, or DNA signals are absent, consult the **Path C signal table** (Tone/Style/Hue/Background/Typography/Shape/Mood signals) and infer the missing dimensions from the file's naming conventions, class names, content tone, and overall visual intent.
11. **Name** → **Write** preset → **update** index → tell user preset path

---

### Path C: Text Extraction

**Design quality mandate:** Create distinctive, production-grade themes. Avoid generic "AI slop" aesthetics — every decision must feel intentional and opinionated.

#### 0. Intent resolution

**With context** → derive tone, style, typography, color, background, and layout from the provided description.

**Without context** → freely invent a distinctive theme. Pick a combination that makes a strong, coherent statement:

- **Tone:** Dark · Light · Colorful · Colorless
- **Style:** formal · Super-Unrealistic · brutally minimal · maximalist · retro-futuristic · editorial · brutalist · art deco · soft/pastel · industrial · Psychedelic Surreal _(or any other strong aesthetic direction)_

Choose the pairing with the most creative tension — not the safest one.

---

1. **Multi-theme check** — if user implies multiple palettes, present list
2. **Parse description** for signals:

   | Signal     | Examples                                   | Maps to                       |
   | ---------- | ------------------------------------------ | ----------------------------- |
   | Tone       | dark, light, colorful, colorless           | Overall lightness/saturation  |
   | Style      | brutalist, art deco, editorial, surreal    | Aesthetic direction           |
   | Hue        | blue, teal, warm orange, purple            | `primary`, `accent`           |
   | Background | dark terminal, white paper, off-white      | `background`                  |
   | Typography | serif editorial, monospace code, geometric | font stacks                   |
   | Shape      | sharp, rounded, pill                       | `borderRadius`                |
   | Reference  | "like GitHub dark", "like Notion"          | Match known palette closely   |
   | Mood       | cyberpunk, minimal, corporate, warm        | Saturation, contrast, spacing |

3. **Synthesize** all 14 slots. Ensure: ≥ 4.5:1 text/bg contrast; `primaryLight` same hue as `primary`; status colors match palette saturation; dark themes bg < 20% lightness, light > 90%.

   **Color palette rules:**
   - Use dominant hues with sharp accents — avoid timid even distributions across the spectrum
   - Build cohesion around 1–2 anchor hues; accents should feel deliberately chosen, not random
   - **AVOID pure `#000000` and `#ffffff`** — use near-black / near-white with slight hue lean unless the theme's identity demands it (e.g., brutalist newspaper, high-contrast accessibility theme)

4. **Typography** — choose a distinctive display + refined body font pair. **Never use:** Inter, Roboto, Arial, system-ui, Helvetica, or Space Grotesk.

   | Style direction         | Display font                                 | Body font                               |
   | ----------------------- | -------------------------------------------- | --------------------------------------- |
   | Editorial / literary    | `'Playfair Display'`, `'Cormorant Garamond'` | `'Lora'`, `'Source Serif 4'`            |
   | Retro-futuristic        | `'Orbitron'`, `'Exo 2'`                      | `'Rajdhani'`, `'Oxanium'`               |
   | Art deco / formal       | `'Poiret One'`, `'Cinzel'`                   | `'Josefin Sans'`, `'Libre Baskerville'` |
   | Brutalist               | `'Bebas Neue'`, `'Anton'`                    | `'IBM Plex Mono'`, `'Courier Prime'`    |
   | Soft / pastel / playful | `'Nunito'`, `'Comfortaa'`                    | `'DM Serif Display'`, `'Quicksand'`     |
   | Industrial / technical  | `'Barlow Condensed'`, `'Syncopate'`          | `'IBM Plex Sans'`, `'Syne'`             |
   | Psychedelic / surreal   | `'Righteous'`, `'Boogaloo'`                  | `'Cabin'`, `'Varela Round'`             |
   | Terminal / code         | `'JetBrains Mono'`, `'Fira Code'`            | `'Inconsolata'`, `'Share Tech Mono'`    |

   All fonts must be loaded via Google Fonts `@import` in the HTML file.

5. **Shape** from feel: terminal=0–2px, brutalist=0px, corporate=4–6px, editorial=6–8px, SaaS=8–12px, art deco=2–4px, playful=16–24px
6. **Background** — prioritize depth over solid colors. Prefer gradient meshes, noise textures, geometric patterns, or layered transparencies.

   | Implies                             | Generate                                      |
   | ----------------------------------- | --------------------------------------------- |
   | paper / notebook / lined            | lines-h; warm off-white base; ~24px spacing   |
   | graph paper / grid                  | grid pattern; ~20px pitch                     |
   | dot grid / bullet journal           | dot-grid; 20–24px pitch                       |
   | blueprint / technical               | blueprint; dark navy + white/cyan lines       |
   | noise / grain / textured            | noise; `patternOpacity: 0.03–0.08`            |
   | gradient / mesh background          | gradient; full `linear-gradient(...)` or mesh |
   | dark / light / minimal (no texture) | solid; `image: none`                          |

7. **Effects** — infer from description:

   | Implies                             | Generate                                                                               |
   | ----------------------------------- | -------------------------------------------------------------------------------------- |
   | neon / glow / cyber / electric      | Full glow system: sm/md/lg `box-shadow` values                                         |
   | glass / frosted / blur              | `glassBlur: 12px`, `glassTint: rgba(...)`, `backdropFilter: blur(12px) saturate(180%)` |
   | gradient / gradient buttons         | `--gradient-hero`, `--gradient-button`, `--gradient-card` values                       |
   | neumorphic / soft shadow / embossed | Dual inset shadows                                                                     |
   | gradient border / rainbow border    | `linear-gradient` for `border-image`                                                   |
   | minimal / flat / clean / no shadow  | All effects `none`                                                                     |
   | (nothing implies it)                | `'none'` or `0` — never invent                                                         |

8. **Layout direction** — don't default to centered symmetric grids. Consider:
   - Asymmetric columns, diagonal dividers, overlapping elements
   - Grid-breaking hero sections, generous negative space or controlled density
   - Diagonal flow lines, staggered cards, off-center typography anchors

9. **Design DNA** from mood words (shared DNA table)

10. **Name** — choose a name that reflects the specific aesthetic (e.g. `midnight-telegraph`, `chrome-pastoral`, `acid-ledger`), not a generic descriptor.

11. **Output** — write as a standalone HTML file that showcases the full theme ability:
    - Use the preset-template as a structural base reference, but **design freely** to express the theme's full potential — layout, custom components, section transitions, anything needed to show what this theme can do
    - Include a visible tag block showing `tone` and `style` (e.g. `Dark · Retro-futuristic`)
    - The showcase content should fit the theme's world — a brutalist theme gets harsh editorial blocks; a psychedelic theme gets flowing surreal sections; art deco gets ornamental dividers
    - All tone / style / typography / color / background / layout decisions must feel cohesive — every component should reinforce the same singular aesthetic

12. **Write** preset → **update** index → tell user preset path

---

### HTML Preset Template

Read `~/.claude/skills/theme-factory/preset-template.html` to get the full template structure. Replace every `<placeholder>` with the actual extracted value. `<script id="theme-data">` must be valid JSON. Every CSS variable in `:root` must have a concrete value. The `<body>` must contain only the generic component showcase — no content from the extraction source.

The template opens with `<!DOCTYPE html><html lang="en" data-theme="<name>">` — read the file for the full structure.

For Path C themes: the template is a **base reference only** — deviate freely in layout, custom sections, and component design to express the theme's full potential. The JSON data block must still be valid and complete.

After writing preset, tell user to look at `~/.claude/skills/theme-factory/index.html` to see the live preview and confirm the theme looks correct.

---

## List Mode

Tell the user: "Open [Theme Gallery](https://html-preview.github.io/?url=https://github.com/PakawatPanyakorn/.claude/blob/master/skills/theme-factory/index.html)"

Do not read files, render swatches, or summarize themes.

---

## Delete Mode

1. Resolve path: `~/.claude/skills/theme-factory/themes/<name>.html`
2. Check exists (Glob). If not: "No theme named '\<name\>' found."
3. Read file → show swatch summary as confirmation
4. Ask: "Delete theme **\<name\>**? This cannot be undone. Reply 'yes' to confirm."
5. On confirm: `Remove-Item "~/.claude/skills/theme-factory/themes/<name>.html"`
6. Update `index.html`: remove the `{ filename: 'themes/<name>.html', data: ... }` entry from `THEMES` array, write back
7. Confirm: "Deleted theme **\<name\>**."

---

## Apply Mode

The theme is a **starting point**. Use its palette as design foundation, then make the whole file look cohesive and production-grade — designer reskin, not find-replace.

**Production-grade means:** WCAG AA contrast everywhere; no color invisible after mode switch; JS SVG colors audited; result looks intentionally designed for this theme with no visible seams.

### Step 1: Load theme

Read `~/.claude/skills/theme-factory/themes/<name>.html`. Parse JSON from `<script id="theme-data">`. Note `colors.background` lightness (dark vs light mode).

### Step 2: Audit target file

Identify before touching anything:

- **Color mode** — dark or light background?
- **Mode switch?** — theme dark + file light (or vice versa) = full color audit; steps 4f/4g/4h mandatory
- **File's shorthand vars** — e.g. `--bg`, `--card`, `--text`, `--accent` (need remapping in Step 3)
- **Hardcoded colors** — literal hex/rgba in `color:`, `background:`, `border-color:`, gradients
- **Colored sections** — hero, callout, header on own surface (need separate treatment)
- **JS hardcoded colors** — hex inside `<script>` tags (`stroke="#..."`, `fill="#..."`, template literals) — CSS vars cannot reach these

### Step 3: Inject :root block

Add `/* Theme: <name> — applied by theme-factory */` `:root {}` at top of `<style>` (or insert `<style>` as first child of `<head>`). Replace existing theme block if present. Use `Edit`, never rewrite the whole file.

```css
/* Theme: <name> — applied by theme-factory */
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
  --noise-opacity: <0–1>;

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

### Step 4: Harmonize

Fix what variable injection can't reach. Use theme palette as baseline color source.

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

**4c. Hardcoded text colors** — near-white (lightness > 70%) on light theme → `var(--color-text-muted)` or `var(--color-text)`. Near-black (< 15%) on dark theme → `var(--color-text)`. Use `replace_all: true`.

**4d. Colored sections** (hero, header, callout) — if section has dark gradient and new theme is light: replace with `linear-gradient(135deg, <primary> 0%, <darker-shade> 100%)`. Ensure interior text uses `var(--color-text-on-primary)` explicitly.

**4e. Semi-transparent overlays** — light theme: `rgba(0,0,0,X)` ok at ≤ 0.08, reduce if higher. Dark theme: `rgba(255,255,255,X)` ok at low opacity. Flip direction if wrong for new mode.

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
- Hover row: `rgba(accent, 0.04)` → `rgba(primary, 0.06–0.08)`

**4h. WCAG contrast** — verify all text-on-background pairings: ≥ 4.5:1 body text, ≥ 3:1 large text/UI components. Common failures on light cream (`#FCFBF4`):

| Old color                 | Ratio  | Replace with                |
| ------------------------- | ------ | --------------------------- |
| `#ffd166` bright yellow   | ~1.3:1 | theme `warning` darkened    |
| `#4fc3f7` cyan            | ~1.8:1 | theme `primary` or `accent` |
| `#52d68a` neon green      | ~2.4:1 | theme `success`             |
| `#ff7a7a` light coral     | ~2.8:1 | theme `error`               |
| `#9fb0c8` light blue-gray | ~2.1:1 | theme `textMuted`           |

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

If `type: solid`, skip. If file already has a pseudo-element pattern layer, update it instead of adding duplicate.

**4j. Gradients, glow, effects:**

- `--gradient-hero` (if not `none`) → hero/header/navbar `background`
- `--gradient-button` → `.btn-primary` / CTA `background`
- `--gradient-card` → card `background` (only if aesthetic fits; skip on flat-design files)
- `--gradient-text` → display headings: `background: var(--gradient-text); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text`
- `--glow-md` (if not `none`) → `box-shadow` on `.btn-primary` and key cards; `:hover` → `--glow-sm`; SVG lines: `filter: drop-shadow(0 0 4px <glowColor>)`
- `--glass-blur` (if > 0) → panels over bg: `background: var(--glass-tint); backdrop-filter: var(--backdrop-filter); -webkit-backdrop-filter: var(--backdrop-filter); border: 1px solid var(--color-border)`
- `--shadow-inset` → inputs, `textarea`, `select`, `.well`
- `--noise-opacity` (if > 0) → `body::after { content:''; position:fixed; inset:0; opacity:var(--noise-opacity); pointer-events:none; z-index:9999 }`

**4i. Design judgment** — if something looks obviously off but doesn't fit the above, fix it. Goal: page looks intentionally designed for this theme at production quality.

### Step 5: Strategy by file type

| Type           | Strategy                                                                                        |
| -------------- | ----------------------------------------------------------------------------------------------- |
| `.html`        | Prepend `:root {}` at top of existing `<style>`; or insert `<style>` as first child of `<head>` |
| `.css`         | Replace existing `:root { ... }` or prepend if none                                             |
| `.md` / `.txt` | Prepend `<style>\n<block>\n</style>` as very first line                                         |

Always use `Edit` for targeted changes — never rewrite the whole file.

### Step 6: Report

```
Applied theme <name> to <file>

Variables injected:  <N> CSS tokens in :root
Shorthand remapped:  <list of --var → token mappings added>
Font updated:        body font-family → var(--font-family)
Color repairs:       <N> hardcoded values replaced (e.g. "#c5c9d9 × 4 → var(--color-text-muted)")
Section fixes:       <selectors touched, e.g. ".hero — gradient updated">
Gradient applied:    <e.g. hero → var(--gradient-hero), .btn-primary → var(--gradient-button)>
Effects applied:     <e.g. glow-md on .btn-primary, glass-tint on .panel>
JS/SVG audit:        <N> hex values replaced in <script> blocks
Opacity fixes:       <list>
Contrast verified:   All pairings ≥ 4.5:1 (≥ 3:1 large text)

  aesthetic: <v>  ·  luminescence: <v>  ·  glass: <N>px  ·  density: <v>  ·  motion: <v>
```

⚠ **Manual review needed:** list anything unfixable — external stylesheets, canvas-drawn graphics, colors injected by third-party libraries.
