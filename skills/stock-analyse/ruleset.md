# Stock Analysis — Ruleset

Rules are grouped by concern. Each row: **why it matters → bad pattern → fix**.  
Apply every rule silently — never narrate fixes or reference this file in output.  
Token names (e.g. `--color-accent`) refer to whatever values the active theme defines — not hardcoded to any specific theme.

---

## 1. File Output

| Rule | Violation | Fix |
|------|-----------|-----|
| **Naming** | `NVDA_June_2026.html`, `nvda_jun26.html`, `NVDA-jun26.html` | `<TICKER>_<mon><YY>.html` — ticker uppercase, 3-letter lowercase month, 2-digit year, one underscore between ticker and date, no separator inside the date. E.g. `NVDA_jun26.html` |

---

## 2. Typography

| Rule | Violation | Fix |
|------|-----------|-----|
| **Font role** | Stat value in body font; section title in mono font; body text hardcoded to sans-serif | Display font (`--font-family-display`) → headings, stat values, labels, pills, scenario headings. Body font (`--font-family`) → paragraphs, descriptions (set on `body` by default). Mono font (`--font-family-mono`) → inline numbers, data labels, dates, code |
| **Italic** | `<em>` in body text; italic on verdict, list items, or section descriptions | Italic only on the hero tagline. Use font-weight or color for all other emphasis |
| **Label contrast** | `.stat-label { color: var(--muted); }` or font-size below 11px or weight below 700 | Both `.stat-label` and `.mini-stat-label`: primary text color, weight 700, min 11px, 1.2px letter-spacing, uppercase, display font |

---

## 3. Color & Theming

| Rule | Violation | Fix |
|------|-----------|-----|
| **Surface tokens** | `background: #ffffff`, `background: #000`, raw hex not in the theme palette | Always use theme CSS tokens — page bg, card surface, alternate surface, primary text, text-on-primary. Never introduce a hex value outside the token palette |
| **Value color-coding** | Revenue growth and net loss both in the same color | Positive/growth/beat → `val-green`; Negative/loss/miss → `val-red`; Mixed/cautionary/guidance range → `val-yellow` |

---

## 4. Layout Anti-Patterns

| Rule | Violation | Fix |
|------|-----------|-----|
| **Card accent border** | `border-left: 4px solid var(--color-accent)` | Top border only: `border-top: 3px solid var(--color-accent)`. Never left, right, or bottom accent borders on any card |
| **Gradient headlines** | `background-clip: text` + `linear-gradient` + `-webkit-text-fill-color: transparent` | Use `color` + `font-weight` only. Display font at weight 700 is distinctive enough |
| **Meter fill color** | `<div class="meter-fill" style="width:70%;background:#3D6E3A">` | Color via semantic class only: `<div class="meter-fill green" style="width:70%">`. Classes `green`, `yellow`, `red` map to success/warning/error tokens |
| **Meter score placement** | Separate `<div class="meter-score">7 / 10</div>` element | Score is the second `<span>` inside `.meter-label`: `<div class="meter-label"><span>Label</span><span>7 / 10</span></div>` |
| **Fixed grid columns** | `.grid-2 { grid-template-columns: 1fr 1fr }` with no media queries | Every report MUST include the two responsive breakpoints from `layout.md`: 760 px (2-col grids collapse to 1 col; 3-col grids collapse to 2 col) and 520 px (all grids collapse to 1 col). The `donut-wrap` must also stack vertically at 520 px |

---

## 5. Scorecard & Metrics

| Rule | Violation | Fix |
|------|-----------|-----|
| **High score = good** | "Regulatory Risk: 8/10" — ambiguous whether high is safe or dangerous | Every metric name must make a high score unambiguously desirable. Readers must never need to invert |
| **Metric name list** | "Valuation Risk", "Debt Level", "Competition Intensity" as standalone scorecard rows | Approved names: Business Model Strength, Revenue Growth, Profitability, Competitive Moat, Regulatory Safety, Management Execution, Long-Term Potential |

---

## 6. Content Structure

| Rule | Violation | Fix |
|------|-----------|-----|
| **Section title element** | `<h2>`, `<p class="section-title">`, or suffix like "(0–10)" in the title | Always `<div class="section-title">Name</div>` — no HTML heading tags, no scale or unit suffixes |
| **Editorial tags** | Tag inside body text; tag repeated within a section; new fourth tag type invented | One tag per section, placed at the section title only. Three allowed types: `[EDITORIAL OPINION]`, `[ANALYST ESTIMATE]`, `[MODEL ESTIMATE]` |
| **TL;DR symbols** | Symbol spans with no fixed width, causing ragged column alignment | Use `.tldr-sym` class: `width:16px`, centered, mono font — all symbols share one fixed-width column |
| **Scenario units** | Bull shows `$80–$100` while bear shows `-25%` in the same grid | Overall scenario grid → always `$` price target ranges. Catalyst grid → always `%` impact. Never mix units within a single grid |

---

## 7. Data Integrity

| Rule | Violation | Fix |
|------|-----------|-----|
| **No fabrication** | Writing `Revenue: $4.2B` when no source confirmed it; describing an unverified partnership | Unfound figure → `[Data not found]`. Whole section unsourceable → `[No source found — this section could not be completed]`. Every estimate labeled `[MODEL ESTIMATE]` or `[ANALYST ESTIMATE]` |
| **No stale risks** | Listing a settled regulatory issue as `[ACTIVE RISK]` based on a year-old article | Every risk must pass recency verification. Resolved risks → omit from the Risks card entirely (brief narrative mention with `[RESOLVED]` label at most). Each risk must show: status + last-verified month/year + source name |

---

## 8. Language & Tone

| Rule | Violation | Fix |
|------|-----------|-----|
| **Plain language** | "TTM EBITDA margin expanded 340bps YoY on operating leverage" with no explanation | Define every technical term on first use in parentheses or with an em-dash. TL;DR and "What Does This Company Do?" sections — no jargon at all, readable at a 10-year-old level |
| **No emojis** | `🚀 Revenue growing`, `📈 Analyst upgrades` | Use text symbols only (`★`, `→`, `⚠`, `►`) or no symbol. Never Unicode emoji characters anywhere in the report |
