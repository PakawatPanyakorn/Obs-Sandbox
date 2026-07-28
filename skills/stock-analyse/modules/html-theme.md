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

### Stat Grid (default for Financial Snapshot)

One of the report's established boxed-treatment exceptions (see `layout.md`'s card discipline note and `ruleset.md`'s "Card overuse" rule) — the only other boxed defaults are `.tldr`/`.verdict` and `.debate-card`. Numeric tiles read faster than table rows for the handful of headline metrics a reader scans for first.

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

### Analyst Scorecard Meters (legacy fallback — no longer the default)

The Analyst Scorecard's default is now the Radar Chart component below. This meter-row CSS stays defined for the rare edge case (e.g. a non-HTML medium that can't render SVG) but a fresh report should not reach for it without a specific reason.

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

### Scorecard Radar Chart (default for Analyst Scorecard)

Flat on the page — not a boxed card. Pairs with the "Analyst Scorecard Radar Chart" block in `layout.md`'s "Shared Interactive JS" appendix, which builds the chart from the `METRICS` array and auto-fits the `viewBox` to the actually-rendered label text (see `ruleset.md`'s "Match canvas to content, not the reverse" rule — never hand-pick a `viewBox` size and hope the font fits).

The `<svg id="scorecardRadar" width="480" ...>` markup in Section 9 keeps `width="480"` as a presentation-attribute fallback, but the `#scorecardRadar { width: 100%; height: auto }` rule below overrides it for layout purposes — the browser derives height from the `viewBox` aspect ratio instead. Combined with `.radar-wrap`'s `width: 100%; max-width: 480px`, the chart caps at 480px on desktop and shrinks fluidly on narrow viewports instead of overflowing (this was a real bug in an early report — the chart clipped its own axis labels off the right edge on mobile until this was added).

```css
.radar-hint {
  font-family: var(--font-family-mono);
  font-size: 10px;
  color: var(--muted);
  text-align: center;
  margin-bottom: 10px;
}
.scorecard-body { display: flex; gap: 24px; align-items: flex-start; flex-wrap: wrap; }
.radar-wrap { flex-shrink: 0; display: flex; justify-content: center; width: 100%; max-width: 480px; }
#scorecardRadar { width: 100%; height: auto; display: block; }
.radar-axis-label {
  font-family: var(--font-family-display);
  font-size: 15px;
  font-weight: 700;
  fill: var(--color-primary);
  cursor: pointer;
}
.radar-dot { cursor: pointer; transition: r 0.15s; }
.radar-dot:hover, .radar-dot.active { r: 10; }

/* Answer panel — a hairline divider, never a filled/boxed card (matches
   .split-cols' own divider convention; see ruleset.md's card-overuse rule) */
.scorecard-why {
  flex: 1;
  min-width: 220px;
  border-left: 1px solid var(--border);
  padding: 4px 0 4px 26px;
}
.scorecard-why .wp-title {
  font-family: var(--font-family-display);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--color-primary);
  margin-bottom: 6px;
}
.scorecard-why .wp-score {
  font-family: var(--font-family-mono);
  font-size: 12px;
  color: var(--color-accent);
  font-weight: 700;
  margin-bottom: 10px;
  display: block;
}
.scorecard-why .wp-text { font-size: 15px; line-height: 1.65; margin: 0; }
.scorecard-why .wp-back {
  display: block;
  font-family: var(--font-family-mono);
  font-size: 11px;
  color: var(--muted);
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  margin-bottom: 10px;
  text-decoration: underline;
}
.scorecard-why .wp-back:hover { color: var(--color-accent); }

@media (max-width: 640px) {
  .scorecard-body { flex-direction: column; }
  .scorecard-why {
    border-left: none;
    border-top: 1px solid var(--border);
    padding: 20px 0 0;
    margin-top: 20px;
  }
}
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

### Icon Rows (Competitive Edge) / Row Text (also reused by Severity List)

`.item-row`/`.item-icon` are Competitive Edge's own row wrapper. `.item-title`/`.item-desc`/`.item-meta` are shared row-content primitives — Severity List rows (Growth Drivers, Risks) reuse these same three classes inside `.sev-row` instead of `.item-row`, so risk/driver text keeps the same typographic treatment as everywhere else.

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

### Debate Box (default for Investor Debate)

One of the report's established boxed-treatment exceptions — a debate is a genuinely oppositional shape, not paired narrative, so it earns its own card identity instead of the `.split-cols` flat default.

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

/* VS badge — centered overlay, only makes sense with two side-by-side cards;
   hidden once .debate-grid collapses to one column (see the 760px media query) */
.debate-vs { position: relative; }
.debate-vs .vs-badge {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: var(--color-primary);
  color: var(--color-text-on-primary);
  font-family: var(--font-family-display);
  font-size: 11px;
  font-weight: 700;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: var(--shadow-md);
  z-index: 2;
  letter-spacing: 0.5px;
}
@media (max-width: 760px) {
  .debate-vs .vs-badge { display: none; }
}
```

### Donut Chart

The SVG donut is 200×200. Center is at cx="100" cy="100". Use `r="70"` for the ring (circumference ≈ 440). Each segment is a `<circle>` with `stroke-dasharray` and `stroke-dashoffset`. Legend sits beside it in a flex row.

The empty-ring base circle uses `stroke="var(--border)"`. Each filled segment uses one of `var(--color-primary)`, `var(--color-secondary)`, `var(--color-accent)`, `var(--color-success)`, `var(--color-warning)` in that priority order (repeat/mix if more than 5 segments) — never introduce a color outside those five tokens. Center label text uses `fill="var(--color-text)"` and `font-family` matching `--font-family-display`.

```css
.donut-wrap { display: flex; align-items: center; gap: 28px; flex-wrap: wrap; }
.donut-legend { flex: 1; min-width: 180px; }
.legend-row {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 8px;
  font-size: 14px;
  /* hover-link state */
  border-radius: 3px;
  padding: 2px 4px;
  cursor: pointer;
  transition: background 0.15s, opacity 0.15s;
}
.legend-row.dim { opacity: 0.35; }
.legend-row.hi { background: color-mix(in srgb, var(--color-accent) 10%, transparent); }
.legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.legend-pct { font-family: var(--font-family-mono); font-weight: 700; margin-left: auto; font-size: 13px; }

/* Hover-link target state, applied to each donut <circle data-seg="..."> */
.seg-dim { opacity: 0.3; transition: opacity 0.15s; }
.seg-hi { transition: opacity 0.15s, filter 0.15s; }
.seg-hi.active-glow { filter: drop-shadow(0 0 4px color-mix(in srgb, var(--color-accent) 55%, transparent)); }
```

Give each donut wedge `<circle>` a `data-seg="<slug>"` attribute matching its `.legend-row`'s own `data-seg` — that's the only markup requirement for the hover-link JS in `layout.md`'s appendix to work.

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

Per `ruleset.md`'s card-discipline rule, boxed/shadowed treatment is reserved for four moments — `.tldr`, `.verdict`, `.stat-card` (Financial Snapshot), and `.debate-card` (Investor Debate) — every other section uses one of these flatter components instead of a `.card`/`.scenario-card` grid.

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
   Default wrapper for Competitive Edge. */
.item-list .item-row { border-bottom: 1px solid var(--border); padding-bottom: 14px; }
.item-list .item-row:last-child { border-bottom: none; padding-bottom: 0; margin-bottom: 0; }

/* Severity list — a colored stripe per row instead of an icon, hairline-divided.
   Default for the Growth Drivers / Risks columns (Section 10) — both columns use
   this same component so they read as one consistent system side by side, not
   two different treatments. Green stripe = driver, red = active/severe risk,
   yellow = reduced/moderate risk. */
.severity-list .sev-row { display: flex; align-items: flex-start; gap: 12px; padding: 10px 0; border-bottom: 1px solid var(--border); }
.severity-list .sev-row:last-child { border-bottom: none; }
.sev-stripe { width: 4px; align-self: stretch; border-radius: 2px; flex-shrink: 0; min-height: 40px; }

/* Report table — theme-native tabular exhibit for comparable rows: rated items,
   sizing metrics. Default for Hidden Catalyst stats and Wall Street Consensus
   (Financial Snapshot now uses Stat Grid tiles; Catalyst Scenarios and Overall
   Scenario Analysis now default to Scenario Tabs — see below). */
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

/* Scenario tabs — Bull/Base/Bear or Positive/Mixed/Negative as clickable tabs,
   one reusable pattern for Section 11 (always) and Section 7's Catalyst
   Scenarios (when the outcome sets are dense enough to earn the click — see
   ruleset.md's "Interaction must earn its click" rule). */
.scenario-tabs .tabs { display: flex; gap: 8px; margin-bottom: 16px; }
.scenario-tabs .tab {
  flex: 1;
  text-align: center;
  cursor: pointer;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 10px 8px;
  background: var(--card);
  font-family: var(--font-family-display);
  font-size: 12px;
  font-weight: 700;
  transition: background 0.15s, border-color 0.15s, transform 0.1s;
}
.scenario-tabs .tab:hover { transform: translateY(-1px); }
.scenario-tabs .tab .p { font-family: var(--font-family-mono); font-weight: 700; display: block; font-size: 14px; margin-top: 3px; }
.scenario-tabs .tab.bull, .scenario-tabs .tab.positive { color: var(--green); }
.scenario-tabs .tab.base, .scenario-tabs .tab.mixed { color: var(--yellow); }
.scenario-tabs .tab.bear, .scenario-tabs .tab.negative { color: var(--red); }
.scenario-tabs .tab.active.bull, .scenario-tabs .tab.active.positive { background: color-mix(in srgb, var(--green) 14%, var(--card)); border-color: var(--green); }
.scenario-tabs .tab.active.base, .scenario-tabs .tab.active.mixed { background: color-mix(in srgb, var(--yellow) 14%, var(--card)); border-color: var(--yellow); }
.scenario-tabs .tab.active.bear, .scenario-tabs .tab.active.negative { background: color-mix(in srgb, var(--red) 14%, var(--card)); border-color: var(--red); }
.scenario-tabs .tab-panel {
  display: none;
  background: var(--card);
  border-radius: var(--radius);
  padding: 18px 20px;
  border-left: 3px solid var(--border);
}
.scenario-tabs .tab-panel.show { display: block; }
.scenario-tabs .tab-panel h4 { margin: 0 0 4px; font-family: var(--font-family-display); font-size: 14px; letter-spacing: 0.5px; }
.scenario-tabs .tab-panel .range { font-family: var(--font-family-mono); font-size: 12.5px; color: var(--muted); margin-bottom: 10px; }
.scenario-tabs .tab-panel ul { margin: 0; padding-left: 18px; font-size: 14px; line-height: 1.6; }
.scenario-tabs .tab-panel li { margin-bottom: 5px; }

/* Scroll-spy rail — sticky section nav, one per report (see layout.md's
   "Section Navigation" note). Fixed to the viewport, not the page column, so
   it doesn't compete with .page's own max-width for space. Hidden below
   1180px — there's no room for it once the page content plus its margins
   gets that close to the viewport edge. */
.spy-rail {
  position: fixed;
  right: 22px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 9px;
  z-index: 40;
}
.spy-rail .spy-item { display: flex; align-items: center; gap: 8px; cursor: pointer; justify-content: flex-end; }
.spy-rail .spy-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--border); flex-shrink: 0; transition: background 0.15s, transform 0.15s; }
.spy-rail .spy-item.active .spy-dot { background: var(--color-accent); transform: scale(1.5); }
.spy-rail .spy-label {
  font-family: var(--font-family-mono);
  font-size: 10px;
  color: var(--muted);
  opacity: 0;
  white-space: nowrap;
  transition: opacity 0.15s;
}
.spy-rail .spy-item.active .spy-label { opacity: 1; color: var(--color-primary); font-weight: 700; }
@media (max-width: 1180px) {
  .spy-rail { display: none; }
}
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
  .debate-vs .vs-badge { display: none; }
}

@media (max-width: 520px) {
  .scenario-tabs .tabs { flex-direction: column; }
}
```
