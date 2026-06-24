# Stock Analysis — Data Schema & Research Protocol

## Phase 1 · Research Queries (Run All Five in Parallel)

Use the current date to anchor all queries. Substitute `<TICKER>`, `<current year>`, and `<current month>` in every query before searching.

| # | Query template | Data to extract |
|---|----------------|-----------------|
| 1 | `<TICKER> stock fundamentals financial analysis <current year>` | Revenue, YoY growth rate, gross/net margins, EPS, forward guidance |
| 2 | `<TICKER> stock latest earnings results revenue` | Most recent quarterly numbers, beats/misses vs. consensus, management commentary |
| 3 | `<TICKER> stock risks competition regulatory <current year>` | Active risks, investigations, competitive threats, regulatory exposure |
| 4 | `<TICKER> stock hidden catalyst growth opportunity <current year>` | Underreported growth driver — new product, market, partnership, regulatory shift |
| 5 | `<TICKER> stock price target analyst rating <current year>` | Consensus rating, price target range and average, rating distribution |

**If Query 4 returns no useful results**, run a follow-up before moving on:
- `<TICKER> underreported catalyst <current year>`
- `<TICKER> next growth driver analysts missing`

If still nothing found, note it explicitly — the layout.md hidden catalyst section explains how to handle this case.

---

## Phase 2 · Risk Recency Verification (Run After Phase 1)

For every risk, investigation, lawsuit, or negative event found in Phase 1, run a targeted recency check before classifying it.

**Query format:** `<TICKER> <risk topic> resolved settled update <current month> <current year>`

**Examples:**
- `HIMS DOJ investigation resolved june 2026`
- `NVDA China export ban update june 2026`

### Risk Status Classification

| Status | Label to use | How to display |
|--------|-------------|----------------|
| Still active / unresolved | `[ACTIVE RISK]` | Risks card, red icon |
| Partially resolved / reduced | `[REDUCED — see note]` | Risks card, yellow icon, one-line note on what changed |
| Fully resolved / closed | `[RESOLVED]` | **Never list in Risks card.** Mention once in narrative text as historical context only. |
| No recent update found | `[STATUS UNKNOWN — as of <source date>]` | Risks card, yellow icon |

**Required for every risk item:** status label + last-verified month+year + source name.
Example: `Active as of Jun 2026 · Source: Reuters`

---

## Phase 3 · Data Model

Populate all fields below from search results before writing the HTML. If a field cannot be sourced, mark it `[Data not found]` — never estimate silently or leave a field blank with invented numbers.

```
COMPANY
  ticker:            string — uppercase exchange symbol
  exchange:          string — e.g. NASDAQ, NYSE, TSX
  full_name:         string — official company name
  tagline:           string — one sentence, zero jargon, 10-year-old reading level
  sector:            string — e.g. Healthcare, Semiconductors, Consumer Tech
  growth_stage:      "Profitable" | "Growing" | "Pre-profit" | "Turnaround"
  key_risk_label:    string — short phrase for the hero pill badge (e.g. "Competition Risk")

FINANCIALS
  stock_price:       string — current price with currency symbol
  market_cap:        string — e.g. "$42B"
  revenue_ttm:       string — trailing 12-month revenue
  revenue_growth:    string — YoY growth percentage
  gross_margin:      string — gross margin %
  net_income:        string — net profit or loss (label clearly)
  eps:               string — earnings per share (trailing or forward)
  forward_guidance:  string — management's stated full-year guidance
  analyst_target:    string — average analyst price target
  analyst_rating:    "Strong Buy" | "Buy" | "Hold" | "Sell" | "Strong Sell" | "No consensus data"
  next_binary_event: string — date + event name (the one thing that will move the stock most)

REVENUE_SEGMENTS
  segments: array of { name: string, pct_current: number, pct_projected_2yr: number, color: hex }
  note: "Exact breakdown" | "Estimated mix based on <source name>. Exact breakdown not publicly disclosed."
  — all pct_current values must sum to 100

RISKS
  — Only include items with status ACTIVE or REDUCED from Phase 2
  risks: array of { label: string, description: string, status: string, last_verified: string, source: string }

GROWTH_DRIVERS
  drivers: array of { icon: "star"|"arrow"|"bolt"|"globe", title: string, description: string }

HIDDEN_CATALYST
  what:        string — the specific opportunity (concrete, not generic)
  how_big:     string — TAM, market size, or projected revenue impact
  key_date:    string — the date or event that makes this real
  advantage:   string — why this company specifically, vs competitors
  readiness:   string — how prepared the company is today
  milestones:  array of { date: string, event: string, type: "past"|"present"|"future" }
  scenarios:   array of { name: string, prob_pct: number, impact_pct: number, conditions: string[] }
  — all prob_pct values must sum to 100; impact uses % only (no $ mixing)

ANALYST_SCORECARD
  scores: array of { metric: string, score: number (1-10), color: "green"|"yellow"|"red" }
  — Metrics (high score always means good/strong — see ruleset.md for naming rules):
    Business Model Strength, Revenue Growth, Profitability, Competitive Moat,
    Regulatory Safety, Management Execution, Long-Term Potential

SCENARIO_OVERALL
  bull: { prob_pct: number, price_low: number, price_high: number, conditions: string[] }
  base: { prob_pct: number, price_low: number, price_high: number, conditions: string[] }
  bear: { prob_pct: number, price_low: number, price_high: number, conditions: string[] }
  — all prob_pct values must sum to 100; prices always in $ terms (not %)

SOURCES
  urls: array of { label: string, url: string }
  — every URL used anywhere in the report must appear here
```

---

## Source Attribution Rules

- Every factual claim must trace to a named search result. Revenue, targets, risks, events — all sourced.
- If a full section cannot be sourced, write inside that section: `[No source found — this section could not be completed]`. Never pad with generic commentary.
- Revenue segment percentages estimated from partial data must be clearly labelled on the donut chart: *"Estimated mix based on [source name]. Exact breakdown not publicly disclosed."*
- If the stock is obscure, foreign-listed, or very small-cap and search results are sparse, open the report with a warning card: *"Limited public data available for this ticker. Sections marked [Limited Data] could not be fully sourced."*
