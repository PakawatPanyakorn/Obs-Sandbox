---
name: theme-factory
description: Manage visual theme presets — extract colors/typography from screenshots, browse with live HTML previews, delete presets, and apply any theme to HTML/reports/dashboards via CSS custom properties
tools: Read, Write, Edit, Bash, Glob
---

# Theme Factory

A personal theme library. Extract visual themes from screenshots, manage named presets with live HTML previews, and apply any preset to HTML files, reports, or dashboards.

## Storage Location

All presets live as self-contained HTML files:
```
~/.claude/skills/theme-factory/themes/<name>.html
```

Each file is both:
- **A live preview** — open in any browser to see colors, typography, and components rendered
- **A data store** — the `<script id="theme-data">` block holds structured JSON for programmatic use

---

## Step 1: Detect Intent

Read the user's message and match one of four modes:

| Mode | Trigger phrases |
|------|----------------|
| **extract** | "extract theme from", "capture theme", "save theme from", screenshot/image path provided, HTML file path provided, text/description provided |
| **list** | "list themes", "show themes", "browse themes", "what themes", "my themes" |
| **delete** | "delete theme", "remove theme", followed by a theme name |
| **apply** | "apply theme", "use theme", "apply X to Y", followed by a theme name and a file |

If the intent is ambiguous, ask: "Did you want to extract a theme from a screenshot, an HTML file, a text description, list saved themes, delete a theme, or apply a theme to a file?"

---

## Mode: Extract — Capture Theme from Screenshot, HTML, or Text

### Source detection

Determine the input source before proceeding:

| Source | Signals | Path |
|--------|---------|------|
| **Image** | Path ends in `.png`, `.jpg`, `.jpeg`, `.webp`, `.gif`; or user says "screenshot" | → Image extraction |
| **HTML file** | Path ends in `.html`, `.htm`; or user says "from this HTML / page / file" | → HTML extraction |
| **Text description** | No file path; user describes a theme in words (e.g. "dark blue terminal", "warm editorial", "inspired by X") | → Text extraction |

---

### Multi-theme detection (check this before extracting on every path)

After reading the source, count how many distinct themes are present **before** building any palette.

**Signals that multiple themes exist:**

| Source | Multi-theme indicators |
|--------|----------------------|
| Image | Clearly separated light and dark variants side-by-side; a theme-switcher UI visible; multiple distinct branded sections with different color bases |
| HTML | More than one `:root` block (e.g. `[data-theme="dark"]`, `.dark`, `@media (prefers-color-scheme: dark)`); multiple named `--*-light` / `--*-dark` variable sets; a theme toggle element |
| Text | User lists multiple concepts ("a dark and a light version", "three palettes: ocean, forest, sunset") |

**If exactly one theme is detected:** proceed directly to the extraction steps for that path.

**If multiple themes are detected:** pause and present a numbered list:

```
I found N themes in this source:
  1. <label> — <one-line description, e.g. "light mode, blue primary">
  2. <label> — <one-line description>
  ...

Which would you like to save?  Reply with a number, a range (1-3), or "all".
```

- User replies with a number → extract that theme only, then proceed normally.
- User replies with a range or "all" → extract each theme in sequence, asking for a name per theme (or auto-naming as `<source-name>-light`, `<source-name>-dark`, etc. in auto mode), writing one preset file per theme, then show a combined swatch summary at the end.

---

### Path A: Image Extraction

**When to use:** User provides a path to an image (PNG, JPG, WEBP) or says "extract/capture/save theme from <image>".

**Steps**

**1. Read the image**
Use the `Read` tool on the provided image path. Claude has vision and will see the image.

**2. Multi-theme check**
Apply the multi-theme detection rules above. If multiple themes are visible (e.g. light + dark side by side, theme switcher UI), present the numbered list and wait for the user's selection before continuing.

**3. Analyze visually across these dimensions** _(for the selected theme(s))_

| Dimension | What to look for |
|-----------|-----------------|
| **background** | The dominant page/canvas color (behind content) |
| **surface** | Card, panel, or container color (often slightly lighter/darker than background) |
| **surfaceAlt** | Secondary surface — zebra rows, sidebar, modal overlay |
| **primary** | Main brand/action color — buttons, active nav, links |
| **primaryLight** | Lighter tint of primary — hover states, chips, badges |
| **secondary** | Supporting accent — pills, tags, secondary buttons |
| **accent** | Pop color — call-to-action highlights, progress bars, icons |
| **text** | Main body text color |
| **textMuted** | Secondary/subdued text — captions, labels, placeholders |
| **textOnPrimary** | Text that sits ON the primary color (usually white or very dark) |
| **border** | Subtle separator or card-outline color |
| **success / warning / error** | Status colors if visible; estimate if not (use conventional green/amber/red in the screenshot's saturation level) |

**4. Analyze typography style**
- Serif, sans-serif, or monospace feel?
- Weight: light/regular/medium/bold?
- Density: compact or spacious?
- Choose a matching system font stack or Google Font that fits the feel. Don't invent made-up font names.

**5. Analyze shape style**
- Fully sharp (0px), subtle (4–6px), rounded (8–16px), very rounded (20px+), or pill?
- Map to a `borderRadius` value.

**6. Analyze design DNA**

Assess the overall look, feel, and design language across these dimensions:

| Dimension | What to observe | Values |
|-----------|----------------|--------|
| **Aesthetic** | Overall visual paradigm | minimal, corporate, editorial, playful, technical, brutalist, glassmorphism, neumorphic, material, flat |
| **Personality tags** | 2–4 adjectives that capture the vibe | e.g. "warm, approachable, structured" / "cold, precise, dense" |
| **Density** | Whitespace and breathing room | compact / comfortable / spacious |
| **Elevation** | Use of shadow and depth layers | flat / subtle / layered / dramatic |
| **Border style** | Presence and weight of borders | none / hairline / subtle / bold |
| **Motion feel** | Implied animation speed and energy | instant / subtle / expressive — estimate `duration-fast/base/slow` |
| **Surface texture** | Background and card surface treatment | flat / frosted / gradient / noise / none |
| **Icon style** | Style of any visible icons or UI controls | outlined / filled / rounded / sharp / duotone |
| **Hierarchy clarity** | How clearly primary vs secondary content is distinguished | low / medium / high |
| **Spacing unit** | Base grid increment visible in padding/gaps | estimate nearest 4px or 8px multiple |
| **Notes** | Anything distinctive not captured above — e.g. "uses dividers instead of cards", "strong use of ALL CAPS labels", "asymmetric layouts" | free text |

**7. Ask for name and description** (once per theme being saved)
Say: "I've extracted the theme. What would you like to name it? (Add a short description too, or I'll generate one.)"

If the user is in auto mode or provides a name inline, skip the question and auto-generate.

**8. Write the HTML preset file** — see template below. Repeat for each theme being saved.

**8b. Update cache** — read `themes-cache.json` (or start with `{"themes":[]}` if missing), append the new theme's summary entry, write cache back.

**9. Report back** — show the inline swatch summary and file path for each saved theme.

---

### Path B: HTML Extraction

**When to use:** User provides a path to an `.html` / `.htm` file, or pastes raw HTML.

**Steps**

**1. Read the file**
Use the `Read` tool on the provided file path, or accept the pasted HTML directly.

**2. Multi-theme check**
Apply the multi-theme detection rules above. Look specifically for multiple `:root` overrides (`[data-theme="..."]`, `.dark`, `@media (prefers-color-scheme: dark)`), named variable sets, or a theme toggle. If found, present the numbered list and wait for the user's selection.

**3. Mine colors from the HTML/CSS in priority order** _(for the selected theme(s))_

| Priority | Source | What to look for |
|----------|--------|-----------------|
| 1 | Existing `:root { --color-* }` block | Read every `--color-*` variable directly |
| 2 | `<style>` inline rules | `background`, `color`, `border-color`, `fill` on `body`, header, `.btn`, `.card`, etc. |
| 3 | `style="..."` attributes | Inline styles on prominent elements (hero, navbar, CTA button) |
| 4 | Tailwind / utility classes | Map classes like `bg-blue-600`, `text-gray-800` to their hex equivalents |
| 5 | `<link>` to external stylesheet | Note that it exists; derive best-effort values from inline clues if the file is unavailable |

Resolve CSS variables recursively (if `--color-primary` references `--brand-blue`, follow the chain).

**3. Map extracted values to theme slots**
Assign extracted colors to: `background`, `surface`, `surfaceAlt`, `primary`, `primaryLight`, `secondary`, `accent`, `text`, `textMuted`, `textOnPrimary`, `border`, `success`, `warning`, `error`.

For any slot not explicitly found, derive it:
- `surface` ≈ background lightened/darkened 3–5%
- `surfaceAlt` ≈ background lightened/darkened 8–10%
- `primaryLight` ≈ primary at 25% opacity over white
- `textOnPrimary` — check contrast; use `#ffffff` or `#1a1a1a` based on primary luminance
- Status colors — estimate from saturation of found colors

**5. Extract typography**
- Look for `font-family` on `body` or `:root`
- Look for `font-size`, `font-weight`, `line-height` on `body` or common elements
- Detect monospace font from `code`, `pre`, `kbd` elements
- Fall back to system font stacks if none found

**6. Extract shape**
- Read `border-radius` from `:root`, `.card`, `.btn`, or the most common card/button selector
- Map to `radius`, `radius-card`, `radius-button`

**7. Extract design DNA from the HTML/CSS**

| Dimension | Where to look in HTML/CSS |
|-----------|--------------------------|
| **Density** | `padding` and `gap` values on cards/rows/containers — small (<12px) = compact, large (>24px) = spacious |
| **Elevation** | `box-shadow` frequency and intensity across components |
| **Border style** | `border-width` and `border` property prevalence; `0` or `none` = flat, `1px` = hairline, `2px+` = bold |
| **Motion feel** | `transition` and `animation` durations — `<100ms` instant, `150–250ms` subtle, `300ms+` expressive |
| **Surface texture** | `backdrop-filter`, `background: linear-gradient`, or `background-image` on surface elements |
| **Spacing unit** | GCD of common margin/padding values — typically 4px or 8px |
| **Icon style** | Class names (`icon-outline`, `fa-`, `bi-`, `heroicons`, etc.) or SVG `stroke-width` / `fill` attributes |
| **Aesthetic** | Synthesize from all of the above into one of: minimal, corporate, editorial, playful, technical, brutalist, glassmorphism, neumorphic, material, flat |
| **Personality tags** | 2–4 adjectives from overall impression |
| **Notes** | Patterns worth calling out — e.g. "heavy use of ALL CAPS labels", "no card borders, only shadows", "strong grid" |

**8. Ask for name and description** (once per theme being saved)
Say: "I've extracted the theme from `<filename>`. What would you like to name it? (Add a short description too, or I'll generate one.)"

If the user is in auto mode or provides a name inline, skip the question and auto-generate.

**9. Write the HTML preset file** — see template below. Set `"source": "html"` and `"sourceFile": "<path>"`. Repeat for each theme being saved.

**9b. Update cache** — read `themes-cache.json` (or start with `{"themes":[]}` if missing), append the new theme's summary entry, write cache back.

**10. Report back** — show the inline swatch summary and file path for each saved theme.

---

### Path C: Text Extraction

**When to use:** User describes a theme in words — no file path provided. Examples: "dark blue cyberpunk terminal", "warm cozy editorial with serif fonts", "inspired by the GitHub dark theme", "minimal light theme with teal accents".

**Steps**

**1. Multi-theme check**
Read the full description first. If the user implies multiple palettes ("a light and a dark version", "three themes: ocean, forest, sunset", "both a warm and a cool variant"), apply the multi-theme detection rules above — present the numbered list and wait for the user's selection before generating anything.

**2. Parse the description for intent signals** _(for the selected theme(s))_

| Signal category | Examples | Maps to |
|----------------|----------|---------|
| Tone | dark, light, high-contrast, muted, vibrant, pastel | Overall lightness / saturation level |
| Dominant hue | blue, teal, warm orange, forest green, purple | `primary`, `accent` |
| Background style | dark terminal, white paper, off-white, black | `background` |
| Typography feel | serif editorial, monospace code, clean sans, geometric | `fontFamily`, `fontFamilyDisplay` |
| Shape feel | sharp, rounded, pill, card-heavy | `borderRadius` |
| Reference | "like GitHub dark", "like Tailwind docs", "like VS Code" | Match well-known palette |
| Mood | cyberpunk, minimal, corporate, playful, warm | Informs saturation, weight, spacing |

**3. Synthesize a complete color palette**
Derive all 14 color slots from the description. Ensure:
- Good contrast between `text` and `background` (≥ 4.5:1 for WCAG AA)
- `primary` and `primaryLight` are clearly related (same hue, different lightness)
- Status colors match the overall saturation level of the palette
- Dark themes: background < 20% lightness; light themes: background > 90% lightness

**4. Choose typography**
Select real, available font stacks that match the described feel:
- Editorial/literary → `Georgia, 'Times New Roman', serif`
- Clean modern → `Inter, system-ui, sans-serif`
- Code/terminal → `'JetBrains Mono', 'Fira Code', monospace`
- Geometric → `'DM Sans', Helvetica, sans-serif`

**5. Choose shape**
- Terminal/code → 0–4px
- Corporate/clean → 6–8px
- Modern SaaS → 8–12px
- Playful/friendly → 16–24px

**6. Infer design DNA from the description**

Map descriptive language to design attributes:

| If the description says… | Infer… |
|--------------------------|--------|
| "minimal", "clean", "whitespace" | aesthetic: minimal; density: spacious; elevation: flat; border: hairline or none |
| "corporate", "enterprise", "professional" | aesthetic: corporate; density: comfortable; hierarchy: high; border: subtle |
| "editorial", "magazine", "blog" | aesthetic: editorial; density: spacious; typography-heavy; surface: flat |
| "playful", "fun", "colorful", "friendly" | aesthetic: playful; density: comfortable; motion: expressive; radius: large |
| "hacker", "terminal", "code", "dev tool" | aesthetic: technical; density: compact; mono fonts; instant motion; border: hairline |
| "glass", "blur", "frosted" | aesthetic: glassmorphism; surface: frosted; elevation: layered |
| "card-heavy", "dashboard", "data" | elevation: layered; density: compact; hierarchy: high; border: subtle |
| "brutal", "stark", "raw" | aesthetic: brutalist; border: bold; radius: 0; flat surfaces |
| "warm", "cozy", "inviting" | personality: warm; saturation up; motion: subtle |
| "like [known product]" | Match that product's known design language holistically |

Estimate spacing unit (4px or 8px grid), transition durations, and border width to match the implied density and motion feel.

**7. Ask for name and description** (once per theme being saved)
Say: "I've generated a theme from your description. What would you like to name it? (Add a short description too, or I'll generate one.)"

If the user is in auto mode or provides a name inline, skip the question and auto-generate.

**8. Write the HTML preset file** — see template below. Set `"source": "text"` and `"sourceFile": ""`. Repeat for each theme being saved.

**8b. Update cache** — read `themes-cache.json` (or start fresh if missing), append the new theme's summary entry and filename, sort `files`, write cache back.

**9. Report back** — show the inline swatch summary and file path for each saved theme.

---

---

### HTML Preset Template

```html
<!DOCTYPE html>
<html lang="en" data-theme="<name>">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Theme: <name></title>

  <!-- THEME DATA — parsed by theme-factory skill -->
  <script id="theme-data" type="application/json">
  {
    "name": "<name>",
    "description": "<description>",
    "createdAt": "<ISO timestamp>",
    "source": "<screenshot | html | text>",
    "sourceFile": "<original path, or empty string for text>",
    "colors": {
      "primary": "<hex>",
      "primaryLight": "<hex>",
      "secondary": "<hex>",
      "accent": "<hex>",
      "background": "<hex>",
      "surface": "<hex>",
      "surfaceAlt": "<hex>",
      "text": "<hex>",
      "textMuted": "<hex>",
      "textOnPrimary": "<hex>",
      "border": "<hex>",
      "success": "<hex>",
      "warning": "<hex>",
      "error": "<hex>"
    },
    "typography": {
      "fontFamily": "<stack>",
      "fontFamilyMono": "<mono stack>",
      "fontFamilyDisplay": "<display stack>",
      "scaleBase": "16px",
      "headingWeight": "<700 or extracted>",
      "bodyWeight": "<400 or extracted>",
      "lineHeight": "<1.5 or extracted>"
    },
    "spacing": {
      "borderRadius": "<Npx>",
      "cardRadius": "<Npx>",
      "buttonRadius": "<Npx>",
      "spaceUnit": "<Npx — base spacing unit, e.g. 8px>",
      "density": "<compact | comfortable | spacious>"
    },
    "shadows": {
      "sm": "<value>",
      "md": "<value>",
      "lg": "<value>",
      "elevation": "<flat | subtle | layered | dramatic>"
    },
    "motion": {
      "durationFast": "<ms>",
      "durationBase": "<ms>",
      "durationSlow": "<ms>",
      "easing": "<CSS easing value>",
      "feel": "<instant | subtle | expressive>"
    },
    "design": {
      "aesthetic": "<one of: minimal, corporate, editorial, playful, technical, brutalist, glassmorphism, neumorphic, material, flat>",
      "personality": ["<tag>", "<tag>"],
      "borderStyle": "<none | hairline | subtle | bold>",
      "iconStyle": "<outlined | filled | rounded | sharp | duotone | unknown>",
      "imageStyle": "<photographic | illustrative | abstract | none | unknown>",
      "surfaceTexture": "<flat | frosted | gradient | noise | none>",
      "hierarchyClarity": "<low | medium | high>",
      "notes": "<free-text: anything notable about the design language not captured above>"
    }
  }
  </script>

  <style>
    /* ── CSS VARIABLES ── copy this :root block into any HTML to apply the theme */
    :root {
      --color-primary:         <hex>;
      --color-primary-light:   <hex>;
      --color-secondary:       <hex>;
      --color-accent:          <hex>;
      --color-bg:              <hex>;
      --color-surface:         <hex>;
      --color-surface-alt:     <hex>;
      --color-text:            <hex>;
      --color-text-muted:      <hex>;
      --color-text-on-primary: <hex>;
      --color-border:          <hex>;
      --color-success:         <hex>;
      --color-warning:         <hex>;
      --color-error:           <hex>;

      --font-family:         <stack>;
      --font-family-mono:    <mono stack>;
      --font-family-display: <display stack>;
      --font-size-base:      16px;
      --font-weight-heading: <700>;
      --font-weight-body:    <400>;
      --line-height:         <1.6>;

      --radius:        <Npx>;
      --radius-card:   <Npx>;
      --radius-button: <Npx>;

      --shadow-sm: <value>;
      --shadow-md: <value>;
      --shadow-lg: <value>;

      /* Spacing */
      --space-1: <Npx>;
      --space-2: <Npx>;
      --space-3: <Npx>;
      --space-4: <Npx>;
      --space-6: <Npx>;
      --space-8: <Npx>;

      /* Motion */
      --duration-fast: <ms>;
      --duration-base: <ms>;
      --duration-slow: <ms>;
      --easing:        <CSS easing value>;

      /* Border */
      --border-width: <px>;
    }

    /* ── PREVIEW PAGE STYLES ── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: var(--color-bg);
      color: var(--color-text);
      font-family: var(--font-family);
      font-size: var(--font-size-base);
      line-height: var(--line-height);
      padding: 2rem;
      max-width: 900px;
      margin: 0 auto;
    }

    /* Header */
    .tf-header {
      background: var(--color-primary);
      color: var(--color-text-on-primary);
      border-radius: var(--radius-card);
      padding: 2rem;
      margin-bottom: 2rem;
      box-shadow: var(--shadow-md);
    }
    .tf-header h1 {
      font-family: var(--font-family-display);
      font-size: 2rem;
      font-weight: var(--font-weight-heading);
      margin-bottom: 0.25rem;
    }
    .tf-header p { opacity: 0.85; font-size: 0.9rem; }

    /* Section */
    .tf-section { margin-bottom: 2rem; }
    .tf-section-title {
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--color-text-muted);
      margin-bottom: 0.75rem;
      padding-bottom: 0.5rem;
      border-bottom: 1px solid var(--color-border);
    }

    /* Color swatches */
    .tf-swatches {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
      gap: 0.75rem;
    }
    .tf-swatch {
      border-radius: var(--radius);
      overflow: hidden;
      border: 1px solid var(--color-border);
      box-shadow: var(--shadow-sm);
    }
    .tf-swatch-color {
      height: 64px;
      width: 100%;
    }
    .tf-swatch-label {
      background: var(--color-surface);
      padding: 0.4rem 0.5rem;
      font-size: 0.7rem;
      font-family: var(--font-family-mono);
      color: var(--color-text-muted);
    }
    .tf-swatch-label strong {
      display: block;
      color: var(--color-text);
      font-size: 0.75rem;
      margin-bottom: 0.1rem;
    }

    /* Typography */
    .tf-type-scale { display: flex; flex-direction: column; gap: 0.5rem; }
    .tf-type-scale .t-h1 { font-size: 2.5rem; font-weight: var(--font-weight-heading); font-family: var(--font-family-display); }
    .tf-type-scale .t-h2 { font-size: 1.75rem; font-weight: var(--font-weight-heading); }
    .tf-type-scale .t-h3 { font-size: 1.25rem; font-weight: var(--font-weight-heading); }
    .tf-type-scale .t-body { font-size: 1rem; }
    .tf-type-scale .t-small { font-size: 0.85rem; color: var(--color-text-muted); }
    .tf-type-scale .t-mono { font-family: var(--font-family-mono); font-size: 0.9rem; background: var(--color-surface-alt); padding: 0.25rem 0.5rem; border-radius: var(--radius); }

    /* Buttons */
    .tf-buttons { display: flex; flex-wrap: wrap; gap: 0.75rem; align-items: center; }
    .tf-btn {
      padding: 0.5rem 1.25rem;
      border-radius: var(--radius-button);
      font-family: var(--font-family);
      font-size: 0.9rem;
      font-weight: 500;
      cursor: pointer;
      border: none;
      transition: opacity 0.15s;
    }
    .tf-btn:hover { opacity: 0.85; }
    .tf-btn-primary { background: var(--color-primary); color: var(--color-text-on-primary); box-shadow: var(--shadow-sm); }
    .tf-btn-secondary { background: var(--color-secondary); color: var(--color-text-on-primary); box-shadow: var(--shadow-sm); }
    .tf-btn-outline { background: transparent; color: var(--color-primary); border: 1.5px solid var(--color-primary); }
    .tf-btn-ghost { background: var(--color-surface-alt); color: var(--color-text); }

    /* Card */
    .tf-card {
      background: var(--color-surface);
      border: 1px solid var(--color-border);
      border-radius: var(--radius-card);
      padding: 1.5rem;
      box-shadow: var(--shadow-md);
    }
    .tf-card h3 { font-weight: var(--font-weight-heading); margin-bottom: 0.5rem; color: var(--color-primary); }
    .tf-card p { color: var(--color-text-muted); font-size: 0.9rem; line-height: var(--line-height); }
    .tf-cards { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 1rem; }

    /* Form */
    .tf-form { display: flex; flex-direction: column; gap: 1rem; max-width: 400px; }
    .tf-form label { font-size: 0.85rem; font-weight: 500; color: var(--color-text-muted); margin-bottom: 0.25rem; display: block; }
    .tf-form input, .tf-form select {
      width: 100%;
      padding: 0.5rem 0.75rem;
      border: 1.5px solid var(--color-border);
      border-radius: var(--radius);
      background: var(--color-surface);
      color: var(--color-text);
      font-family: var(--font-family);
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.15s;
    }
    .tf-form input:focus, .tf-form select:focus { border-color: var(--color-primary); }

    /* Badges */
    .tf-badges { display: flex; flex-wrap: wrap; gap: 0.5rem; }
    .tf-badge {
      padding: 0.2rem 0.75rem;
      border-radius: 999px;
      font-size: 0.75rem;
      font-weight: 600;
    }
    .tf-badge-primary { background: var(--color-primary-light); color: var(--color-primary); }
    .tf-badge-success { background: var(--color-success); color: #fff; }
    .tf-badge-warning { background: var(--color-warning); color: #fff; }
    .tf-badge-error { background: var(--color-error); color: #fff; }
    .tf-badge-neutral { background: var(--color-surface-alt); color: var(--color-text-muted); border: 1px solid var(--color-border); }

  </style>
</head>
<body>

  <!-- HEADER -->
  <div class="tf-header">
    <h1>Theme Preview</h1>
    <p>Colors · Typography · Components</p>
  </div>

  <!-- COLOR PALETTE -->
  <div class="tf-section">
    <div class="tf-section-title">Color Palette</div>
    <div class="tf-swatches">
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-primary)"></div>
        <div class="tf-swatch-label"><strong>primary</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-primary-light)"></div>
        <div class="tf-swatch-label"><strong>primaryLight</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-secondary)"></div>
        <div class="tf-swatch-label"><strong>secondary</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-accent)"></div>
        <div class="tf-swatch-label"><strong>accent</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-bg)"></div>
        <div class="tf-swatch-label"><strong>background</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-surface)"></div>
        <div class="tf-swatch-label"><strong>surface</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-surface-alt)"></div>
        <div class="tf-swatch-label"><strong>surfaceAlt</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-text)"></div>
        <div class="tf-swatch-label"><strong>text</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-text-muted)"></div>
        <div class="tf-swatch-label"><strong>textMuted</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-border)"></div>
        <div class="tf-swatch-label"><strong>border</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-success)"></div>
        <div class="tf-swatch-label"><strong>success</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-warning)"></div>
        <div class="tf-swatch-label"><strong>warning</strong><hex></div>
      </div>
      <div class="tf-swatch">
        <div class="tf-swatch-color" style="background:var(--color-error)"></div>
        <div class="tf-swatch-label"><strong>error</strong><hex></div>
      </div>
    </div>
  </div>

  <!-- TYPOGRAPHY -->
  <div class="tf-section">
    <div class="tf-section-title">Typography</div>
    <div class="tf-type-scale">
      <div class="t-h1">Display Heading</div>
      <div class="t-h2">Section Heading</div>
      <div class="t-h3">Subsection Heading</div>
      <div class="t-body">Body text — the quick brown fox jumps over the lazy dog. Used for paragraphs, descriptions, and general readable content at base size.</div>
      <div class="t-small">Small / muted — captions, labels, timestamps, helper text</div>
      <div class="t-mono">monospace: code(), variables, keys</div>
    </div>
  </div>

  <!-- BUTTONS -->
  <div class="tf-section">
    <div class="tf-section-title">Buttons</div>
    <div class="tf-buttons">
      <button class="tf-btn tf-btn-primary">Primary Action</button>
      <button class="tf-btn tf-btn-secondary">Secondary</button>
      <button class="tf-btn tf-btn-outline">Outlined</button>
      <button class="tf-btn tf-btn-ghost">Ghost</button>
    </div>
  </div>

  <!-- CARDS -->
  <div class="tf-section">
    <div class="tf-section-title">Cards</div>
    <div class="tf-cards">
      <div class="tf-card">
        <h3>Card Title</h3>
        <p>A standard card component with surface background, border, border-radius, and shadow from theme variables.</p>
      </div>
      <div class="tf-card">
        <h3>Data Card</h3>
        <p>Cards adapt naturally to the theme because every visual property references a CSS variable — swap themes by swapping :root.</p>
      </div>
      <div class="tf-card" style="background:var(--color-surface-alt)">
        <h3>Alt Surface</h3>
        <p>Using surfaceAlt — useful for sidebar panels, alternate rows, or secondary containers.</p>
      </div>
    </div>
  </div>

  <!-- FORM -->
  <div class="tf-section">
    <div class="tf-section-title">Form Elements</div>
    <div class="tf-form">
      <div>
        <label>Text Input</label>
        <input type="text" placeholder="Enter value…">
      </div>
      <div>
        <label>Select</label>
        <select>
          <option>Option A</option>
          <option>Option B</option>
          <option>Option C</option>
        </select>
      </div>
    </div>
  </div>

  <!-- BADGES -->
  <div class="tf-section">
    <div class="tf-section-title">Badges & Status</div>
    <div class="tf-badges">
      <span class="tf-badge tf-badge-primary">Primary</span>
      <span class="tf-badge tf-badge-success">Success</span>
      <span class="tf-badge tf-badge-warning">Warning</span>
      <span class="tf-badge tf-badge-error">Error</span>
      <span class="tf-badge tf-badge-neutral">Neutral</span>
    </div>
  </div>


</body>
</html>
```

> **Important when writing the HTML file:** Replace every `<placeholder>` with the actual extracted value. The `<script id="theme-data">` block must contain valid JSON. Every CSS variable in `:root` must have a concrete hex value. The swatch tiles in the body use `style="background:var(--color-...)"` — they render automatically once the variables are set. The rendered `<body>` must contain **only** the generic component showcase above — no text, labels, headings, or content from the extraction source.

---

### Inline Swatch Summary (show in chat after saving)

**IMPORTANT: VSCode's chat pane does NOT render inline HTML.** Do NOT use `<span>` tags — they appear as raw text. Use this emoji-circle format instead, which works in all chat environments.

**Color-to-emoji mapping rules** — pick the closest emoji for each hex:

| Hue / Tone | Emoji | Examples |
|------------|-------|---------|
| Red / coral / crimson | 🔴 | `#ff0000`, `#fe4450`, `#c94040` |
| Orange / amber / peach | 🟠 | `#e07838`, `#ef8354`, `#f5a870` |
| Yellow / gold / lime-yellow | 🟡 | `#ffe66d`, `#f7c050`, `#ccdd00` |
| Green / teal / mint | 🟢 | `#00ff41`, `#72f1b8`, `#5ab885`, `#00ff88` |
| Cyan / aqua | 🔵 | `#00e5ff`, `#36f9f6`, `#00ccff` — use 🔵 for bright cyan |
| Blue / indigo | 🔵 | `#5599ff`, `#4f5d75`, `#1a3e7f` |
| Purple / violet / pink-purple | 🟣 | `#ff7edb`, `#b078b8`, `#848bbd`, `#9aa8c8` |
| Near-black / very dark | ⚫ | lightness < 15%: `#07070F`, `#000900`, `#1a0f2e` |
| Dark grey / dark navy | 🩶 | lightness 15–35%: `#262335`, `#2d2145`, `#2a1828` |
| Mid grey / slate | 🩶 | lightness 35–60%: `#7a8299`, `#8080a8` |
| Light grey / silver | ⚪ | lightness 60–85%: `#d0d8e4`, `#bfc0c0`, `#c8c0b0` |
| Near-white / cream / off-white | ⚪ | lightness > 85%: `#ffffff`, `#fef4ee`, `#f6f1e8` |
| Brown / tan / warm dark | 🟤 | warm dark with brown hue |
| Pink (hot/neon) | 🩷 | `#ff7edb` — prefer 🩷 over 🟣 for saturated pinks |
| Light blue / sky | 🩵 | pale cyan or periwinkle |
| Dark navy / near-black blue | ⚫ | `#1a1a3e`, `#07070F` |

**Output format** — use this exact layout, replacing emoji and hex values:

**\<name\>**  ·  \<description\>
```
 🩷 primary    #ff7edb   ⚫ primaryLight #4d1a40
 🩵 secondary  #36f9f6   🟡 accent       #ffe66d
 🩶 background #262335   🩶 surface      #2d2145
 ⚪ text       #cbe3f6   🩶 textMuted    #848bbd
 🟢 success    #72f1b8   🟡 warning      #ffe66d   🔴 error #fe4450
 🩶 border     #433d60
```
Font: `<fontFamily>`  |  Radius: `<borderRadius>`
Feel: \<aesthetic\>  ·  \<personality tags\>
Density: \<density\>  |  Elevation: \<elevation\>  |  Motion: \<feel\>

> **Rendering note:** Output the color block inside a fenced code block (``` ``` ```) so the monospace alignment holds. The emoji provides a quick visual hue hint; the hex is the precise value. For light/near-white colors, ⚪ with a hex like `#ffffff` or `#fef4ee` is immediately recognizable as pale without needing a chip.

---

## Mode: List — Browse Saved Themes

### Cache

A cache file lives at `~/.claude/skills/theme-factory/themes-cache.json`. It stores all display data so listing only reads one file instead of N HTML files.

**Cache format:**
```json
{
  "themes": [
    {
      "name": "...",
      "description": "...",
      "file": "themes/<name>.html",
      "colors": { "primary": "...", "primaryLight": "...", "secondary": "...", "accent": "...",
                  "background": "...", "surface": "...", "surfaceAlt": "...", "text": "...",
                  "textMuted": "...", "border": "...", "success": "...", "warning": "...", "error": "..." },
      "typography": { "fontFamily": "..." },
      "spacing": { "borderRadius": "...", "density": "..." },
      "shadows": { "elevation": "..." },
      "motion": { "feel": "..." },
      "design": { "aesthetic": "...", "personality": [] }
    }
  ]
}
```

The cache is always up to date — extract appends to it, delete removes from it. List reads it directly with no staleness check.

### Steps

1. Read `~/.claude/skills/theme-factory/themes-cache.json`. If missing: "No themes saved yet. Use `/theme-factory` and say 'extract theme from <screenshot>' to create your first preset."
2. For each entry in `cache.themes`, display the inline swatch summary block using cached data.
3. After listing all themes, show a summary line:

```
── <N> themes saved ──────────────────────────────────
  ocean-breeze    → themes/ocean-breeze.html
  dark-terminal   → themes/dark-terminal.html
  warm-editorial  → themes/warm-editorial.html

To apply: "apply theme <name> to <file>"
To delete: "delete theme <name>"
```

---

## Mode: Delete — Remove a Preset

### Steps

1. Resolve the file path: `~/.claude/skills/theme-factory/themes/<name>.html`
2. Check it exists (Glob or Bash `Test-Path`). If not found, say: "No theme named '<name>' found. Use 'list themes' to see available presets."
3. Read the file and show the inline swatch summary as confirmation.
4. Ask: "Delete theme **<name>**? This cannot be undone. Reply 'yes' to confirm."
5. On confirmation: `Bash` — `Remove-Item "~/.claude/skills/theme-factory/themes/<name>.html"`
6. Remove the entry from `themes-cache.json`: read cache, filter out the deleted theme from `themes`, write cache back.
7. Confirm: "Deleted theme **<name>**."

---

## Mode: Apply — Use Theme as Design Baseline, Then Improve

The theme is a **starting point**, not a rigid contract. Use its colors, typography, and spacing as your design foundation — then exercise judgment to make the whole file look **cohesive, easy to read, and production-grade**. Think like a designer doing a professional reskin, not a script doing a find-replace.

**Production-grade means:**
- Every text element has WCAG AA contrast (≥ 4.5:1 for body text, ≥ 3:1 for large text/UI components) against its actual background — not just against the page canvas
- No color becomes invisible or nearly invisible after the theme switch (opacity artifacts, washed-out fills, near-white-on-white)
- JS-generated SVG and template-literal colors are audited and fixed — CSS variables cannot reach them
- Fill areas, overlays, and opacity values are recalibrated for the new background lightness
- The result looks intentionally designed for this theme, with no visible seams from the swap

---

### Step 1: Load the theme

Read `~/.claude/skills/theme-factory/themes/<name>.html`.
Parse the JSON from `<script id="theme-data">` to extract the full palette, typography, and design DNA.

Note the **theme's color mode** (dark vs light) from `colors.background` lightness.

---

### Step 2: Read and understand the target file

Before touching anything, read the file and understand:

- **What color mode is it?** (dark body background = dark mode; light = light mode)
- **Does a mode switch happen?** Theme dark + file light (or vice versa) is the case that needs the most repair
- **What shorthand CSS vars does the file define?** (e.g., `--bg`, `--card`, `--text`, `--accent`) — these are the file's own variable system
- **What is hardcoded?** Literal hex or rgba values in `color:`, `background:`, `border-color:`, gradients
- **Are there colored sections?** Hero banners, callout boxes, headers, and section highlights live on their own colored surface, not the page canvas
- **Does the file contain JavaScript that generates SVG or HTML with hardcoded colors?** Chart rendering, canvas drawing, or template literals with `stroke="#..."`, `fill="#..."`, or `color:#...` — CSS vars **cannot reach these**. Grep for hex patterns inside `<script>` tags.

> **MODE SWITCH WARNING — dark ↔ light:**
> If the file's current background lightness and the theme's background lightness are on opposite sides (one dark, one light), treat every hardcoded color as a potential failure. Colors designed for dark canvases (dim blues, near-whites, low-opacity fills) will be invisible or washed-out on cream/white, and vice versa. This case requires a full color audit beyond CSS variable remapping — plan to do Steps 4f, 4g, and 4h below before considering the apply complete.

---

### Step 3: Inject the theme token block

Inject a `/* Theme: <name> — applied by theme-factory */` `:root {}` block at the top of the file's `<style>` tag (or create one). The block contains the full theme token set plus a **remapping section** for any shorthand document vars found in Step 2.

```css
/* Theme: <name> — applied by theme-factory */
:root {
  /* ── Color tokens ── */
  --color-primary:         <hex>;
  --color-primary-light:   <hex>;
  --color-secondary:       <hex>;
  --color-accent:          <hex>;
  --color-bg:              <hex>;
  --color-surface:         <hex>;
  --color-surface-alt:     <hex>;
  --color-text:            <hex>;
  --color-text-muted:      <hex>;
  --color-text-on-primary: <hex>;
  --color-border:          <hex>;
  --color-success:         <hex>;
  --color-warning:         <hex>;
  --color-error:           <hex>;

  /* ── Typography ── */
  --font-family:         <value>;
  --font-family-mono:    <value>;
  --font-family-display: <value>;
  --font-size-base:      16px;
  --font-weight-heading: <value>;
  --font-weight-body:    <value>;
  --line-height:         <value>;

  /* ── Shape ── */
  --radius:        <value>;
  --radius-card:   <value>;
  --radius-button: <value>;

  /* ── Shadows ── */
  --shadow-sm: <value>;
  --shadow-md: <value>;
  --shadow-lg: <value>;

  /* ── Spacing ── */
  --space-1: <value>; --space-2: <value>; --space-3: <value>;
  --space-4: <value>; --space-6: <value>; --space-8: <value>;

  /* ── Motion ── */
  --duration-fast: <value>;
  --duration-base: <value>;
  --duration-slow: <value>;
  --easing:        <value>;

  /* ── Border ── */
  --border-width: <value>;

  /* ── Remap document vars → theme tokens ── */
  /* (only include vars that actually exist in this file) */
  --bg:     var(--color-bg);
  --card:   var(--color-surface);
  --card2:  var(--color-surface-alt);
  --border: var(--color-border);
  --accent: var(--color-primary);
  --text:   var(--color-text);
  --muted:  var(--color-text-muted);
  --green:  var(--color-success);
  --red:    var(--color-error);
  --yellow: var(--color-warning);
  /* ... adapt to what the file actually uses */
}
```

Common document-var → theme-token mappings:

| Document var | Theme token |
|--------------|------------|
| `--bg`, `--background`, `--page-bg` | `var(--color-bg)` |
| `--card`, `--surface`, `--panel` | `var(--color-surface)` |
| `--card2`, `--surface-alt`, `--alt` | `var(--color-surface-alt)` |
| `--border`, `--divider` | `var(--color-border)` |
| `--accent`, `--primary`, `--brand` | `var(--color-primary)` |
| `--secondary` | `var(--color-secondary)` |
| `--text`, `--fg` | `var(--color-text)` |
| `--muted`, `--subtle`, `--dim` | `var(--color-text-muted)` |
| `--radius`, `--rounded` | `var(--radius-card)` |
| `--green`, `--success` | `var(--color-success)` |
| `--red`, `--error`, `--danger` | `var(--color-error)` |
| `--yellow`, `--warning` | `var(--color-warning)` |

If an existing `/* Theme: ... */` block is already present, replace it entirely.

---

### Step 4: Harmonize — fix what the variable injection can't reach

The remap block handles anything that uses CSS vars. Now look at what remains: hardcoded colors, font stacks, and colored sections that need design decisions.

**Use the theme as your baseline color palette when making these decisions.** You are not enforcing a strict rule — you are making the page look like it belongs to this theme.

**4a. Color distribution — use the full palette, not just primary**

A professional dashboard feels dynamic because it uses the full palette with intention. If the file currently uses only one accent color everywhere (all-primary, all-cyan, etc.), redistribute color roles across the theme palette:

| UI element | Recommended color |
|-----------|------------------|
| Primary data line / main series / hero metric | `primary` (e.g. slate blue `#4f5d75`) |
| Secondary data line / comparison series / supporting metric | `secondary` or `accent` (e.g. coral `#ef8354`) |
| Positive / profit / gain outcome | `success` |
| Neutral / unchanged / breakeven outcome | `primary` (desaturated) or `textMuted` |
| Warning / at-risk / partial outcome | `warning` |
| Negative / loss / error outcome | `error` |
| Active tab / selected state | `primary` with full opacity |
| Inactive tab / default state | `textMuted` border, `text` label |
| Section headings / stat labels | `primary` |
| Chart grid lines | `border` hex — subtle, not distracting |
| Reference / FV lines | `textMuted` hex — dashed, secondary hierarchy |
| Scenario buttons / pills | Border `primary`; active: filled `primary`; each scenario can carry its own semantic color |
| Badge / tag accents | Rotate between `primaryLight`, `success`, `warning`, `error` by meaning |
| Card borders or left-accent bars | `secondary` or `accent` for visual rhythm on repeated cards |

**Avoid:** mapping every interactive element to the same color. If the primary color appears in >60% of colored elements, look for opportunities to introduce `secondary` or `accent` as a counterpoint.

**For JS-generated charts specifically:** use `primary` for the main price/value line, `accent` (coral/orange) for comparison or signal lines, `success`/`warning`/`error` for scenario outcomes. This alone makes charts feel intentionally designed rather than monochrome.

**4b. Font-family on body / html**
If `font-family` on `body` is hardcoded (not `var(--font-family)`), update it to `var(--font-family)`.

**4c. Hardcoded text colors that clash with the new background**
Text designed for a dark canvas becomes invisible on a light one (and vice versa). Look for:
- Near-white text values (`#c5c9d9`, `#e8eaf0`, `#ccc`, `#ddd`, lightness > 70%) on a light-theme file → replace with `var(--color-text-muted)` for secondary text or `var(--color-text)` for body copy
- Near-black text values (`#111`, `#1a1a1a`, lightness < 15%) on a dark-theme file → replace with `var(--color-text)`

Use `replace_all: true` when the same value appears in multiple rules.

**4d. Colored sections (hero, header, callout, banner)**
These live on their own surface, not the page canvas. They need special treatment:
- If the section has a **hardcoded dark gradient or dark solid background** and the new theme is light: replace the gradient with one derived from the theme's primary color (e.g., `linear-gradient(135deg, <primary> 0%, <darker-primary-shade> 100%)`). Make sure all text inside uses white or `var(--color-text-on-primary)` explicitly — it won't inherit from the body.
- If the section already looks good on the new theme (e.g., a colored callout that still works), leave it but ensure text contrast is explicit.
- For pill/badge/tag elements inside colored sections that used `rgba()` tints from the old palette: update the tint hue to match the new theme's color family, keeping similar opacity.

**4e. Semi-transparent overlays**
- On **light themes**: dark overlays (`rgba(0,0,0,X)`) at low opacity (≤ 0.08) are fine for depth. Higher opacity feels heavy — reduce.
- On **dark themes**: light overlays (`rgba(255,255,255,X)`) at low opacity work for highlights. High opacity is jarring — reduce.
- If the overlay direction is wrong for the new mode, flip it.

**4f. JS-generated SVG and template-literal colors (MANDATORY on mode switch)**

CSS variables cannot reach colors hardcoded inside `<script>` blocks. After applying the `:root` block, grep the file for hex color patterns in JavaScript:

```
Grep patterns to run inside <script> tags:
  stroke="#[0-9a-fA-F]{3,6}"
  fill="#[0-9a-fA-F]{3,6}"
  color:#[0-9a-fA-F]{3,6}
  "#[0-9a-fA-F]{6}"   (JS object color fields, template literals)
  '[0-9a-fA-F]{6}'
```

For each found color, evaluate it against the **new** background:

| Found color type | Action |
|-----------------|--------|
| Grid/axis lines (was dark navy for dark bg) | Replace with light border color from theme (e.g. `--color-border` hex) |
| Reference/guide lines (was dim gray) | Replace with `textMuted` hex — visible but not dominant |
| Primary data line (was washed-out cyan/blue on light bg) | Replace with theme accent or primary hex — must pop against new bg |
| Status/scenario colors (bright neon green, yellow, red) | Remap to theme semantic colors (`success`, `warning`, `error`) which are calibrated for contrast |
| Text labels inside SVG (`fill="#..."`) | Replace with `textMuted` or `text` hex depending on hierarchy |
| Arrow/marker text on colored shapes (`fill` inside circle) | Use `#ffffff` if shape is dark, `#000000` or `text` hex if shape is light |
| Fill areas with `opacity` attribute | See 4g below |

Use `replace_all: true` when the same hex appears multiple times. After replacing, re-grep to confirm 0 remaining old-theme hex values.

**4g. Opacity recalibration for fill areas and verdict backgrounds**

Opacity values designed for dark backgrounds are often too faint on light ones:

| Pattern | Dark-bg original | Light-bg fix |
|---------|-----------------|--------------|
| SVG fill area under a line chart | `opacity="0.07"` or `"0a"` (4%) | Double it: `opacity="0.14"` or `"18"` (~9.5%) |
| Verdict / result box background tint | `color+'0a'` (4% tint) | `color+'18'` or `color+'20'` |
| Hover row highlight | `rgba(accent, 0.04)` | `rgba(primary, 0.06–0.08)` |

Adjust until fills are clearly visible but not overpowering the content above them.

**4h. WCAG contrast verification pass**

After all color substitutions, mentally check every text-on-background pairing against WCAG AA minimums:

| Contrast ratio | Requirement |
|---------------|-------------|
| ≥ 4.5:1 | Body text, labels, axis ticks, legend items, form values |
| ≥ 3:1 | Large text (≥ 18px bold or ≥ 24px normal), UI component boundaries |

**Known failure patterns on light cream backgrounds (`#FCFBF4` / `#F5F3EC`):**

| Old color | Approx ratio on cream | Status | Replace with |
|-----------|----------------------|--------|--------------|
| `#ffd166` bright yellow | ~1.3:1 | FAIL | theme `warning` (`#d4980e`) or darker |
| `#4fc3f7` cyan | ~1.8:1 | FAIL | theme `primary` or `accent` |
| `#52d68a` neon green | ~2.4:1 | FAIL | theme `success` (`#3d9e6d`) |
| `#ff7a7a` light coral | ~2.8:1 | FAIL | theme `error` (`#c94040`) |
| `#9fb0c8` light blue-gray | ~2.1:1 | FAIL | theme `textMuted` (`#7a8299`) |
| `#d4980e` amber on `#EEECE3` | ~2.2:1 | FAIL | theme `primary`/`accent` for text; amber is OK as border/indicator only |
| `#f0a030` orange on cream | ~2.5:1 | FAIL | Darken to `#c07000` or similar (~4.7:1) |

If any text color fails, replace it with the nearest theme semantic color that passes. Never leave failing contrast as "good enough."

**4i. Use your design judgment**
The above are systematic checks, not an exhaustive rulebook. If something looks obviously off but doesn't fit a rule above, fix it. The goal is a page that looks intentionally designed for this theme at a professional, production-ready standard — zero visible seams from the swap.

---

### Step 5: Inject strategy by file type

| File type | Strategy |
|-----------|----------|
| `.html` | Prepend the `:root {}` block at the start of the existing `<style>` tag. If none exists, insert `<style>\n<block>\n</style>` as first child of `<head>`. |
| `.css` | Replace existing `:root { ... }` entirely, or prepend if none exists. |
| `.md` / `.txt` | Prepend `<style>\n<block>\n</style>` as the very first line. |

Always use `Edit` for targeted changes — never rewrite the whole file.

---

### Step 6: Report

```
Applied theme <name> to <file>

Variables injected:  <N> CSS tokens in :root
Shorthand remapped:  <list of --var remappings added>
Font updated:        body font-family → var(--font-family)
Color repairs:       <N> hardcoded CSS values replaced (e.g. "#c5c9d9 × 4 → var(--color-text-muted)")
Section fixes:       <list of selectors touched, e.g. ".hero — gradient updated to primary palette">
JS/SVG audit:        <N> hardcoded hex values replaced in <script> blocks (e.g. "#4fc3f7 × 3 → #ef8354 [DR line]")
Opacity fixes:       <list, e.g. "fill area opacity 0.07 → 0.14, verdict bg '0a' → '18'">
Contrast verified:   All text-on-background pairings ≥ 4.5:1 (or ≥ 3:1 for large text)

  aesthetic: <value>  ·  density: <value>  ·  motion: <value>
```

If anything could **not** be fixed, list it explicitly under a `⚠ Manual review needed:` line — e.g. external stylesheets, canvas-drawn graphics, or colors injected by a third-party library. Never omit this section if issues remain.

---

## Tips for Color Extraction

### From a screenshot — prioritize these visual areas:

- **Headers and hero areas** → primary color
- **Call-to-action buttons** → primary or accent
- **Page/canvas fill** → background
- **Content panels, cards** → surface
- **Navigation bars** → may reveal a dark variant of primary
- **Body text blocks** → text color
- **Footnotes, metadata, labels** → textMuted
- **Dividers, card outlines** → border color

For dark themes: background will be very dark (< 30% lightness), surface will be slightly lighter, text will be near-white.

For light themes: background is near-white or very light, surface is pure white or light gray, text is near-black.

**Estimate colors you can't see directly** (status colors) — match the saturation level of what you can see. A muted-tone design should have muted success/warning/error too, not neon green/red.

### From HTML — parsing priority

1. `:root { --color-* }` variables (highest fidelity — use directly)
2. `body`, `header`, `.btn`, `.card` CSS rules
3. Inline `style=""` attributes on prominent elements
4. Tailwind/utility class names (map to known hex values)

### From text descriptions — accuracy heuristics

- Named colors ("cobalt blue", "warm amber") → pick a specific, intentional hex, not a generic one
- Reference designs ("like Notion", "like GitHub dark") → match the known palette closely
- Mood words ("cozy", "clinical", "hacker") → guide saturation and contrast, not just hue
- When the user names a specific hex or RGB value, use it exactly

---

## Reuse Tip

Once a theme is applied to an HTML file, every element that uses `var(--color-primary)`, `var(--font-family)`, etc. automatically reflects the theme. Encourage users to build their HTML/dashboards/reports with these variable names so swapping themes is a one-command operation.
