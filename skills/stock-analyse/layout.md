# Stock Analysis — HTML Layout & Section Templates

All sections sit inside `<div class="page">`. Write them in this exact order.

---

## Page Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TICKER — Stock Analysis · MonYY</title>
  <!-- Google Fonts (from html-theme.md) -->
  <style>
    /* CSS from html-theme.md — paste the full block here */

    /* Responsive layout — REQUIRED in every report */
    @media (max-width: 760px) {
      body { padding: 12px; }
      .grid-2,
      .debate-grid {
        grid-template-columns: 1fr;
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
<body>
<div class="page">

  <!-- Sections 1–16 in order below -->

</div>
<script>
  /* IntersectionObserver for animated segment bars — paste at end of file */
</script>
</body>
</html>
```

**Responsive grid behaviour:**

| Window width | `.grid-2` / `.debate-grid` | `.grid-3` / `.stat-grid` / `.scenario-grid` |
|---|---|---|
| > 760 px | 2 columns | 3 columns |
| 521–760 px | 1 column | 2 columns |
| ≤ 520 px | 1 column | 1 column |

The donut chart (`donut-wrap`) stacks vertically below 520 px.

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

Three-column stat grid. Minimum 9 stat cards. Color-code values: green = positive/growing, red = negative/loss, yellow = mixed.

```html
<div class="section">
  <div class="section-title">Financial Snapshot</div>
  <div class="stat-grid">
    <div class="stat-card">
      <div class="stat-label">Stock Price</div>
      <div class="stat-value">$XX.XX</div>
      <div class="stat-sub">As of Mon YYYY</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Market Cap</div>
      <div class="stat-value">$XXB</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Revenue (TTM)</div>
      <div class="stat-value val-green">$XXB</div>
      <div class="stat-sub">+XX% YoY</div>
    </div>
    <!-- Continue: Net Income, EPS, Gross Margin, Forward Guidance, Analyst Target, Next Event -->
  </div>
</div>
```

---

## Section 4 · Revenue Breakdown Chart

`[MODEL ESTIMATE]` tag on section title if breakdown is estimated.

```html
<div class="section">
  <div class="section-title">Revenue Mix <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[MODEL ESTIMATE]</span></div>
  <div class="card">

    <!-- Donut SVG + legend side by side -->
    <div class="donut-wrap">
      <svg width="200" height="200" viewBox="0 0 200 200">
        <!-- Each segment: stroke-dasharray="<seg_len> 440" stroke-dashoffset="<offset>" -->
        <circle cx="100" cy="100" r="70" fill="none" stroke="#E5DCC8" stroke-width="28"/>
        <circle cx="100" cy="100" r="70" fill="none" stroke="#1E3B6F" stroke-width="28"
                stroke-dasharray="220 440" stroke-dashoffset="0" stroke-linecap="butt"/>
        <!-- repeat per segment, incrementing offset by previous segment lengths -->
        <text x="100" y="104" text-anchor="middle" font-family="'Cinzel',serif" font-size="13" font-weight="700" fill="#1C1812">Revenue</text>
      </svg>
      <div class="donut-legend">
        <div class="legend-row">
          <div class="legend-dot" style="background:#1E3B6F"></div>
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
        <div class="seg-fill" style="width:50%;background:#1E3B6F"></div>
      </div>
      <div class="seg-proj js-proj-bar" data-target="60" style="width:0%;background:#1E3B6F;margin-top:3px;height:4px;border-radius:2px"></div>
      <div class="seg-note">Brief annotation explaining expected shift.</div>
    </div>
    <!-- repeat per segment -->

  </div>
</div>
```

IntersectionObserver JS (add to bottom of file) animates `.js-proj-bar` elements to their `data-target` width on scroll.

---

## Section 5 · What Does This Company Actually Do?

Two story-boxes with top accent borders.

```html
<div class="section">
  <div class="section-title">What Does This Company Actually Do?</div>
  <div class="grid-2">
    <div class="card">
      <h3>The Simple Story</h3>
      <p>Explain the business in one paragraph. Zero jargon. Use a simple analogy (e.g. "like Netflix but for your health"). Write as if explaining to a 10-year-old.</p>
    </div>
    <div class="card">
      <h3>The Big Bet Right Now</h3>
      <p>What is the company betting on this year? What would need to go right for it to pay off?</p>
    </div>
  </div>
</div>
```

---

## Section 6 · Business Model

Two-column grid.

```html
<div class="section">
  <div class="section-title">Business Model</div>
  <div class="grid-2">
    <div class="card">
      <h3>How They Make Money</h3>
      <ul style="margin:0;padding-left:18px;font-size:15px;line-height:1.65">
        <li>Revenue stream 1 — brief description</li>
        <li>Revenue stream 2</li>
      </ul>
    </div>
    <div class="card">
      <h3>Why the Model Is Clever</h3>
      <ul style="margin:0;padding-left:18px;font-size:15px;line-height:1.65">
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

Structure:

```html
<div class="section">
  <div class="section-title">Hidden Catalyst Deep Dive</div>

  <!-- Two story-boxes: what it is + why this company wins -->
  <div class="grid-2" style="margin-bottom:16px">
    <div class="card">
      <h3>The Opportunity</h3>
      <p>Specifics: what exactly, how big, what the timeline looks like.</p>
    </div>
    <div class="card">
      <h3>Why This Company Wins</h3>
      <p>Why this specific company has an advantage over competitors for this catalyst.</p>
    </div>
  </div>

  <!-- Stat grid: TAM, key date/event, company readiness -->
  <div class="stat-grid" style="margin-bottom:20px">
    <div class="stat-card">
      <div class="stat-label">TAM / Market Size</div>
      <div class="stat-value">$XXB</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Key Date / Event</div>
      <div class="stat-value" style="font-size:16px">Mon YYYY</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Company Readiness</div>
      <div class="stat-value" style="font-size:15px">High / Medium / Early</div>
    </div>
  </div>

  <!-- Vertical timeline: past milestones → present → future inflection -->
  <div class="card" style="margin-bottom:16px">
    <h3>Timeline</h3>
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

  <!-- Catalyst-specific 3-scenario grid — EDITORIAL OPINION tag on title -->
  <div class="section-title" style="margin-top:20px">Catalyst Scenarios <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="scenario-grid">
    <div class="scenario-card scenario-bull">
      <h3>Positive Outcome</h3>
      <div class="scenario-prob val-green">XX%</div>
      <div class="scenario-target">+XX% stock impact</div>
      <ul><li>Condition 1</li><li>Condition 2</li></ul>
    </div>
    <div class="scenario-card scenario-base">
      <h3>Mixed Outcome</h3>
      <div class="scenario-prob val-yellow">XX%</div>
      <div class="scenario-target">+X% to -X% stock impact</div>
      <ul><li>Condition 1</li></ul>
    </div>
    <div class="scenario-card scenario-bear">
      <h3>Negative Outcome</h3>
      <div class="scenario-prob val-red">XX%</div>
      <div class="scenario-target">-XX% stock impact</div>
      <ul><li>Condition 1</li></ul>
    </div>
  </div>

</div>
```

---

## Section 8 · Competitive Edge

Four to six item-rows. Include at least one underappreciated advantage.

```html
<div class="section">
  <div class="section-title">Competitive Edge</div>
  <div class="card">
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

Seven metrics on 0–10 scale. High score always means good/strong (see ruleset.md for naming constraint).

```html
<div class="section">
  <div class="section-title">Analyst Scorecard</div>
  <div class="card">
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

Two-column grid. Left = growth drivers (green header). Right = risks (red header). Only include ACTIVE or REDUCED risks — never RESOLVED.

```html
<div class="section">
  <div class="section-title">Current Situation</div>
  <div class="grid-2">
    <div class="card">
      <h3 style="color:var(--color-success)">Growth Drivers</h3>
      <div class="item-row">
        <div class="item-icon" style="color:var(--green)">→</div>
        <div>
          <div class="item-title">Driver Title</div>
          <div class="item-desc">Description of why this drives growth.</div>
        </div>
      </div>
      <!-- 3–4 drivers total -->
    </div>
    <div class="card">
      <h3 style="color:var(--color-error)">Risks</h3>
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
```

---

## Section 11 · Overall Scenario Analysis

`[EDITORIAL OPINION]` tag on section title. Three cards: Bull / Base / Bear. All use $ price targets (not %).

```html
<div class="section">
  <div class="section-title">Scenario Analysis <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="scenario-grid">
    <div class="scenario-card scenario-bull">
      <h3>Bull Case</h3>
      <div class="scenario-prob val-green">XX%</div>
      <div class="scenario-target">$XX–$XX target</div>
      <ul>
        <li>Condition for bull case 1</li>
        <li>Condition 2</li>
        <li>Condition 3</li>
        <li>Condition 4</li>
        <li>Condition 5</li>
      </ul>
    </div>
    <div class="scenario-card scenario-base">
      <h3>Base Case</h3>
      <div class="scenario-prob val-yellow">XX%</div>
      <div class="scenario-target">$XX–$XX target</div>
      <ul><!-- 5–6 conditions --></ul>
    </div>
    <div class="scenario-card scenario-bear">
      <h3>Bear Case</h3>
      <div class="scenario-prob val-red">XX%</div>
      <div class="scenario-target">$XX–$XX target</div>
      <ul><!-- 5–6 conditions --></ul>
    </div>
  </div>
</div>
```

---

## Section 12 · Investor Debate

`[EDITORIAL OPINION]` tag. Five bullets each side. Honest representation of both views — no bias.

```html
<div class="section">
  <div class="section-title">Investor Debate <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span></div>
  <div class="debate-grid">
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

`[ANALYST ESTIMATE]` tag on section title.

```html
<div class="section">
  <div class="section-title">Wall Street Consensus <span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[ANALYST ESTIMATE]</span></div>
  <div class="stat-grid">
    <div class="stat-card">
      <div class="stat-label">Consensus Rating</div>
      <div class="stat-value" style="font-size:18px">Buy</div>
      <div class="stat-sub">X Buy · X Hold · X Sell</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Avg. Price Target</div>
      <div class="stat-value val-green">$XX.XX</div>
      <div class="stat-sub">vs. current $XX.XX (+XX%)</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">Additional Signal</div>
      <div class="stat-value" style="font-size:16px">XX%</div>
      <div class="stat-sub">Short interest / Insider buying / Fair value estimate</div>
    </div>
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
