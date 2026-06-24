# Stock Analysis — HTML Theme (Wisdom)

## Google Fonts — Add to `<head>` Before `<style>`

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700;900&family=EB+Garamond:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Courier+Prime:wght@400;700&display=swap" rel="stylesheet">
```

---

## CSS Custom Properties — Copy Exactly

```css
:root {
  --color-primary:         #1E3B6F;
  --color-primary-light:   #C8D8EC;
  --color-secondary:       #8B4513;
  --color-accent:          #B8860B;
  --color-bg:              #F4EFE2;
  --color-surface:         #EBE4D1;
  --color-surface-alt:     #DDD5BC;
  --color-text:            #1C1812;
  --color-text-muted:      #6E5E48;
  --color-text-on-primary: #F4EFE2;
  --color-border:          #C4B59A;
  --color-success:         #3D6E3A;
  --color-warning:         #B07820;
  --color-error:           #8B2020;

  --font-family:         'EB Garamond', Georgia, serif;
  --font-family-display: 'Cinzel', 'Times New Roman', serif;
  --font-family-mono:    'Courier Prime', 'Courier New', monospace;
  --font-size-base:      16px;
  --font-weight-heading: 700;
  --line-height:         1.65;
  --radius-card:         10px;
  --shadow-sm:           0 1px 3px rgba(28,24,18,0.08);
  --shadow-md:           0 4px 12px rgba(28,24,18,0.12);
  --shadow-lg:           0 8px 24px rgba(28,24,18,0.16);

  /* Shorthand aliases */
  --bg:     var(--color-bg);
  --card:   var(--color-surface);
  --card2:  var(--color-surface-alt);
  --border: var(--color-border);
  --accent: var(--color-primary);
  --green:  var(--color-success);
  --red:    var(--color-error);
  --yellow: var(--color-warning);
  --text:   var(--color-text);
  --muted:  var(--color-text-muted);
  --radius: var(--radius-card);
}
```

---

## Body & Page Container

```css
body {
  background-color: #F4EFE2;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='0.05'/%3E%3C/svg%3E");
  background-size: 300px 300px;
  background-repeat: repeat;
  font-family: var(--font-family);
  color: var(--text);
  margin: 0;
  padding: 20px;
}

.page {
  max-width: 900px;
  margin: 0 auto;
}
```

---

## Hero Banner

```css
.hero {
  background: linear-gradient(135deg, #1E3B6F 0%, #2C5298 60%, #1A3260 100%);
  border-top: 3px solid #C9A84C;
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  color: var(--color-text-on-primary);
  padding: 36px 32px;
  margin-bottom: 24px;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: '';
  position: absolute; top: -60px; right: -60px;
  width: 220px; height: 220px;
  background: radial-gradient(circle, rgba(200,216,236,0.12) 0%, transparent 70%);
  border-radius: 50%;
}
.hero-ticker  { font-size: 11px; font-weight: 700; letter-spacing: 2.5px; color: rgba(244,239,226,0.65); text-transform: uppercase; margin-bottom: 6px; font-family: var(--font-family-display); }
.hero-name    { font-size: 28px; font-weight: 700; margin-bottom: 8px; color: #F4EFE2; font-family: var(--font-family-display); letter-spacing: 0.03em; }
.hero-tagline { font-size: 15px; color: rgba(244,239,226,0.78); max-width: 540px; margin-bottom: 20px; font-style: italic; }
.hero-pills   { display: flex; flex-wrap: wrap; gap: 8px; }
.pill         { padding: 4px 14px; border-radius: 50px; font-size: 11px; font-weight: 600; border: 1px solid; letter-spacing: 0.04em; font-family: var(--font-family-display); }
.pill-blue    { background: rgba(200,216,236,.18); border-color: rgba(200,216,236,.45); color: #C8D8EC; }
.pill-green   { background: rgba(61,110,58,.25);   border-color: rgba(61,110,58,.6);    color: #a8d5a4; }
.pill-red     { background: rgba(139,32,32,.25);   border-color: rgba(139,32,32,.6);    color: #e8a4a4; }
.pill-yellow  { background: rgba(176,120,32,.25);  border-color: rgba(176,120,32,.6);   color: #e8cc90; }
```

---

## Section & Card Structure

```css
.section       { margin-bottom: 32px; }
.section-title { font-family: var(--font-family-display); font-size: 13px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: var(--color-primary); margin-bottom: 14px; }

.card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 20px 22px;
  margin-bottom: 14px;
}
.card h3 { font-family: var(--font-family-display); font-size: 13px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; color: var(--color-primary); margin: 0 0 10px 0; }

.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
```

---

## Stat Grid

```css
.stat-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; }

.stat-card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 16px 18px;
}
.stat-label      { font-family: var(--font-family-display); font-size: 11px; font-weight: 700; letter-spacing: 1.2px; text-transform: uppercase; color: var(--color-primary); margin-bottom: 6px; }
.mini-stat-label { font-family: var(--font-family-display); font-size: 11px; font-weight: 700; letter-spacing: 1.2px; text-transform: uppercase; color: var(--color-primary); margin-bottom: 4px; }
.stat-value      { font-family: var(--font-family-display); font-size: 22px; font-weight: 700; color: var(--color-text); }
.stat-sub        { font-family: var(--font-family-mono); font-size: 12px; color: var(--muted); margin-top: 4px; }
.val-green       { color: var(--color-success); }
.val-red         { color: var(--color-error); }
.val-yellow      { color: var(--color-warning); }
```

---

## TL;DR Box

```css
.tldr {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-md);
  padding: 22px 24px;
  margin-bottom: 28px;
}
.tldr h2 { font-family: var(--font-family-display); font-size: 13px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: var(--color-primary); margin: 0 0 14px 0; }
.tldr-item { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 10px; font-size: 15px; line-height: 1.55; }
/* Symbol spans — always 16px wide so text column aligns regardless of symbol width */
.tldr-sym { width: 16px; text-align: center; flex-shrink: 0; font-family: var(--font-family-mono); font-weight: 800; }
```

---

## Analyst Scorecard Meters

```css
.meter-row   { margin-bottom: 14px; }
.meter-label { display: flex; justify-content: space-between; font-size: 13px; margin-bottom: 5px; font-family: var(--font-family-display); }
.meter-label span:last-child { font-weight: 700; font-family: var(--font-family-mono); }
.meter-track { background: var(--card2); border-radius: 6px; height: 10px; overflow: hidden; }
.meter-fill  { height: 100%; border-radius: 6px; }
.meter-fill.green  { background: var(--green); }
.meter-fill.yellow { background: var(--yellow); }
.meter-fill.red    { background: var(--red); }
```

---

## Scenario Cards

```css
.scenario-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
.scenario-card {
  background: var(--card);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  padding: 18px 20px;
}
.scenario-card h3 { font-family: var(--font-family-display); font-size: 13px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; margin: 0 0 6px 0; }
.scenario-prob    { font-family: var(--font-family-mono); font-size: 20px; font-weight: 700; margin-bottom: 4px; }
.scenario-target  { font-family: var(--font-family-mono); font-size: 13px; color: var(--muted); margin-bottom: 12px; }
.scenario-card ul { margin: 0; padding-left: 16px; font-size: 14px; line-height: 1.6; }
.scenario-bull h3 { color: var(--color-success); }
.scenario-base h3 { color: var(--color-warning); }
.scenario-bear h3 { color: var(--color-error); }
```

---

## Timeline Component

```css
.timeline { position: relative; padding-left: 28px; }
.timeline::before { content: ''; position: absolute; left: 7px; top: 6px; bottom: 6px; width: 2px; background: var(--border); }
.timeline-item { position: relative; margin-bottom: 20px; }
.timeline-dot  { position: absolute; left: -25px; top: 4px; width: 12px; height: 12px; border-radius: 50%; border: 2px solid var(--border); background: var(--card2); }
.timeline-dot.past    { background: var(--color-text-muted); border-color: var(--color-text-muted); }
.timeline-dot.present { background: var(--color-primary); border-color: var(--color-primary); width: 14px; height: 14px; left: -26px; }
.timeline-dot.future  { background: var(--card); border-color: var(--color-accent); }
.timeline-date { font-family: var(--font-family-mono); font-size: 11px; color: var(--muted); margin-bottom: 2px; }
.timeline-event { font-size: 14px; line-height: 1.5; }
```

---

## Verdict / Bottom Line Card

```css
.verdict {
  background: linear-gradient(135deg, var(--color-surface) 0%, var(--color-surface-alt) 100%);
  border-radius: var(--radius);
  border-top: 3px solid var(--color-accent);
  box-shadow: var(--shadow-md);
  padding: 28px 30px;
}
.verdict-title { font-family: var(--font-family-display); font-size: 14px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: var(--color-primary); margin-bottom: 16px; }
.verdict p { font-size: 16px; line-height: 1.7; margin-bottom: 14px; }
.verdict p:last-child { margin-bottom: 0; }
```

---

## Icon Rows (Competitive Edge, Growth/Risk cards)

```css
.item-row { display: flex; align-items: flex-start; gap: 12px; margin-bottom: 14px; }
.item-icon { width: 20px; flex-shrink: 0; text-align: center; font-size: 14px; margin-top: 1px; }
.item-title { font-family: var(--font-family-display); font-size: 12px; font-weight: 700; letter-spacing: 0.5px; text-transform: uppercase; color: var(--color-primary); margin-bottom: 2px; }
.item-desc  { font-size: 14px; line-height: 1.55; }
.item-meta  { font-family: var(--font-family-mono); font-size: 11px; color: var(--muted); margin-top: 3px; }
```

---

## Debate Box

```css
.debate-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.debate-card { background: var(--card); border-radius: var(--radius); border-top: 3px solid var(--color-accent); box-shadow: var(--shadow-sm); padding: 20px 22px; }
.debate-card h3 { font-family: var(--font-family-display); font-size: 13px; font-weight: 700; letter-spacing: 1px; text-transform: uppercase; margin: 0 0 12px 0; }
.debate-card.optimist h3 { color: var(--color-success); }
.debate-card.pessimist h3 { color: var(--color-error); }
.debate-card ul { margin: 0; padding-left: 16px; font-size: 14px; line-height: 1.65; }
.debate-card li { margin-bottom: 6px; }
```

---

## Donut Chart

The SVG donut is 200×200. Center is at cx="100" cy="100". Use `r="70"` for the ring (circumference ≈ 440). Each segment is a `<circle>` with `stroke-dasharray` and `stroke-dashoffset`. Legend sits beside it in a flex row.

```css
.donut-wrap  { display: flex; align-items: center; gap: 28px; flex-wrap: wrap; }
.donut-legend { flex: 1; min-width: 180px; }
.legend-row  { display: flex; align-items: center; gap: 8px; margin-bottom: 8px; font-size: 14px; }
.legend-dot  { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.legend-pct  { font-family: var(--font-family-mono); font-weight: 700; margin-left: auto; font-size: 13px; }
```

Segment bar rows (current vs projected, below the donut):

```css
.seg-row     { margin-bottom: 16px; }
.seg-label   { display: flex; justify-content: space-between; font-size: 13px; margin-bottom: 5px; font-family: var(--font-family-display); font-weight: 700; letter-spacing: 0.5px; }
.seg-track   { background: var(--card2); border-radius: 4px; height: 8px; overflow: hidden; position: relative; }
.seg-fill    { height: 100%; border-radius: 4px; }
.seg-proj    { height: 100%; border-radius: 4px; opacity: 0.45; }
.seg-note    { font-size: 12px; color: var(--muted); margin-top: 4px; }
```
