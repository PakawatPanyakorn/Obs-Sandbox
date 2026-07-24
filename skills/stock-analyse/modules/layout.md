# Stock Analysis — HTML Layout & Section Templates

All sections sit inside `<div class="page">`, in the order below. The 16 sections themselves (their content and data bindings) are the same regardless of which layout-factory archetype was picked; what changes per report is the **structural blend** in Part 1 below: container width, grid module, spacing rhythm, masthead/hero treatment, and one signature structural move drawn from the selected archetype.

**Card discipline (baseline for every report, independent of layout family):** `.tldr` and `.verdict` are the only two boxed/shadowed treatments a report gets — they're the report's bookend "pull-quote" moments. Every other section uses the flat/tabular components from `html-theme.md`'s "Flat / Tabular Components" block instead of stacking `.card`/`.stat-card`/`.scenario-card`/`.debate-card` boxes: `.report-table` for comparable rows (financial metrics, scenarios, rated items), `.split-cols` for paired text (story/bet, opportunity/why-we-win, growth/risks, optimist/pessimist), `.item-list` for icon rows (Competitive Edge, and the two Growth/Risk columns), `.exhibit-visual` for the chart frame in Revenue Mix, and a bare `.subhead` for the Timeline label. A report that boxes every section in a shadowed card, regardless of which layout was picked, is the anti-pattern this baseline exists to prevent — see `ruleset.md`'s "Card overuse" rule.

---

## Part 1 — Structural Blend (Selected Layout Archetype)

`style-selection.md` picked one layout-factory preset and noted its `family`. Read `~/.claude/skills/layout-factory/layouts/<selected-layout>.html` for its JSON (`grid.columns`, `grid.gutter`, `grid.maxWidth`, `grid.marginInline`, `spacing.scale`, `spacing.sectionGap`) and `~/.claude/skills/layout-factory/layouts/<selected-layout>.md` for its **Region / Component Guidance** and **Content-Type Notes** (use the `cardOrListHeavy` notes — that's the closest match to this report's shape).

### Structural token block

Inject alongside (never inside) the theme-factory `:root` block from `html-theme.md` — separate namespace, per `apply-mode-html-implementation.md`'s coexistence rule:

```css
/* Layout: <selected-layout> - applied by obs-layout-factory */
:root {
  --layout-columns: <from grid.columns>;
  --layout-gutter: <from grid.gutter>;
  --layout-max-width: <from grid.maxWidth>;
  --layout-margin-inline: <from grid.marginInline>;
  --layout-space-2: <spacing.scale[1]>;
  --layout-space-4: <spacing.scale[3]>;
  --layout-space-6: <spacing.scale[5]>;
  --layout-section-gap: <spacing.sectionGap or spacing.scale[6]>;
}
```

Apply `--layout-max-width` to `.page` (replacing the 900px default in `html-theme.md`) and `--layout-section-gap` to `.section { margin-bottom: ... }`. Add `data-layout="<selected-layout>"` on `<body>`.

### Blend pattern by family

Pick the block matching the selected layout's `family`. Apply it on top of the existing 16 sections — don't remove or reorder sections, just adjust how they're grouped, captioned, and spaced.

**`data-dense-report`** (e.g. `data-dense-report-grid`, `marginalia-annotated`, `tufte-sidenote`)
- This family is where the report-table/split-cols/item-list baseline matters most — lean into it fully rather than the minimum. Add a quiet masthead identity band as the very first element inside `.page` (report name · ticker · series label, small mono uppercase, hairline border-bottom) and give every `.section` a hairline `border-top` (instead of bare margin) so the page reads as a numbered stream, not a scroll of loosely-spaced blocks.
- Add a one-line mono caption above every major exhibit — not just three — using a colored `FIG. NN` prefix: `<div class="fig-caption"><span class="fig-num">FIG. 01</span>What this exhibit shows.</div>`. Number sequentially through the report across all of: Financial Snapshot, Revenue Mix, Hidden Catalyst stats, Analyst Scorecard, Growth & Risks, Overall Scenario Analysis, and Wall Street Consensus. Narrative-only sections (Simple Story, Business Model, Hidden Catalyst opportunity/wins, Competitive Edge, Investor Debate, Verdict) stay caption-free — they're argument, not exhibits.
- Give the TL;DR box the archetype's one allowed pull-quote treatment (per its doc) if it has one — e.g. bumping its shadow to `--shadow-lg` instead of the default `--shadow-md`.

**`editorial-narrative`** (e.g. `magazine-well`, `single-column-editorial`, `masthead-feature-river`, `timeline-river`, `cover-and-contents`)
- Pick ONE section to act as the dominant lead — Hidden Catalyst Deep Dive is the natural choice (it's already the longest, most-researched section); occasionally Bottom Line Verdict if the catalyst section came back thin.
- Give the lead section a larger `.section-title` (add 2-3px) and, if the archetype uses pull quotes, pull one sentence from it into a `<blockquote>` styled per `html-theme.md`'s verdict treatment (surface-tinted, hero shadow).
- Quiet the other sections slightly by comparison: drop their card `box-shadow` to `--shadow-sm` even where they'd default to `--shadow-md`, and don't give them oversized captions.

**`grid-discipline`** (e.g. `swiss-international-grid`, `bauhaus-geometry`, `bauhaus-konstrukt`, `bento-mosaic`, `two-column-academic`, `asymmetric-split`, `card-catalogue-index`)
- Snap `.split-cols` and `.report-table` gaps/gutters to `--layout-gutter` and the archetype's declared column span for that region — no ad hoc gap values outside the injected spacing scale.
- Flush-left every `.section-title`, `.split-cols h3`, and `.report-table th` (already default; just don't center anything).
- If the archetype is `asymmetric-split`: move the Footer/Sources section into a persistent text-only rail beside the main body (8:4 ratio) instead of stacking it at the bottom — rail entries are plain hairline-divided text, matching the `.item-list` convention already used elsewhere in the report.

**`dashboard-legitimate`** (`dashboard-with-rail` — rare pick; `style-selection.md` disqualifies it by default for this static content, only chosen when the request explicitly wants that feel)
- Confine the TL;DR box and Financial Snapshot's report-table into a persistent left rail (`position: sticky; top: 20px`) at `--layout-columns` fraction ~1/4 width; the rest of the sections (business story, catalyst, competitive edge, debate, verdict) run in the remaining body column.
- Everything inside the rail keeps its existing card markup — only the container becomes sticky/narrow, not the components themselves.

### Responsive grid behaviour

| Window width | `.split-cols` | `.report-table` |
|---|---|---|
| > 760 px | 2 columns, hairline vertical divider | Full table, normal layout |
| ≤ 760 px | 1 column, divider flips to a horizontal hairline (`border-top` instead of `border-left`) | Wrapped in `.report-table-wrap` (`overflow-x: auto`) so it scrolls horizontally instead of breaking |

The donut chart (`donut-wrap`) stacks vertically below 520 px. If any section still uses the boxed `.grid-2`/`.grid-3`/`.stat-grid`/`.scenario-grid`/`.debate-grid` components (rare — see the card-discipline note above), they follow the older 3-column → 2-column → 1-column collapse at 760px/520px. If the selected layout's JSON declares its own `grid.breakpoints`, use those column counts instead — but keep the same two breakpoint widths (760px, 520px) so the rest of the CSS doesn't need per-report media query rewrites.

### Page Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TICKER — Stock Analysis · MonYY</title>
  <!-- Google Fonts (copied from the selected theme-factory preset, per html-theme.md Part 1) -->
  <style>
    /* Theme :root block (html-theme.md Part 1) */
    /* Layout :root block (this file, Part 1) */
    /* Component CSS (html-theme.md Part 2) */

    /* Responsive layout — REQUIRED in every report */
    @media (max-width: 760px) {
      body { padding: 12px; }
      .grid-2,
      .debate-grid,
      .split-cols {
        grid-template-columns: 1fr;
      }
      .split-cols > div + div {
        border-left: none;
        padding-left: 0;
        border-top: 1px solid var(--border);
        padding-top: 20px;
      }
      .grid-3,
      .stat-grid,
      .scenario-grid {
        grid-template-columns: 1fr 1fr;
      }
      .hero { padding: 24px 20px; }
      .hero-name { font-size: 22px; }
    }

    @media (max-width: 520px) {
      .grid-3,
      .stat-grid,
      .scenario-grid {
        grid-template-columns: 1fr;
      }
      .donut-wrap {
        flex-direction: column;
        align-items: flex-start;
      }
    }
  </style>
</head>
<body data-layout="<selected-layout>">
<div class="page">

  <!-- Sections 1–16 in order below, blended per the family pattern in Part 1 -->

</div>
<script>
  /* IntersectionObserver for animated segment bars — paste at end of file */
</script>
</body>
</html>
```

---

## Section 1 · Hero Banner

Place as the **first child** inside `<div class="page">`.

```html
<div class="hero">
  <div class="hero-ticker">EXCHANGE: TICKER &nbsp;|&nbsp; Stock Analysis &nbsp;|&nbsp; Month YYYY</div>
  <div class="hero-name">Full Company Name</div>
  <div class="hero-tagline">One sentence explaining the company to a 10-year-old — no jargon.</div>
  <div class="hero-pills">
    <span class="pill pill-blue">Sector Tag</span>
    <span class="pill pill-green">Profitable</span>  <!-- or pill-yellow for growing/pre-profit -->
    <span class="pill pill-yellow">Valuation Risk</span>  <!-- or pill-red for serious risk -->
  </div>
</div>
```

**Pill color guide:** sector → `pill-blue`, growth stage → `pill-green` (profitable) / `pill-yellow` (growing / pre-profit), key risk → `pill-red` (severe) / `pill-yellow` (moderate).

---

## Section 2 · TL;DR Box

Place immediately after the hero. Uses `+` / `!` / `-` / `►` prefix symbols.

```html
<div class="tldr">
  <h2>TL;DR</h2>
  <div class="tldr-item">
    <span class="tldr-sym" style="color:var(--green)">+</span>
    <span>What the company does — one plain-English line.</span>
  </div>
  <div class="tldr-item">
    <span class="tldr-sym" style="color:var(--yellow)">!</span>
    <span>The key thing happening right now — pivot, problem, or opportunity.</span>
  </div>
  <div class="tldr-item">
    <span class="tldr-sym" style="color:var(--accent)">►</span>
    <span>The hidden or underreported catalyst most investors are not talking about.</span>
  </div>
  <div class="tldr-item">
    <span class="tldr-sym" style="color:var(--red)">-</span>
    <span>The main risk in plain language.</span>
  </div>
  <div class="tldr-item">
    <span class="tldr-sym" style="color:var(--green)">+</span>
    <span>Verdict: analyst average target vs. current price. Next binary event to watch.</span>
  </div>
</div>
```

---

## Section 3 · Financial Snapshot

A `.report-table` exhibit: Metric | Value | Detail. Minimum 9 rows. Color-code the Value cell: green = positive/growing, red = negative/loss, yellow = mixed.

```html
<div class="section">
  <div class="section-title">Financial Snapshot</div>
  <div class="report-table-wrap">
    <table class="report-table">
      <thead>
        <tr><th>Metric</th><th>Value</th><th>Detail</th></tr>
      </thead>
      <tbody>
        <tr><td class="row-label">Stock Price</td><td class="mono">$XX.XX</td><td>As of Mon YYYY</td></tr>
        <tr><td class="row-label">Market Cap</td><td class="mono">$XXB</td><td>—</td></tr>
        <tr><td class="row-label">Revenue (TTM)</td><td class="mono val-green">$XXB</td><td>+XX% YoY</td></tr>
        <!-- Continue: Net Income, EPS, Gross Margin, Forward Guidance, Analyst Target, Next Event -->
      </tbody>
    </table>
  </div>
</div>
```

---

## Section 4 · Revenue Breakdown Chart

`[MODEL ESTIMATE]` tag on section title if breakdown is estimated.

```html
<div class="section">
  <div class="section-title">Revenue Mix <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[MODEL ESTIMATE]</span></div>
  <div class="exhibit-visual">

    <!-- Donut SVG + legend side by side -->
    <div class="donut-wrap">
      <svg width="200" height="200" viewBox="0 0 200 200">
        <!-- Each segment: stroke-dasharray="<seg_len> 440" stroke-dashoffset="<offset>" -->
        <circle cx="100" cy="100" r="70" fill="none" stroke="var(--border)" stroke-width="28"/>
        <circle cx="100" cy="100" r="70" fill="none" stroke="var(--color-primary)" stroke-width="28"
                stroke-dasharray="220 440" stroke-dashoffset="0" stroke-linecap="butt"/>
        <!-- repeat per segment, incrementing offset by previous segment lengths; cycle through
             var(--color-primary), var(--color-secondary), var(--color-accent), var(--color-success), var(--color-warning) -->
        <text x="100" y="104" text-anchor="middle" font-family="var(--font-family-display)" font-size="13" font-weight="700" fill="var(--color-text)">Revenue</text>
      </svg>
      <div class="donut-legend">
        <div class="legend-row">
          <div class="legend-dot" style="background:var(--color-primary)"></div>
          <span>Segment Name</span>
          <span class="legend-pct">50%</span>
        </div>
        <!-- repeat per segment -->
      </div>
    </div>

    <!-- Estimated mix note (if applicable) -->
    <p style="font-size:12px;color:var(--muted);margin:14px 0 20px 0">Estimated mix based on [source]. Exact breakdown not publicly disclosed.</p>

    <!-- Segment bars: current % vs projected % in 2 years -->
    <div class="seg-row">
      <div class="seg-label"><span>Segment Name</span><span style="font-family:var(--font-family-mono)">50% → 60%</span></div>
      <div class="seg-track">
        <div class="seg-fill" style="width:50%;background:var(--color-primary)"></div>
      </div>
      <div class="seg-proj js-proj-bar" data-target="60" style="width:0%;background:var(--color-primary);margin-top:3px;height:4px;border-radius:2px"></div>
      <div class="seg-note">Brief annotation explaining expected shift.</div>
    </div>
    <!-- repeat per segment, matching the same color used for that segment's donut wedge -->

  </div>
</div>
```

IntersectionObserver JS (add to bottom of file) animates `.js-proj-bar` elements to their `data-target` width on scroll.

---

## Section 5 · What Does This Company Actually Do?

Two flat text columns divided by a hairline rule — no card boxes.

```html
<div class="section">
  <div class="section-title">What Does This Company Actually Do?</div>
  <div class="split-cols">
    <div>
      <h3>The Simple Story</h3>
      <p>Explain the business in one paragraph. Zero jargon. Use a simple analogy (e.g. "like Netflix but for your health"). Write as if explaining to a 10-year-old.</p>
    </div>
    <div>
      <h3>The Big Bet Right Now</h3>
      <p>What is the company betting on this year? What would need to go right for it to pay off?</p>
    </div>
  </div>
</div>
```

---

## Section 6 · Business Model

Two flat text columns divided by a hairline rule.

```html
<div class="section">
  <div class="section-title">Business Model</div>
  <div class="split-cols">
    <div>
      <h3>How They Make Money</h3>
      <ul>
        <li>Revenue stream 1 — brief description</li>
        <li>Revenue stream 2</li>
      </ul>
    </div>
    <div>
      <h3>Why the Model Is Clever</h3>
      <ul>
        <li>Structural advantage 1</li>
        <li>Structural advantage 2</li>
      </ul>
    </div>
  </div>
</div>
```

---

## Section 7 · Hidden Catalyst Deep Dive

This is the longest and most researched section. If no catalyst was found, write: *"Insufficient public data found to identify a clear underreported catalyst. A follow-up search is recommended."* — do not pad with generic commentary.

If the `editorial-narrative` blend pattern (Part 1) picked this section as the lead, apply its larger section-title and pull-quote treatment here.

Structure:

```html
<div class="section">
  <div class="section-title">Hidden Catalyst Deep Dive</div>

  <!-- Two flat text columns: what it is + why this company wins -->
  <div class="split-cols" style="margin-bottom:24px">
    <div>
      <h3>The Opportunity</h3>
      <p>Specifics: what exactly, how big, what the timeline looks like.</p>
    </div>
    <div>
      <h3>Why This Company Wins</h3>
      <p>Why this specific company has an advantage over competitors for this catalyst.</p>
    </div>
  </div>

  <!-- Report table: TAM, key date/event, company readiness -->
  <div class="report-table-wrap" style="margin-bottom:24px">
    <table class="report-table">
      <thead>
        <tr><th>Metric</th><th>Value</th></tr>
      </thead>
      <tbody>
        <tr><td class="row-label">TAM / Market Size</td><td class="mono">$XXB</td></tr>
        <tr><td class="row-label">Key Date / Event</td><td class="mono">Mon YYYY</td></tr>
        <tr><td class="row-label">Company Readiness</td><td class="mono">High / Medium / Early</td></tr>
      </tbody>
    </table>
  </div>

  <!-- Vertical timeline: past milestones → present → future inflection — bare subhead, no card -->
  <div style="margin-bottom:24px">
    <div class="subhead">Timeline</div>
    <div class="timeline">
      <div class="timeline-item">
        <div class="timeline-dot past"></div>
        <div class="timeline-date">Mon YYYY</div>
        <div class="timeline-event">Past milestone description.</div>
      </div>
      <div class="timeline-item">
        <div class="timeline-dot present"></div>
        <div class="timeline-date">Now</div>
        <div class="timeline-event">Current moment — what is happening today.</div>
      </div>
      <div class="timeline-item">
        <div class="timeline-dot future"></div>
        <div class="timeline-date">Mon YYYY</div>
        <div class="timeline-event">Future inflection point — the binary event.</div>
      </div>
    </div>
  </div>

  <!-- Catalyst-specific scenario table — EDITORIAL OPINION tag on title -->
  <div class="section-title" style="margin-top:20px">Catalyst Scenarios <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="report-table-wrap">
    <table class="report-table">
      <thead>
        <tr><th>Outcome</th><th>Probability</th><th>Stock Impact</th><th>Conditions</th></tr>
      </thead>
      <tbody>
        <tr>
          <td class="row-label" style="color:var(--color-success)">Positive</td>
          <td class="mono val-green">XX%</td>
          <td class="mono val-green">+XX%</td>
          <td><ul><li>Condition 1</li><li>Condition 2</li></ul></td>
        </tr>
        <tr>
          <td class="row-label" style="color:var(--color-warning)">Mixed</td>
          <td class="mono val-yellow">XX%</td>
          <td class="mono val-yellow">+X% to -X%</td>
          <td><ul><li>Condition 1</li></ul></td>
        </tr>
        <tr>
          <td class="row-label" style="color:var(--color-error)">Negative</td>
          <td class="mono val-red">XX%</td>
          <td class="mono val-red">-XX%</td>
          <td><ul><li>Condition 1</li></ul></td>
        </tr>
      </tbody>
    </table>
  </div>

</div>
```

---

## Section 8 · Competitive Edge

Four to six item-rows, hairline-divided — no wrapping card. Include at least one underappreciated advantage.

```html
<div class="section">
  <div class="section-title">Competitive Edge</div>
  <div class="item-list">
    <div class="item-row">
      <div class="item-icon">★</div>
      <div>
        <div class="item-title">Advantage Title</div>
        <div class="item-desc">Description of the advantage and why it matters.</div>
      </div>
    </div>
    <!-- repeat; use ★ for strength, → for momentum, ⚠ for underappreciated -->
  </div>
</div>
```

---

## Section 9 · Analyst Scorecard

Seven metrics on 0–10 scale, no wrapping card — the colored bars already carry enough visual weight. High score always means good/strong (see ruleset.md for naming constraint).

```html
<div class="section">
  <div class="section-title">Analyst Scorecard</div>
  <div>
    <div class="meter-row">
      <div class="meter-label"><span>Business Model Strength</span><span>7 / 10</span></div>
      <div class="meter-track"><div class="meter-fill green" style="width:70%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Revenue Growth</span><span>8 / 10</span></div>
      <div class="meter-track"><div class="meter-fill green" style="width:80%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Profitability</span><span>5 / 10</span></div>
      <div class="meter-track"><div class="meter-fill yellow" style="width:50%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Competitive Moat</span><span>8 / 10</span></div>
      <div class="meter-track"><div class="meter-fill green" style="width:80%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Regulatory Safety</span><span>4 / 10</span></div>
      <div class="meter-track"><div class="meter-fill red" style="width:40%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Management Execution</span><span>7 / 10</span></div>
      <div class="meter-track"><div class="meter-fill green" style="width:70%"></div></div>
    </div>
    <div class="meter-row">
      <div class="meter-label"><span>Long-Term Potential</span><span>8 / 10</span></div>
      <div class="meter-track"><div class="meter-fill green" style="width:80%"></div></div>
    </div>
  </div>
</div>
```

---

## Section 10 · Current Situation — Growth & Risks

Two flat text columns divided by a hairline rule. Left = growth drivers (green header). Right = risks (red header). Only include ACTIVE or REDUCED risks — never RESOLVED.

```html
<div class="section">
  <div class="section-title">Current Situation</div>
  <div class="split-cols">
    <div>
      <h3 style="color:var(--color-success)">Growth Drivers</h3>
      <div class="item-list">
        <div class="item-row">
          <div class="item-icon" style="color:var(--green)">→</div>
          <div>
            <div class="item-title">Driver Title</div>
            <div class="item-desc">Description of why this drives growth.</div>
          </div>
        </div>
        <!-- 3–4 drivers total -->
      </div>
    </div>
    <div>
      <h3 style="color:var(--color-error)">Risks</h3>
      <div class="item-list">
        <div class="item-row">
          <div class="item-icon" style="color:var(--red)">⚠</div>  <!-- red for ACTIVE, yellow for REDUCED -->
          <div>
            <div class="item-title">Risk Title [ACTIVE RISK]</div>
            <div class="item-desc">Plain-English description of the risk.</div>
            <div class="item-meta">Active as of Jun 2026 · Source: Reuters</div>
          </div>
        </div>
        <!-- 3–4 risks total; each must show status + last-verified date + source -->
      </div>
    </div>
  </div>
</div>
```

---

## Section 11 · Overall Scenario Analysis

`[EDITORIAL OPINION]` tag on section title. A `.report-table`: Case | Probability | Price Target | Key Conditions — Bull / Base / Bear rows. All use $ price targets (not %).

```html
<div class="section">
  <div class="section-title">Scenario Analysis <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="report-table-wrap">
    <table class="report-table">
      <thead>
        <tr><th>Case</th><th>Probability</th><th>Price Target</th><th>Key Conditions</th></tr>
      </thead>
      <tbody>
        <tr>
          <td class="row-label" style="color:var(--color-success)">Bull</td>
          <td class="mono val-green">XX%</td>
          <td class="mono val-green">$XX–$XX</td>
          <td><ul>
            <li>Condition for bull case 1</li>
            <li>Condition 2</li>
            <li>Condition 3</li>
            <li>Condition 4</li>
            <li>Condition 5</li>
          </ul></td>
        </tr>
        <tr>
          <td class="row-label" style="color:var(--color-warning)">Base</td>
          <td class="mono val-yellow">XX%</td>
          <td class="mono val-yellow">$XX–$XX</td>
          <td><ul><!-- 5–6 conditions --></ul></td>
        </tr>
        <tr>
          <td class="row-label" style="color:var(--color-error)">Bear</td>
          <td class="mono val-red">XX%</td>
          <td class="mono val-red">$XX–$XX</td>
          <td><ul><!-- 5–6 conditions --></ul></td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
```

---

## Section 12 · Investor Debate

`[EDITORIAL OPINION]` tag. Five bullets each side, as flat text columns divided by a hairline rule — no card boxes. Honest representation of both views — no bias.

```html
<div class="section">
  <div class="section-title">Investor Debate <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="split-cols">
    <div>
      <h3 style="color:var(--color-success)">The Optimist Sees…</h3>
      <ul>
        <li>Bull point 1</li>
        <li>Bull point 2</li>
        <li>Bull point 3</li>
        <li>Bull point 4</li>
        <li>Bull point 5</li>
      </ul>
    </div>
    <div>
      <h3 style="color:var(--color-error)">The Pessimist Sees…</h3>
      <ul>
        <li>Bear point 1</li>
        <li>Bear point 2</li>
        <li>Bear point 3</li>
        <li>Bear point 4</li>
        <li>Bear point 5</li>
      </ul>
    </div>
  </div>
</div>
```

---

## Section 13 · Bottom Line Verdict

`[EDITORIAL OPINION]` tag. Three paragraphs: analogy, green case, bear case + time horizon.

```html
<div class="section">
  <div class="section-title">Bottom Line Verdict <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="verdict">
    <div class="verdict-title">The Verdict</div>
    <p>A simple analogy that captures the company's situation (e.g. "Like a surfer paddling into position — the wave exists, but timing matters.").</p>
    <p>Why the long-term story is believable — the green case in plain language, referencing the key growth driver and hidden catalyst.</p>
    <p>Why the near-term pain is real — the bear case honestly, ending with a recommended time horizon for different investor types.</p>
  </div>
</div>
```

---

## Section 14 · Wall Street Consensus

`[ANALYST ESTIMATE]` tag on section title. A `.report-table`: Metric | Value | Detail.

```html
<div class="section">
  <div class="section-title">Wall Street Consensus <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[ANALYST ESTIMATE]</span></div>
  <div class="report-table-wrap">
    <table class="report-table">
      <thead>
        <tr><th>Metric</th><th>Value</th><th>Detail</th></tr>
      </thead>
      <tbody>
        <tr><td class="row-label">Consensus Rating</td><td class="mono">Buy</td><td>X Buy · X Hold · X Sell</td></tr>
        <tr><td class="row-label">Avg. Price Target</td><td class="mono val-green">$XX.XX</td><td>vs. current $XX.XX (+XX%)</td></tr>
        <tr><td class="row-label">Additional Signal</td><td class="mono">XX%</td><td>Short interest / Insider buying / Fair value estimate</td></tr>
      </tbody>
    </table>
  </div>
</div>
```

---

## Section 15 · Footer

```html
<div class="section" style="border-top:1px solid var(--border);padding-top:20px;margin-top:32px">
  <div style="font-family:var(--font-family-display);font-size:11px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--muted);margin-bottom:10px">Sources</div>
  <ul style="font-size:13px;line-height:1.8;padding-left:18px;color:var(--muted)">
    <li><a href="URL" style="color:var(--color-primary)">Source label — publication name</a></li>
    <!-- repeat for every URL used -->
  </ul>
  <p style="font-size:12px;color:var(--muted);margin-top:16px">This is not financial advice. For informational purposes only. Analysis produced: Month YYYY.</p>
</div>
```

(If the `grid-discipline` blend pattern in Part 1 applies and the selected archetype is `asymmetric-split`, this section moves into the rail instead of staying here — see Part 1.)

---

## IntersectionObserver JS (Animated Segment Bars)

Paste before `</body>`:

```html
<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const bar = entry.target;
        const target = bar.dataset.target;
        bar.style.transition = 'width 0.9s cubic-bezier(0.16,1,0.3,1)';
        bar.style.width = target + '%';
        observer.unobserve(bar);
      }
    });
  }, { threshold: 0.3 });
  document.querySelectorAll('.js-proj-bar').forEach(el => observer.observe(el));
</script>
```
