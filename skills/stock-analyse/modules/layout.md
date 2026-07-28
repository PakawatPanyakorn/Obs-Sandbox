# Stock Analysis — HTML Layout & Section Templates

All sections sit inside `<div class="page">`, in the order below. The 16 sections themselves (their content and data bindings) are the same regardless of which layout-factory archetype was picked; what changes per report is the **structural blend** in Part 1 below: container width, grid module, spacing rhythm, masthead/hero treatment, and one signature structural move drawn from the selected archetype.

**Card discipline (baseline for every report, independent of layout family):** boxed/shadowed treatment is reserved for four moments: `.tldr` and `.verdict` (the report's bookend "pull-quote" moments), `.stat-card` tiles in Financial Snapshot (scannable numeric tiles, not narrative), and `.debate-card` + VS badge in Investor Debate (a genuinely oppositional comparison, not paired narrative). Every other section uses the flat/tabular components from `html-theme.md`'s "Flat / Tabular Components" block instead of stacking `.card`/`.scenario-card` boxes: `.report-table` for comparable rows (Hidden Catalyst stats, Overall Scenario Analysis when not using tabs, Wall Street Consensus), `.split-cols` for paired narrative text (story/bet, opportunity/why-we-win), `.item-list` for icon rows (Competitive Edge), `.severity-list` for stripe-marked rows (Growth Drivers, Risks), `.exhibit-visual` for the chart frame in Revenue Mix, and a bare `.subhead` for the Timeline label. A report that boxes every section in a shadowed card, regardless of which layout was picked, is the anti-pattern this baseline exists to prevent — see `ruleset.md`'s "Card overuse" rule.

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
      .debate-vs .vs-badge { display: none; }
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
      .scenario-tabs .tabs {
        flex-direction: column;
      }
    }
  </style>
</head>
<body data-layout="<selected-layout>">
<nav class="spy-rail" id="spyRail" aria-label="Section navigation"></nav>
<div class="page">

  <!-- Sections 1–16 in order below, blended per the family pattern in Part 1.
       Give each top-level section wrapper a stable id — the scroll-spy rail
       hooks into these exact ids (see "Section Navigation" below):
       hero, tldr, snapshot, mix, story, model, catalyst, edge, scorecard,
       situation, scenario, debate, verdict, wall -->

</div>
<script>
  /* Shared interactive JS — paste before </body>. See "Shared Interactive JS"
     appendix at the end of this file: animated segment bars, scenario tabs,
     donut hover-link, scroll-spy rail, and the Analyst Scorecard radar chart. */
</script>
</body>
</html>
```

### Section Navigation (Scroll-Spy Rail)

Include on every report — it's cheap and this report shape (14 sections, ~1,000+ lines) consistently benefits from a way to jump around instead of pure linear scroll. Placed as a `<nav>` sibling of `.page`, not inside it — `position: fixed`, so DOM position doesn't matter. Lists all 14 section ids with short labels, tracked via `IntersectionObserver` (`root: null`, the viewport), marking the current section active as the reader scrolls and letting them click to jump. Hides below `1180px` viewport width (see `html-theme.md`'s Scroll-Spy Rail component) — there's no room for it once the page content plus its margins gets that close to the viewport edge. See the "Shared Interactive JS" appendix for the build function.

---

## Section 1 · Hero Banner

Place as the **first child** inside `<div class="page">`.

```html
<div class="hero" id="hero">
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
<div class="tldr" id="tldr">
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

A `.stat-grid` of `.stat-card` tiles — one of the report's established boxed-treatment exceptions (see card discipline above). Minimum 9 metrics: Stock Price, Market Cap, Revenue (TTM), Net Income (TTM), EPS (TTM), Gross Margin, Forward Guidance, Analyst Target, Next Event. Tiles read faster than table rows for the handful of headline numbers a reader actually scans for. Color-code `.stat-value`: green = positive/growing, red = negative/loss, yellow = mixed. Keep each `.stat-sub` line short (a date, a %, a one-word qualifier) — it's a caption, not a sentence.

```html
<div class="section" id="snapshot">
  <div class="section-title">Financial Snapshot</div>
  <div class="fig-caption"><span class="fig-num">FIG. 01</span>Core financial metrics as of the most recent quarter and trading session.</div>
  <div class="stat-grid">
    <div class="stat-card"><div class="stat-label">Stock Price</div><div class="stat-value mono">$XX.XX</div><div class="stat-sub">As of Mon YYYY</div></div>
    <div class="stat-card"><div class="stat-label">Market Cap</div><div class="stat-value mono">$XXB</div><div class="stat-sub">—</div></div>
    <div class="stat-card"><div class="stat-label">Revenue (TTM)</div><div class="stat-value mono val-green">$XXB</div><div class="stat-sub">+XX% YoY</div></div>
    <!-- Continue: Net Income, EPS, Gross Margin, Forward Guidance, Analyst Target, Next Event -->
  </div>
</div>
```

If a value doesn't fit `.stat-value`'s default 22px at one line (e.g. a long guidance range or event name), add an inline `style="font-size:15px"` to that one tile rather than shrinking the whole grid.

---

## Section 4 · Revenue Breakdown Chart

`[MODEL ESTIMATE]` tag on section title if breakdown is estimated. The donut and its legend are hover-linked (see "Shared Interactive JS" appendix) — hovering a legend row highlights the matching wedge and dims the rest, so the reader doesn't have to manually match colors. Give each donut segment `<circle>` and each `.legend-row` a matching `data-seg="<slug>"` attribute — that's the only markup change the hover-link needs.

```html
<div class="section" id="mix">
  <div class="section-title">Revenue Mix <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[MODEL ESTIMATE]</span></div>
  <div class="fig-caption"><span class="fig-num">FIG. 02</span>Product-line revenue mix, current vs. two-year projected share. <em>Hover a segment below to trace it through the chart.</em></div>
  <div class="exhibit-visual">

    <!-- Donut SVG + legend side by side -->
    <div class="donut-wrap">
      <svg width="200" height="200" viewBox="0 0 200 200" id="revenueDonut">
        <!-- Each segment: stroke-dasharray="<seg_len> 440" stroke-dashoffset="<offset>" -->
        <circle cx="100" cy="100" r="70" fill="none" stroke="var(--border)" stroke-width="28"/>
        <circle class="seg-hi" data-seg="segment-a" cx="100" cy="100" r="70" fill="none" stroke="var(--color-primary)" stroke-width="28"
                stroke-dasharray="220 440" stroke-dashoffset="0" stroke-linecap="butt"/>
        <!-- repeat per segment, incrementing offset by previous segment lengths, giving each a unique data-seg slug; cycle through
             var(--color-primary), var(--color-secondary), var(--color-accent), var(--color-success), var(--color-warning) -->
        <text x="100" y="104" text-anchor="middle" font-family="var(--font-family-display)" font-size="13" font-weight="700" fill="var(--color-text)">Revenue</text>
      </svg>
      <div class="donut-legend" id="revenueLegend">
        <div class="legend-row" data-seg="segment-a">
          <div class="legend-dot" style="background:var(--color-primary)"></div>
          <span>Segment Name</span>
          <span class="legend-pct">50%</span>
        </div>
        <!-- repeat per segment, same data-seg slug as its donut circle -->
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

Two flat text columns divided by a hairline rule — no card boxes. **Scope boundary:** this section is purely descriptive — what the product is and who buys it. It does NOT preview the forward-looking thesis; that's Section 7's job exclusively. Writing the "big bet"/catalyst narrative here duplicates Section 7 and reads as repetitive (this is a real failure mode, not a hypothetical one — catch it in review).

```html
<div class="section" id="story">
  <div class="section-title">What Does This Company Actually Do?</div>
  <div class="split-cols">
    <div>
      <h3>The Simple Story</h3>
      <p>Explain the business in one paragraph. Zero jargon. Use a simple analogy (e.g. "like Netflix but for your health"). Write as if explaining to a 10-year-old.</p>
    </div>
    <div>
      <h3>Who Actually Buys It</h3>
      <p>Who the actual customer is (consumer, enterprise, a specific industry) and how the sale happens — descriptive, not speculative.</p>
    </div>
  </div>
</div>
```

---

## Section 6 · Business Model

Two flat text columns divided by a hairline rule. **Scope boundary:** this is the mechanics of how money is made and why the model is structurally advantaged — not a restatement of Competitive Edge (Section 8) or the forward-looking catalyst (Section 7). If a product line's future direction matters, name it in one clause and point forward ("see Hidden Catalyst Deep Dive below") rather than re-arguing the thesis here.

```html
<div class="section" id="model">
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

This is the longest and most researched section, and the **exclusive home of the forward-looking thesis** — the "big bet"/catalyst narrative belongs here only, not previewed in Section 5 or re-argued in Section 6 (see their scope-boundary notes above). If no catalyst was found, write: *"Insufficient public data found to identify a clear underreported catalyst. A follow-up search is recommended."* — do not pad with generic commentary.

If the `editorial-narrative` blend pattern (Part 1) picked this section as the lead, apply its larger section-title and pull-quote treatment here.

Structure:

```html
<div class="section" id="catalyst">
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

  <!-- Catalyst-specific scenario data — EDITORIAL OPINION tag on title.
       Decision rule (ruleset.md's "Interaction must earn its click"): count the
       conditions per outcome. 4+ each → interactive tabs (below, Option A).
       2–3 each → static side-by-side .scenario-card row (Option B) — thin
       content doesn't earn a click. Never both; pick one per report. -->
  <div class="section-title" style="margin-top:20px">Catalyst Scenarios <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>

  <!-- Option A — 4+ conditions per outcome: interactive tabs -->
  <div class="scenario-tabs" data-tabgroup="catalyst">
    <div class="tabs">
      <div class="tab positive active" data-tab="positive">Positive <span class="p mono">XX%</span></div>
      <div class="tab mixed" data-tab="mixed">Mixed <span class="p mono">XX%</span></div>
      <div class="tab negative" data-tab="negative">Negative <span class="p mono">XX%</span></div>
    </div>
    <div class="tab-panel show" data-panel="positive">
      <h4 style="color:var(--color-success)">Positive · +XX% Stock Impact</h4>
      <div class="range">XX% probability</div>
      <ul><li>Condition 1</li><li>Condition 2</li><li>Condition 3</li><li>Condition 4</li></ul>
    </div>
    <div class="tab-panel" data-panel="mixed">
      <h4 style="color:var(--color-warning)">Mixed · +X% to -X% Stock Impact</h4>
      <div class="range">XX% probability</div>
      <ul><li>Condition 1</li><li>Condition 2</li><li>Condition 3</li><li>Condition 4</li></ul>
    </div>
    <div class="tab-panel" data-panel="negative">
      <h4 style="color:var(--color-error)">Negative · -XX% Stock Impact</h4>
      <div class="range">XX% probability</div>
      <ul><li>Condition 1</li><li>Condition 2</li><li>Condition 3</li><li>Condition 4</li></ul>
    </div>
  </div>

  <!-- Option B — 2–3 conditions per outcome: static cards, no click needed -->
  <div class="scenario-grid">
    <div class="scenario-card">
      <h3 style="color:var(--color-success)">Positive</h3>
      <div class="scenario-prob" style="color:var(--color-success)">XX%</div>
      <div class="scenario-target">+XX% stock impact</div>
      <ul><li>Condition 1</li><li>Condition 2</li></ul>
    </div>
    <div class="scenario-card">
      <h3 style="color:var(--color-warning)">Mixed</h3>
      <div class="scenario-prob" style="color:var(--color-warning)">XX%</div>
      <div class="scenario-target">+X% to -X% stock impact</div>
      <ul><li>Condition 1</li></ul>
    </div>
    <div class="scenario-card">
      <h3 style="color:var(--color-error)">Negative</h3>
      <div class="scenario-prob" style="color:var(--color-error)">-XX%</div>
      <div class="scenario-target">stock impact</div>
      <ul><li>Condition 1</li></ul>
    </div>
  </div>

</div>
```

---

## Section 8 · Competitive Edge

Four to six item-rows, hairline-divided — no wrapping card. Include at least one underappreciated advantage.

```html
<div class="section" id="edge">
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

Seven metrics on a 0–10 scale, rendered as an interactive filled radar chart, not meter bars — a radar shows the shape of the business at a glance instead of seven disconnected rows. High score always means good/strong (see `ruleset.md` for the naming constraint). No wrapping card — flat on the page like everything else in this baseline.

Click any point or its label to see why that metric scored the way it did, in a hairline-divided panel beside the chart (not a boxed card — see `html-theme.md`'s Scorecard Radar Chart component for the CSS and `.wp-*` panel classes). Before any click, the panel shows an **overall summary** (average score + which metric is strongest/weakest) — never an empty "click a point" placeholder; see `ruleset.md`'s "No dead-empty default states" rule.

```html
<div class="section" id="scorecard">
  <div class="section-title">Analyst Scorecard</div>
  <div class="fig-caption"><span class="fig-num">FIG. 04</span>Seven-metric scoring of business quality, each on a 0–10 scale where higher is always better.</div>
  <div class="radar-hint">click a point or label to see why it scored that way</div>
  <div class="scorecard-body">
    <div class="radar-wrap"><svg id="scorecardRadar" width="480" viewBox="0 0 400 400"></svg></div>
    <div class="scorecard-why" id="scorecardWhy"></div>
  </div>
</div>
```

The chart itself is built entirely in JS from a `METRICS` array — see the "Analyst Scorecard Radar Chart" block in the "Shared Interactive JS" appendix below. Populate `METRICS` with the 7 approved metric names (`ruleset.md` §5), each metric's score, and a one-sentence `why` grounded in a fact already stated elsewhere in this same report (a number, a named competitor, a dated event — never a generic restatement of the label). Example shape:

```js
var METRICS = [
  { label: 'Business Model', full: 'Business Model Strength', value: 8, why: 'One sentence citing a specific fact from this report.' },
  { label: 'Revenue Growth', full: 'Revenue Growth', value: 10, why: '...' },
  { label: 'Profitability', full: 'Profitability', value: 7, why: '...' },
  { label: 'Competitive Moat', full: 'Competitive Moat', value: 6, why: '...' },
  { label: 'Regulatory Safety', full: 'Regulatory Safety', value: 8, why: '...' },
  { label: 'Mgmt Execution', full: 'Management Execution', value: 8, why: '...' },
  { label: 'Long-Term Potential', full: 'Long-Term Potential', value: 8, why: '...' }
];
```

`label` is the short axis caption (keep it short — long full names get clipped against the chart edge); `full` is the complete metric name shown in the click panel, where there's room for it.

---

## Section 10 · Current Situation — Growth & Risks

Two flat text columns divided by a hairline rule. Left = growth drivers (green header). Right = risks (red header). Both columns use `.severity-list` — a colored stripe per row instead of an icon — so the two columns read as one consistent system side by side, not two different treatments (an icon-row list on one side and something else on the other reads as visually mismatched; this is a real failure mode, not hypothetical). Green stripes for drivers; red for active/severe risks, yellow for reduced/moderate ones. Only include ACTIVE or REDUCED risks — never RESOLVED.

```html
<div class="section" id="situation">
  <div class="section-title">Current Situation</div>
  <div class="fig-caption"><span class="fig-num">FIG. 05</span>Growth drivers weighed against active, recency-verified risks.</div>
  <div class="split-cols">
    <div>
      <h3 style="color:var(--color-success)">Growth Drivers</h3>
      <div class="severity-list">
        <div class="sev-row">
          <div class="sev-stripe" style="background:var(--green)"></div>
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
      <div class="severity-list">
        <div class="sev-row">
          <div class="sev-stripe" style="background:var(--red)"></div>  <!-- red for ACTIVE/severe, yellow for REDUCED/moderate -->
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

`[EDITORIAL OPINION]` tag on section title. Bull / Base / Bear as **interactive tabs** (not a table) — this section always carries 5–6 conditions per case, well past the 4+ threshold in `ruleset.md`'s "Interaction must earn its click" rule, so it always qualifies for the tabbed treatment (unlike Catalyst Scenarios in Section 7, which is conditional on density). All cases use `$` price targets (not %). Reuses the same `.scenario-tabs` component and tab-switching JS as Section 7's tabs — one interaction pattern, learned once, reused twice.

```html
<div class="section" id="scenario">
  <div class="section-title">Scenario Analysis <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="fig-caption"><span class="fig-num">FIG. 06</span>Twelve-month price scenarios weighted by probability, in dollar terms.</div>
  <div class="scenario-tabs" data-tabgroup="overall">
    <div class="tabs">
      <div class="tab bull active" data-tab="bull">Bull <span class="p mono">XX%</span></div>
      <div class="tab base" data-tab="base">Base <span class="p mono">XX%</span></div>
      <div class="tab bear" data-tab="bear">Bear <span class="p mono">XX%</span></div>
    </div>
    <div class="tab-panel show" data-panel="bull">
      <h4 style="color:var(--color-success)">Bull Case · $XX–$XX</h4>
      <div class="range">XX% probability · 12-month price target</div>
      <ul>
        <li>Condition for bull case 1</li>
        <li>Condition 2</li>
        <li>Condition 3</li>
        <li>Condition 4</li>
        <li>Condition 5</li>
      </ul>
    </div>
    <div class="tab-panel" data-panel="base">
      <h4 style="color:var(--color-warning)">Base Case · $XX–$XX</h4>
      <div class="range">XX% probability · 12-month price target</div>
      <ul><!-- 5–6 conditions --></ul>
    </div>
    <div class="tab-panel" data-panel="bear">
      <h4 style="color:var(--color-error)">Bear Case · $XX–$XX</h4>
      <div class="range">XX% probability · 12-month price target</div>
      <ul><!-- 5–6 conditions --></ul>
    </div>
  </div>
</div>
```

---

## Section 12 · Investor Debate

`[EDITORIAL OPINION]` tag. Five bullets each side, as **boxed `.debate-card`s with a VS badge** — one of the report's established boxed-treatment exceptions (see card discipline above). A debate is a genuinely oppositional content shape, not paired narrative like Sections 5/6/7's split-cols — it earns its own visual identity instead of the same flat treatment as everything else. Honest representation of both views — no bias.

```html
<div class="section" id="debate">
  <div class="section-title">Investor Debate <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="debate-grid debate-vs">
    <div class="debate-card optimist">
      <h3>The Optimist Sees…</h3>
      <ul>
        <li>Bull point 1</li>
        <li>Bull point 2</li>
        <li>Bull point 3</li>
        <li>Bull point 4</li>
        <li>Bull point 5</li>
      </ul>
    </div>
    <div class="debate-card pessimist">
      <h3>The Pessimist Sees…</h3>
      <ul>
        <li>Bear point 1</li>
        <li>Bear point 2</li>
        <li>Bear point 3</li>
        <li>Bear point 4</li>
        <li>Bear point 5</li>
      </ul>
    </div>
    <div class="vs-badge">VS</div>
  </div>
</div>
```

The VS badge hides below 760px (see `html-theme.md`) once `.debate-grid` collapses to a single stacked column — centered-overlay math only works with two side-by-side cards.

---

## Section 13 · Bottom Line Verdict

`[EDITORIAL OPINION]` tag. Three paragraphs: analogy, green case, bear case + time horizon.

```html
<div class="section" id="verdict">
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
<div class="section" id="wall">
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

## Shared Interactive JS

Paste before `</body>`, in one `<script>` block. Every piece below guards on `getElementById`/`querySelectorAll` returning nothing, so a report that skips a given component (e.g. picked the thin-content static scenario cards instead of tabs) doesn't error — omit the pieces you don't need, or leave them all in since the no-ops are free.

### Animated Segment Bars (Revenue Mix)

```js
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
```

### Scenario Tabs (Section 7's Catalyst Scenarios if tabbed, and Section 11 always)

One handler covers every `.scenario-tabs` group on the page, however many there are:

```js
document.querySelectorAll('.scenario-tabs').forEach(function (group) {
  group.querySelectorAll('.tab').forEach(function (tab) {
    tab.addEventListener('click', function () {
      var name = tab.getAttribute('data-tab');
      group.querySelectorAll('.tab').forEach(function (t) { t.classList.remove('active'); });
      tab.classList.add('active');
      group.querySelectorAll('.tab-panel').forEach(function (p) {
        p.classList.toggle('show', p.getAttribute('data-panel') === name);
      });
    });
  });
});
```

### Revenue Mix Donut ↔ Legend Hover-Link

Requires each donut `<circle>` and its matching `.legend-row` to share a `data-seg` value (see Section 4):

```js
(function () {
  var legend = document.getElementById('revenueLegend');
  var svg = document.getElementById('revenueDonut');
  if (!legend || !svg) return;
  legend.querySelectorAll('.legend-row').forEach(function (row) {
    row.addEventListener('mouseenter', function () {
      var seg = row.getAttribute('data-seg');
      legend.querySelectorAll('.legend-row').forEach(function (r) {
        r.classList.toggle('dim', r !== row);
        r.classList.toggle('hi', r === row);
      });
      svg.querySelectorAll('circle[data-seg]').forEach(function (c) {
        var match = c.getAttribute('data-seg') === seg;
        c.classList.toggle('seg-dim', !match);
        c.classList.toggle('active-glow', match);
      });
    });
    row.addEventListener('mouseleave', function () {
      legend.querySelectorAll('.legend-row').forEach(function (r) { r.classList.remove('dim', 'hi'); });
      svg.querySelectorAll('circle[data-seg]').forEach(function (c) { c.classList.remove('seg-dim', 'active-glow'); });
    });
  });
})();
```

### Scroll-Spy Section Rail

Builds itself from a `sections` array of `[id, shortLabel]` pairs — list every section id actually present on the page (see the id list in the Page Shell), in document order:

```js
(function () {
  var rail = document.getElementById('spyRail');
  if (!rail) return;
  var sections = [
    ['hero', 'Hero'], ['tldr', 'TL;DR'], ['snapshot', 'Snapshot'], ['mix', 'Revenue Mix'],
    ['story', 'What It Does'], ['model', 'Biz Model'], ['catalyst', 'Catalyst'], ['edge', 'Comp. Edge'],
    ['scorecard', 'Scorecard'], ['situation', 'Growth/Risks'], ['scenario', 'Scenarios'],
    ['debate', 'Debate'], ['verdict', 'Verdict'], ['wall', 'Consensus']
  ];
  var items = sections.map(function (s) {
    var el = document.getElementById(s[0]);
    if (!el) return null;
    var item = document.createElement('div');
    item.className = 'spy-item';
    item.innerHTML = '<span class="spy-label">' + s[1] + '</span><span class="spy-dot"></span>';
    item.addEventListener('click', function () { el.scrollIntoView({ behavior: 'smooth', block: 'start' }); });
    rail.appendChild(item);
    return { id: s[0], el: el, item: item };
  }).filter(Boolean);

  var obs = new IntersectionObserver(function (entries) {
    entries.forEach(function (entry) {
      if (entry.isIntersecting) {
        var match = items.find(function (i) { return i.el === entry.target; });
        if (!match) return;
        items.forEach(function (i) { i.item.classList.toggle('active', i === match); });
      }
    });
  }, { rootMargin: '-40% 0px -55% 0px', threshold: 0 });
  items.forEach(function (i) { obs.observe(i.el); });
  if (items.length) items[0].item.classList.add('active');
})();
```

### Analyst Scorecard Radar Chart

Draws the radar entirely from the `METRICS` array defined in Section 9, then **measures its own rendered content** (`getBBox()`) to set the final `viewBox` — this is deliberate, not incidental: hand-picking a `viewBox` size and hoping the labels fit is exactly the bug `ruleset.md`'s "Match canvas to content, not the reverse" rule exists to prevent. The internal coordinate system (`cx`/`cy`/`maxR` below) is arbitrary — it gets rescaled to fit whatever physical `width` the `<svg>` element declares, so don't hand-tune these numbers per report.

```js
(function () {
  var svgEl = document.getElementById('scorecardRadar');
  var whyEl = document.getElementById('scorecardWhy');
  if (!svgEl || !whyEl) return;

  // Paste the populated METRICS array from Section 9 here, replacing this
  // line — it must be declared inside this IIFE, not in an outer scope.
  var METRICS = [ /* 7 entries: {label, full, value, why} */ ];
  var MAX = 10;
  var dots = [];

  function svgNode(tag) { return document.createElementNS('http://www.w3.org/2000/svg', tag); }

  function average(data) {
    var sum = data.reduce(function (acc, d) { return acc + d.value; }, 0);
    return Math.round((sum / data.length) * 10) / 10;
  }

  function showOverall() {
    var avg = average(METRICS);
    var best = METRICS.reduce(function (a, b) { return b.value > a.value ? b : a; });
    var worst = METRICS.reduce(function (a, b) { return b.value < a.value ? b : a; });
    whyEl.innerHTML =
      '<div class="wp-title">Overall</div>' +
      '<span class="wp-score">' + avg + ' / 10 average</span>' +
      '<p class="wp-text">Strong across nearly every dimension, led by ' + best.full + ' (' + best.value + '/10). The one real soft spot is ' +
      worst.full + ' (' + worst.value + '/10) — click any point on the chart for the reasoning behind each score.</p>';
  }

  function showWhy(d) {
    whyEl.innerHTML =
      '<button class="wp-back" type="button">&larr; Overall</button>' +
      '<div class="wp-title">' + d.full + '</div>' +
      '<span class="wp-score">' + d.value + ' / 10</span>' +
      '<p class="wp-text">' + d.why + '</p>';
    whyEl.querySelector('.wp-back').addEventListener('click', function () {
      dots.forEach(function (dd) { dd.classList.remove('active'); });
      showOverall();
    });
  }

  var cx = 200, cy = 200, maxR = 140;
  var n = METRICS.length;
  var angleStep = (Math.PI * 2) / n;
  var startAngle = -Math.PI / 2;

  function pt(i, ratio) {
    var a = startAngle + i * angleStep;
    return [cx + maxR * ratio * Math.cos(a), cy + maxR * ratio * Math.sin(a)];
  }

  [0.25, 0.5, 0.75, 1].forEach(function (ratio) {
    var pts = METRICS.map(function (_, i) { return pt(i, ratio).join(','); }).join(' ');
    var poly = svgNode('polygon');
    poly.setAttribute('points', pts);
    poly.setAttribute('fill', 'none');
    poly.setAttribute('stroke', 'var(--border)');
    poly.setAttribute('stroke-width', ratio === 1 ? '1.2' : '1');
    poly.setAttribute('stroke-dasharray', ratio === 1 ? 'none' : '2,3');
    svgEl.appendChild(poly);
  });

  METRICS.forEach(function (_, i) {
    var p = pt(i, 1);
    var line = svgNode('line');
    line.setAttribute('x1', cx); line.setAttribute('y1', cy);
    line.setAttribute('x2', p[0]); line.setAttribute('y2', p[1]);
    line.setAttribute('stroke', 'var(--border)');
    line.setAttribute('stroke-width', '1');
    svgEl.appendChild(line);
  });

  var dataPts = METRICS.map(function (d, i) { return pt(i, d.value / MAX); });
  var dataPoly = svgNode('polygon');
  dataPoly.setAttribute('points', dataPts.map(function (p) { return p.join(','); }).join(' '));
  dataPoly.setAttribute('fill', 'var(--color-accent)');
  dataPoly.setAttribute('fill-opacity', '0.18');
  dataPoly.setAttribute('stroke', 'var(--color-accent)');
  dataPoly.setAttribute('stroke-width', '2');
  svgEl.appendChild(dataPoly);

  dataPts.forEach(function (p, i) {
    var dot = svgNode('circle');
    dot.setAttribute('cx', p[0]); dot.setAttribute('cy', p[1]);
    dot.setAttribute('r', 7);
    dot.setAttribute('fill', 'var(--color-accent)');
    dot.setAttribute('class', 'radar-dot');
    dot.addEventListener('click', function () {
      dots.forEach(function (dd) { dd.classList.remove('active'); });
      dot.classList.add('active');
      showWhy(METRICS[i]);
    });
    svgEl.appendChild(dot);
    dots.push(dot);
  });

  METRICS.forEach(function (d, i) {
    var lp = pt(i, 1.26);
    var anchor = 'middle';
    if (lp[0] < cx - 5) anchor = 'end';
    else if (lp[0] > cx + 5) anchor = 'start';
    var text = svgNode('text');
    text.setAttribute('x', lp[0]); text.setAttribute('y', lp[1]);
    text.setAttribute('text-anchor', anchor);
    text.setAttribute('dominant-baseline', 'middle');
    text.setAttribute('class', 'radar-axis-label');
    text.textContent = d.label;
    text.addEventListener('click', function () {
      dots.forEach(function (dd) { dd.classList.remove('active'); });
      dots[i].classList.add('active');
      showWhy(d);
    });
    svgEl.appendChild(text);
  });

  // Auto-fit the viewBox to whatever the labels actually render at, then match
  // the <svg>'s own physical height to that content's aspect ratio (instead of
  // forcing a square box) so there's no letterboxed empty space above/below.
  var bbox = svgEl.getBBox();
  var pad = 16;
  var vbW = bbox.width + pad * 2;
  var vbH = bbox.height + pad * 2;
  svgEl.setAttribute('viewBox', (bbox.x - pad) + ' ' + (bbox.y - pad) + ' ' + vbW + ' ' + vbH);
  var targetWidth = parseFloat(svgEl.getAttribute('width')) || 480;
  svgEl.setAttribute('height', Math.round(targetWidth * (vbH / vbW)));

  showOverall();
})();
```
