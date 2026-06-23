---
description: Research any stock and produce a minimalist-themed HTML analysis page — fundamentals, revenue chart, scenario analysis, TL;DR, and hidden catalyst deep dive — saved to static/<TICKER>_analysis.html.
argument-hint: "<TICKER> e.g. AAPL, NVDA, TSLA"
---

# Stock Analyse Command

Produce a professional, kid-friendly stock analysis HTML page for the ticker provided in `$ARGUMENTS`.

## Research Phase

Use the current date from the system context to determine the current year and month. Substitute it wherever searches need a time anchor.

### Step 1 — Initial Research (Run All in Parallel)

1. `<TICKER> stock fundamentals financial analysis <current year>` — revenue, growth rate, margins, EPS, guidance
2. `<TICKER> stock latest earnings results revenue` — most recent quarterly numbers
3. `<TICKER> stock risks competition regulatory <current year>` — key threats and bottlenecks
4. `<TICKER> stock hidden catalyst growth opportunity <current year>` — any underreported growth driver (new product, market, partnership, regulation shift)
5. `<TICKER> stock price target analyst rating <current year>` — Wall Street consensus, price targets

### Step 2 — Recency Verification (Run After Step 1, Before Writing)

For every risk, investigation, lawsuit, regulatory issue, or negative event found in Step 1, run a follow-up search to check whether it has since been resolved, reduced, or changed status:

- Query format: `<TICKER> <risk topic> resolved settled update <current month> <current year>`
- Examples: `HIMS DOJ investigation resolved 2026`, `HIMS FDA warning letter outcome june 2026`

**Classify each item based on what you find:**

| Status | Label to use in HTML | How to display |
|--------|----------------------|----------------|
| Still active / unresolved | `[ACTIVE RISK]` | Show in the Risks section in red |
| Partially resolved / reduced pressure | `[REDUCED — see note]` | Show in Risks section in yellow with a note explaining what changed |
| Fully resolved / closed | `[RESOLVED]` | Do NOT list in Risks section. Mention briefly in the Current Situation narrative as context only |
| No update found | `[STATUS UNKNOWN — as of <source date>]` | Show in Risks section in yellow, note the date of last known status |

**Every risk item in the HTML must show its last-verified date** pulled from the source: e.g. `Last updated: June 2026 · Source: Reuters`.

### Step 3 — Identify What to Report

Identify the company's:
- Core business and revenue breakdown by segment (%)
- Biggest current growth driver and its size/trajectory
- One under-covered or hidden catalyst most investors are not talking about
- Only risks that are currently ACTIVE or REDUCED — never list RESOLVED items as risks
- Current-year and long-term guidance

## HTML Output Rules

Save the result to `static/analysis/<TICKER>_<month>_<year>.html` where:
- `<TICKER>` is uppercase (e.g. `HIMS`, `NVDA`)
- `<date>` is the 3-letter lowercase month + 2-digit year with no separator (e.g. `jun26`, `jan27`, `dec28`)

Example: `static/analysis/HIMS_jun26.html`

If the `static/analysis/` directory does not exist, create it first. If `static/` itself does not exist, save directly to `analysis/<TICKER>_<month>_<year>.html` and create that folder.

The HTML must follow this exact section order:

### 1. `<head>` — Apply Minimalist Theme

Use this exact CSS block inside `<style>`. It is the minimalist theme from theme-factory. Do NOT use a dark background — use the light minimalist palette:

```css
:root {
  --color-primary:         #4f5d75;
  --color-primary-light:   #d0d8e4;
  --color-secondary:       #ef8354;
  --color-accent:          #ef8354;
  --color-bg:              #ffffff;
  --color-surface:         #f7f8fa;
  --color-surface-alt:     #eef0f4;
  --color-text:            #2d3142;
  --color-text-muted:      #50566a;
  --color-text-on-primary: #ffffff;
  --color-border:          #d6d9e0;
  --color-success:         #3d9e6d;
  --color-warning:         #d4980e;
  --color-error:           #c94040;

  --font-family:         Inter, system-ui, -apple-system, sans-serif;
  --font-size-base:      16px;
  --font-weight-heading: 700;
  --line-height:         1.6;
  --radius-card:         12px;
  --shadow-sm:           0 1px 3px rgba(45,49,66,0.08);
  --shadow-md:           0 4px 12px rgba(45,49,66,0.12);
  --shadow-lg:           0 8px 24px rgba(45,49,66,0.16);

  /* Shorthand aliases used throughout */
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

The hero banner must be a contained "big box" card — **not** a full-width stripe. It sits inside the `.page` wrapper so it is constrained to the content width and has rounded corners and a drop shadow. Use this exact CSS:

```css
.hero {
  background: linear-gradient(135deg, #4f5d75 0%, #3d4d63 60%, #2d3a52 100%);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  color: #fff;
  padding: 36px 32px;
  margin-bottom: 24px;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: '';
  position: absolute; top: -60px; right: -60px;
  width: 220px; height: 220px;
  background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, transparent 70%);
  border-radius: 50%;
}
.hero-ticker  { font-size: 13px; font-weight: 700; letter-spacing: 2px; color: rgba(255,255,255,0.65); text-transform: uppercase; margin-bottom: 6px; }
.hero-name    { font-size: 28px; font-weight: 800; margin-bottom: 8px; color: #ffffff; }
.hero-tagline { font-size: 15px; color: rgba(255,255,255,0.75); max-width: 540px; margin-bottom: 20px; }
.hero-pills   { display: flex; flex-wrap: wrap; gap: 8px; }
.pill         { padding: 4px 14px; border-radius: 50px; font-size: 12px; font-weight: 600; border: 1px solid; }
.pill-blue    { background: rgba(255,255,255,.15); border-color: rgba(255,255,255,.4);  color: #ffffff; }
.pill-green   { background: rgba(61,158,109,.25);  border-color: rgba(61,158,109,.6);   color: #7ee8b8; }
.pill-red     { background: rgba(201,64,64,.25);   border-color: rgba(201,64,64,.6);    color: #f4a0a0; }
.pill-yellow  { background: rgba(212,152,14,.25);  border-color: rgba(212,152,14,.6);   color: #f5d070; }
```

Place the hero as the **first child inside `<div class="page">`** — never outside it. Use this HTML structure:

```html
<div class="page">
<div class="hero">
  <div class="hero-ticker">NYSE: AAPL &nbsp;|&nbsp; Stock Analysis &nbsp;|&nbsp; June 2026</div>
  <div class="hero-name">Apple Inc.</div>
  <div class="hero-tagline">One sentence that explains the company like you're talking to a 10-year-old.</div>
  <div class="hero-pills">
    <span class="pill pill-blue">Consumer Tech</span>
    <span class="pill pill-green">Profitable</span>
    <span class="pill pill-yellow">Valuation Risk</span>
  </div>
</div>
```

### 2. Hero Banner
- Ticker meta line: `EXCHANGE: TICKER &nbsp;|&nbsp; Stock Analysis &nbsp;|&nbsp; Month YYYY` — use the same month + year as the filename
- Company full name as `.hero-name`
- One-sentence tagline (`.hero-tagline`) explaining the company to a 10-year-old — no jargon
- Pill badges (`.hero-pills`): sector tag (`pill-blue`), growth stage (`pill-green` / `pill-yellow`), key risk label (`pill-red` / `pill-yellow`)

### 3. TL;DR Box
Bordered card with left accent line. Use `+` (green) / `!` (yellow) / `-` (red) / `►` (blue) prefix icons. Cover:
- What the company does (1 line)
- The key thing happening right now (pivot, problem, opportunity)
- The hidden / underreported catalyst
- The main risk
- Verdict sentence with analyst target vs current price and next binary event to watch

### 4. Financial Snapshot
3-column stat grid showing at minimum: stock price, market cap, latest revenue, YoY revenue growth %, net income or loss, subscriber/user count (if applicable), forward guidance, international split (if relevant), long-term target.

Color code values: green = positive/growing, red = negative/loss, yellow = mixed/caution.

### 5. Revenue Breakdown Chart
SVG donut chart (200×200) with a legend beside it showing revenue mix by segment (%). Use distinct colors per segment. Add a dashed placeholder row for any upcoming segment currently at 0% with projected future %.

Below the donut, add horizontal bar rows comparing current % vs projected % in 2 years for each segment with a brief annotation explaining the expected shift.

Animate the "new/future" segment bar with an IntersectionObserver JS snippet at the bottom of the file.

### 6. "What Does This Company Actually Do?" Section
Two story-boxes with left accent border:
- Box 1: Simple story (explain like a kid — one paragraph, no jargon)
- Box 2: The big bet right now (what is the company betting on this year)

### 7. Business Model
2-column grid:
- Left card: "How They Make Money" — revenue streams as bullet list
- Right card: "Why the Model Is Clever" — structural advantages

### 8. Hidden Catalyst Deep Dive
This is the most important section. Research the one growth driver that is underreported or not fully priced in. For each stock this will be different — it could be a new product category, a regulatory event, a geographic expansion, a technology pivot, a partnership, etc.

Structure:
- Two story-boxes at the top explaining the catalyst simply
- Left card: specifics of the opportunity (what exactly, how big, timeline)
- Right card: why THIS company has an advantage over competitors for this catalyst
- Stat grid: TAM, key date/event, company readiness
- Timeline component (vertical dots) showing past milestones → current moment → future inflection point
- Catalyst-specific 3-scenario analysis (Approved/Positive / Mixed / Rejected/Negative) with % probabilities and % stock impact for all three (never mix $ and % in the same scenario grid — pick one unit and use it consistently)

### 9. Competitive Edge
Card with item-rows. Each row: icon (star/arrow/warning) + title + description. Cover 4–6 real advantages including at least one that is underappreciated.

### 10. Analyst Scorecard
Horizontal meter bars (0–10 scale) for: Business Model Strength, Revenue Growth, Profitability, Competitive Moat, Regulatory Risk, Management Execution, Long-Term Potential. Color each bar green/yellow/red based on the score.

### 11. Current Situation — Growth & Risks
2-column grid:
- Left card (green header): 3–4 growth drivers with icon rows
- Right card (red header): 3–4 risks/bottlenecks with icon rows

Rules for the Risks card:
- Only include risks with status `[ACTIVE RISK]` or `[REDUCED]` from the recency verification step
- Never include `[RESOLVED]` items as risks — they belong in the narrative text at most
- Each risk item must show its status label and last-verified date in small muted text below the description, e.g. `Active as of Jun 2026 · Source: Reuters`
- `[REDUCED]` risks use a yellow icon instead of red, with a one-line note on what changed (e.g. "Novo Nordisk settlement reduced DOJ pressure — civil case still open")

### 12. Scenario Analysis (Overall)
3-column scenario cards: Bull / Base / Bear. Each must show:
- Probability (%)
- Price target range (e.g. $60–$80) — always in $ terms for overall scenarios
- 5–6 bullet conditions that would make this scenario happen

### 13. Investor Debate Box
2-column grid: "The Optimist Sees…" vs "The Pessimist Sees…" — 5 bullets each, honestly representing both sides.

### 14. Bottom Line Verdict
Gradient card with a 3-paragraph verdict:
- Para 1: A simple analogy (like the surfboard/wave analogy used for HIMS)
- Para 2: Why the long-term story is believable (green case summary)
- Para 3: Why the near-term pain is real (bear case summary), ending with time horizon recommendation

### 15. Wall Street Consensus
3-column stat grid: consensus rating, average price target vs current price, and one additional signal (fair value estimate, short interest, insider buying, etc.)

### 16. Footer
Data sources as markdown links. Disclaimer: "This is not financial advice. For informational purposes only."

## Integrity Rules — STRICT, No Exceptions

These rules override everything else. Violating them is worse than producing a shorter report.

### No Fabrication
- **Never invent numbers.** If a specific figure (revenue, price target, margin, subscriber count, market share) was not found in a search result, do not write it. Leave the stat box blank and label it "Data not found" rather than estimating.
- **Never invent events.** Do not describe a partnership, acquisition, regulatory decision, product launch, or lawsuit unless a search result explicitly confirmed it.
- **Never invent analyst ratings or price targets.** If no consensus data was found, say "No analyst consensus data available" in that section.
- **If a search returns no useful results for a section**, write a clearly marked notice inside that section: `[No source found — this section could not be completed]` and move on. Do not fill the gap with plausible-sounding guesses.

### Source Attribution
- **Every factual claim must trace to a search result.** Revenue figures, growth rates, subscriber counts, guidance numbers, regulatory decisions, partnership details — all must come from a named source found during research.
- **The footer Sources list is mandatory.** Every URL used must appear there as a clickable link. If a fact came from a source, that source must be in the footer.
- **Revenue segment percentages** are estimates unless an official breakdown was found. If estimating from partial data, label the donut chart clearly: "Estimated mix based on [source]. Exact breakdown not publicly disclosed."

### Opinion vs Fact — Clear Separation
- **Any forward-looking projection, price target estimate, or scenario probability is an opinion.** Label it visibly with one of these tags rendered in the HTML:
  - `[ANALYST ESTIMATE — source]` for figures taken from analyst reports
  - `[MODEL ESTIMATE — based on X]` for figures derived by inference from known data
  - `[EDITORIAL OPINION]` for qualitative judgements made by this analysis (e.g. "management has been disciplined")
- **Scenario probabilities (30%, 50%, 20% etc.) are always editorial opinion**, not forecasts. Add a small note under each scenario grid: "Probabilities are editorial judgements based on available evidence, not statistical forecasts."
- **The investor debate section and verdict are explicitly opinion sections.** Add a banner at the top of each: "The following reflects analytical opinion, not verified fact."

### Staleness — Never Present Resolved Issues as Active Risks
- **A risk that has been resolved must not appear in the Risks section.** It may be mentioned once in narrative text as historical context with a `[RESOLVED]` tag.
- **Every risk item must show when its status was last verified** (month + year + source). If you cannot find a recent update, label it `[STATUS UNKNOWN — last known: <date>]` in yellow, not red.
- **Do not copy risks from old articles without verifying their current status.** An investigation mentioned in a 12-month-old article may have since been dropped, settled, or escalated. Always search for the latest update before listing it.

### When in Doubt — Stop and Say So
- If there is not enough search data to write a substantive hidden catalyst section, say: "Insufficient public data found to identify a clear underreported catalyst for this stock. A follow-up search is recommended."
- If the stock is obscure, foreign-listed, or very small-cap and search results are sparse, open the report with a warning card: "Limited public data available for this ticker. Sections marked [Limited Data] could not be fully sourced."
- **Never pad a section with generic industry commentary to make it look complete.** A short honest section is better than a long fabricated one.

## Quality Rules

- **Consistency**: All scenario impact metrics must use the same unit within each grid (all $ or all % — never mixed)
- **Kid-friendly language**: Avoid jargon. Every technical term must be explained the first time it appears
- **No emojis** in the output
- **Colors must contrast** against their background — don't use dark text on dark background or light text on light background
- **The hidden catalyst section must be substantive** — if initial searches don't surface one, run a follow-up search specifically for `<TICKER> underreported catalyst <current year>` or `<TICKER> next growth driver analysts missing`. If still nothing found, say so honestly.
- **Revenue percentages must add to 100%** across all segments in the donut chart. If exact breakdown is unknown, label as estimated.
- **All three scenario cards in any grid must use the same impact metric format**

## Output Style Notes

Key things to always do:
- TL;DR at the top so busy readers get the full picture in 30 seconds
- Explain complex things like a kid (e.g. "like Netflix but for your health") — no jargon without explanation
- Revenue donut chart with forward-looking mix projections (~2 years out)
- A dedicated deep-dive on the hidden/underreported catalyst — this must be the longest and most researched section
- Consistent units in scenario grids — all % or all $, never mixed within the same grid
- The vertical timeline showing past milestones → present moment → upcoming binary event
- Minimalist light theme (CSS variables embedded above)
- Honest two-sided investor debate section with no bias toward bull or bear

Do not produce a summary or explanation after writing the file — just confirm the file path where the analysis was saved and the one next binary event to watch for this stock.
