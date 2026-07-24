# Stock Analysis — HTML Theme (Dynamic)

The theme is picked per-report by `style-selection.md`, not fixed. This file has two parts: **(1)** how to pull the chosen theme's actual tokens in, **(2)** the component CSS every report shares, written entirely against those tokens — no hex literal ever belongs in this file or in a generated report.

---

## Part 1 — Load the Selected Theme

1. Read `~/.claude/skills/theme-factory/themes/<selected-theme>.html`. It contains a ready-made `<link>` Google Fonts block and a complete `:root { ... }` token block inside `<style>` — copy both verbatim into the report's `<head>`.
2. Read `~/.claude/skills/theme-factory/themes/<selected-theme>.md` — use its **Color Role Guidance** section when a component below gives you a choice (e.g. which token carries "secondary" weight), and its **Apply-Mode Notes** for anything theme-specific (some themes explicitly forbid glow/luminescence, some want a specific gradient treatment — honor those).
3. Above the copied `:root` block, add the signature comment so the file is detectable by theme-factory later:
   ```css
   /* Theme: <selected-theme> - applied by obs-theme-factory */
   ```
4. Immediately after the copied token block, append the shorthand aliases the component CSS below relies on (only the ones the theme file doesn't already define):
   ```css
   --bg: var(--color-bg);
   --card: var(--color-surface);
   --card2: var(--color-surface-alt);
   --border: var(--color-border);
   --accent: var(--color-primary);
   --green: var(--color-success);
   --red: var(--color-error);
   --yellow: var(--color-warning);
   --text: var(--color-text);
   --muted: var(--color-text-muted);
   --radius: var(--radius-card);
   ```
5. **Background** — check the theme's `background.type` field (from its JSON):
   - `solid` → `body { background-color: var(--color-bg); }`, no background-image.
   - `pattern` / `noise` / `gradient` → use the theme's own `--bg-image` / `--bg-size` / `--bg-position` / `--bg-repeat` tokens (already in the copied `:root` block) on `body`. Do not invent a new texture — the fallback marble-grain SVG in older versions of this file was wisdom-specific and must not leak into other themes.
6. **Font weights** — `--font-weight-heading` / `--font-weight-body` come from the theme; use them on `h1`-`h3`/`.section-title`/`.stat-value` (heading weight) and body copy (body weight) instead of assuming 700 everywhere.

---

## Part 2 — Component CSS (token-only, copy exactly)

Every value below is a `var(--...)` reference or a `color-mix()` derived from one — never a hex literal. Paste this block after the token `:root` from Part 1.

### Body & Page Container

```css
body {
  font-family: var(--font-family);
  font-weight: var(--font-weight-body, 400);
  color: var(--text);
  line-height: var(--line-height);
  margin: 0;
  padding: 20px;
}

.page {
  max-width: 900px;
  margin: 0 auto;
}
```

(`.page` max-width is overridden per Part 3 of `layout.md` using the selected layout's `grid.maxWidth` — leave the 900px default only if no layout override applies.)

### Hero Banner

```css
.hero {
  background: var(--gradient-hero);
  border-top: 3px solid var(--color-accent);
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  color: var(--color-text-on-primary);
  padding: 36px 32px;
  margin-bottom: 24px;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: "";
  position: absolute;
  top: -60px;
  right: -60px;
  width: 220px;
  height: 220px;
  background: radial-gradient(circle, color-mix(in srgb, var(--color-primary-light) 12%, transparent) 0%, transparent 70%);
  border-radius: 50%;
}
.hero-ticker {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2.5px;
  color: var(--color-accent);
  text-transform: uppercase;
  margin-bottom: 6px;
  font-family: var(--font-family-display);
}
.hero-name {
  font-size: 28px;
  font-weight: var(--font-weight-heading, 700);
  margin-bottom: 8px;
  color: var(--color-text-on-primary);
  font-family: var(--font-family-display);
  letter-spacing: 0.03em;
}
.hero-tagline {
  font-size: 15px;
  color: color-mix(in srgb, var(--color-text-on-primary) 78%, transparent);
  max-width: 540px;
  margin-bottom: 20px;
  font-style: italic;
}
.hero-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
.pill {
  padding: 4px 14px;
  border-radius: 50px;
  font-size: 11px;
  font-weight: 600;
  border: 1px solid;
  letter-spacing: 0.04em;
  font-family: var(--font-family-display);
}
.pill-blue {
  background: color-mix(in srgb, var(--color-primary-light) 18%, transparent);
  border-color: color-mix(in srgb, var(--color-primary-light) 45%, transparent);
  color: var(--color-primary-light);
}
.pill-green {
  background: color-mix(in srgb, var(--color-success) 25%, transparent);
  border-color: color-mix(in srgb, var(--color-success) 60%, transparent);
  color: color-mix(in srgb, var(--color-success) 55%, white);
}
.pill-red {
  background: color-mix(in srgb, var(--color-error) 25%, transparent);
  border-color: color-mix(in srgb, var(--color-error) 60%, transparent);
  color: color-mix(in srgb, var(--color-error) 55%, white);
}
.pill-yellow {
  background: color-mix(in srgb, var(--color-warning) 25%, transparent);
  border-color: color-mix(in srgb, var(--color-warning) 60%, transparent);
  color: color-mix(in srgb, var(--color-warning) 55%, white);
}
```

### Section & Card Structure

```css
.section {
  margin-bottom: 32px;
}
.section-title {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 14px;
}

.card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 20px 22px;
  margin-bottom: 14px;
}
.card h3 {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin: 0 0 10px 0;
}

.grid-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}
.grid-3 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}
```

### Stat Grid

```css
.stat-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
}

.stat-card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 16px 18px;
}
.stat-label {
  font-family: var(--font-family-display);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 6px;
}
.mini-stat-label {
  font-family: var(--font-family-display);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.2px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 4px;
}
.stat-value {
  font-family: var(--font-family-display);
  font-size: 22px;
  font-weight: var(--font-weight-heading, 700);
  color: var(--color-text);
}
.stat-sub {
  font-family: var(--font-family-mono);
  font-size: 12px;
  color: var(--muted);
  margin-top: 4px;
}
.val-green { color: var(--color-success); }
.val-red { color: var(--color-error); }
.val-yellow { color: var(--color-warning); }
```

### TL;DR Box

```css
.tldr {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-md);
  padding: 22px 24px;
  margin-bottom: 28px;
}
.tldr h2 {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin: 0 0 14px 0;
}
.tldr-item {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  margin-bottom: 10px;
  font-size: 15px;
  line-height: 1.55;
}
/* Symbol spans — always 16px wide so text column aligns regardless of symbol width */
.tldr-sym {
  width: 16px;
  text-align: center;
  flex-shrink: 0;
  font-family: var(--font-family-mono);
  font-weight: 800;
}
```

### Analyst Scorecard Meters

```css
.meter-row { margin-bottom: 14px; }
.meter-label {
  display: flex;
  justify-content: space-between;
  font-size: 13px;
  margin-bottom: 5px;
  font-family: var(--font-family-display);
}
.meter-label span:last-child {
  font-weight: 700;
  font-family: var(--font-family-mono);
}
.meter-track {
  background: var(--card2);
  border-radius: 6px;
  height: 10px;
  overflow: hidden;
}
.meter-fill { height: 100%; border-radius: 6px; }
.meter-fill.green { background: var(--green); }
.meter-fill.yellow { background: var(--yellow); }
.meter-fill.red { background: var(--red); }
```

### Scenario Cards

```css
.scenario-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}
.scenario-card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 18px 20px;
}
.scenario-card h3 {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 1px;
  text-transform: uppercase;
  margin: 0 0 6px 0;
}
.scenario-prob {
  font-family: var(--font-family-mono);
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 4px;
}
.scenario-target {
  font-family: var(--font-family-mono);
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 12px;
}
.scenario-card ul {
  margin: 0;
  padding-left: 16px;
  font-size: 14px;
  line-height: 1.6;
}
.scenario-bull h3 { color: var(--color-success); }
.scenario-base h3 { color: var(--color-warning); }
.scenario-bear h3 { color: var(--color-error); }
```

### Timeline Component

```css
.timeline { position: relative; padding-left: 28px; }
.timeline::before {
  content: "";
  position: absolute;
  left: 7px;
  top: 6px;
  bottom: 6px;
  width: 2px;
  background: var(--border);
}
.timeline-item { position: relative; margin-bottom: 20px; }
.timeline-dot {
  position: absolute;
  left: -25px;
  top: 4px;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid var(--border);
  background: var(--card2);
}
.timeline-dot.past { background: var(--color-text-muted); border-color: var(--color-text-muted); }
.timeline-dot.present {
  background: var(--color-primary);
  border-color: var(--color-primary);
  width: 14px;
  height: 14px;
  left: -26px;
}
.timeline-dot.future { background: var(--card); border-color: var(--color-accent); }
.timeline-date {
  font-family: var(--font-family-mono);
  font-size: 11px;
  color: var(--muted);
  margin-bottom: 2px;
}
.timeline-event { font-size: 14px; line-height: 1.5; }
```

### Verdict / Bottom Line Card

```css
.verdict {
  background: linear-gradient(135deg, var(--color-surface) 0%, var(--color-surface-alt) 100%);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-md);
  padding: 28px 30px;
}
.verdict-title {
  font-family: var(--font-family-display);
  font-size: 14px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 16px;
}
.verdict p { font-size: 16px; line-height: 1.7; margin-bottom: 14px; }
.verdict p:last-child { margin-bottom: 0; }
```

### Icon Rows (Competitive Edge, Growth/Risk cards)

```css
.item-row { display: flex; align-items: flex-start; gap: 12px; margin-bottom: 14px; }
.item-icon { width: 20px; flex-shrink: 0; text-align: center; font-size: 14px; margin-top: 1px; }
.item-title {
  font-family: var(--font-family-display);
  font-size: 12px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 2px;
}
.item-desc { font-size: 14px; line-height: 1.55; }
.item-meta {
  font-family: var(--font-family-mono);
  font-size: 11px;
  color: var(--muted);
  margin-top: 3px;
}
```

### Debate Box

```css
.debate-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.debate-card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 20px 22px;
}
.debate-card h3 {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 1px;
  text-transform: uppercase;
  margin: 0 0 12px 0;
}
.debate-card.optimist h3 { color: var(--color-success); }
.debate-card.pessimist h3 { color: var(--color-error); }
.debate-card ul { margin: 0; padding-left: 16px; font-size: 14px; line-height: 1.65; }
.debate-card li { margin-bottom: 6px; }
```

### Donut Chart

The SVG donut is 200×200. Center is at cx="100" cy="100". Use `r="70"` for the ring (circumference ≈ 440). Each segment is a `<circle>` with `stroke-dasharray` and `stroke-dashoffset`. Legend sits beside it in a flex row.

The empty-ring base circle uses `stroke="var(--border)"`. Each filled segment uses one of `var(--color-primary)`, `var(--color-secondary)`, `var(--color-accent)`, `var(--color-success)`, `var(--color-warning)` in that priority order (repeat/mix if more than 5 segments) — never introduce a color outside those five tokens. Center label text uses `fill="var(--color-text)"` and `font-family` matching `--font-family-display`.

```css
.donut-wrap { display: flex; align-items: center; gap: 28px; flex-wrap: wrap; }
.donut-legend { flex: 1; min-width: 180px; }
.legend-row { display: flex; align-items: center; gap: 8px; margin-bottom: 8px; font-size: 14px; }
.legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.legend-pct { font-family: var(--font-family-mono); font-weight: 700; margin-left: auto; font-size: 13px; }
```

Segment bar rows (current vs projected, below the donut) — `.seg-fill`/`.seg-proj` inline `background` uses the same segment token as the matching donut wedge:

```css
.seg-row { margin-bottom: 16px; }
.seg-label {
  display: flex;
  justify-content: space-between;
  font-size: 13px;
  margin-bottom: 5px;
  font-family: var(--font-family-display);
  font-weight: 700;
  letter-spacing: 0.5px;
}
.seg-track { background: var(--card2); border-radius: 4px; height: 8px; overflow: hidden; position: relative; }
.seg-fill { height: 100%; border-radius: 4px; }
.seg-proj { height: 100%; border-radius: 4px; opacity: 0.45; }
.seg-note { font-size: 12px; color: var(--muted); margin-top: 4px; }
```

### Flat / Tabular Components (default for comparable or tabular content)

Per `ruleset.md`'s card-discipline rule: `.tldr` and `.verdict` are the only two boxed/shadowed treatments a report gets — every other section uses one of these flatter components instead of a `.card`/`.stat-card`/`.scenario-card`/`.debate-card` grid. The boxed components above (Stat Grid, Scenario Cards, Debate Box) stay defined for the rare case a section genuinely needs individually-weighted boxes, but default to the components below first.

```css
/* Exhibit visual — bordered, unshadowed frame for a chart (never a card: no fill, no shadow) */
.exhibit-visual {
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 20px 22px;
  margin-bottom: 14px;
}

/* Subhead — a labeled sub-block within a section that doesn't need its own card */
.subhead {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin: 0 0 10px 0;
}

/* Split columns — flat two-up text layout divided by a hairline rule, no card boxes.
   Default for any paired-column content (story/bet, how-it-works/why-clever,
   opportunity/why-we-win, growth/risks, optimist/pessimist). */
.split-cols { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; }
.split-cols > div + div { border-left: 1px solid var(--border); padding-left: 32px; }
.split-cols h3 {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: var(--font-weight-heading, 700);
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin: 0 0 10px 0;
}
.split-cols p { font-size: 15px; line-height: 1.65; margin: 0; }
.split-cols ul { margin: 0; padding-left: 18px; font-size: 15px; line-height: 1.65; }
.split-cols li { margin-bottom: 6px; }

/* Item list — icon rows separated by hairline rules instead of sitting in a card.
   Default wrapper for Competitive Edge and Growth/Risk item-rows. */
.item-list .item-row { border-bottom: 1px solid var(--border); padding-bottom: 14px; }
.item-list .item-row:last-child { border-bottom: none; padding-bottom: 0; margin-bottom: 0; }

/* Report table — theme-native tabular exhibit for comparable rows: financial metrics,
   scenarios, rated items. Default for Financial Snapshot, Hidden Catalyst stats,
   Catalyst Scenarios, Overall Scenario Analysis, and Wall Street Consensus. */
.report-table-wrap { overflow-x: auto; }
.report-table { width: 100%; border-collapse: collapse; font-size: 14px; }
.report-table th {
  font-family: var(--font-family-display);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--muted);
  text-align: left;
  padding: 0 16px 8px 0;
  border-bottom: 2px solid var(--color-primary);
  white-space: nowrap;
}
.report-table td {
  padding: 14px 16px 14px 0;
  border-bottom: 1px solid var(--border);
  vertical-align: top;
}
.report-table tr:hover td { background: color-mix(in srgb, var(--color-primary) 4%, transparent); }
.report-table tr:last-child td { border-bottom: 1px solid var(--border); }
.report-table .row-label {
  font-family: var(--font-family-display);
  font-weight: 700;
  letter-spacing: 0.3px;
  color: var(--text);
  white-space: nowrap;
}
.report-table .mono { font-family: var(--font-family-mono); font-weight: 700; }
.report-table ul { margin: 0; padding-left: 16px; font-size: 13px; line-height: 1.55; }
.report-table li { margin-bottom: 3px; }
```

Add the matching responsive rules to every report's required media-query block (`layout.md`'s Page Shell):

```css
@media (max-width: 760px) {
  .split-cols { grid-template-columns: 1fr; }
  .split-cols > div + div {
    border-left: none;
    padding-left: 0;
    border-top: 1px solid var(--border);
    padding-top: 20px;
  }
}
```
