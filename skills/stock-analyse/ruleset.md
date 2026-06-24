# Stock Analysis — Ruleset

Each rule states: **Why** it exists → **What** a violation looks like → **How to fix** (the pattern we use).
Apply every rule silently — do not narrate fixes or mention this file in output.

---

## Output Naming

**Why:** Inconsistent naming breaks file organisation and makes reports hard to find by date.
**What a violation looks like:** `NVDA_June_2026.html`, `nvda_jun26.html`, `NVDA-jun26.html`
**How to fix:** `<UPPERCASE_TICKER>_<3-letter-lowercase-month><2-digit-year>.html` with an underscore separator only between ticker and date. No separator inside the date portion. Examples: `NVDA_jun26.html`, `HIMS_dec26.html`, `AAPL_jan27.html`.

---

## Typography — Font Assignments

**Why:** Mixing fonts randomly breaks the visual hierarchy. The Wisdom theme uses three fonts with distinct roles: Cinzel (display/headers), EB Garamond (body reading), Courier Prime (numbers/data). Using the wrong font in the wrong role makes the page feel inconsistent.

**What a violation looks like:** A stat value set in EB Garamond. A section title in Courier Prime. Body text hardcoded to a sans-serif. A paragraph using `font-family: var(--font-family-display)`.

**How to fix:**
- `var(--font-family-display)` (Cinzel) on: `.section-title`, card `h3`, `.stat-value`, `.stat-label`, `.mini-stat-label`, `.meter-label`, scenario headings, `.verdict-title`, `.hero-ticker`, `.hero-name`, pill text
- `var(--font-family)` (EB Garamond) on: all body paragraphs, list item descriptions — this is the default set on `body`, so no explicit declaration needed unless overriding
- `var(--font-family-mono)` (Courier Prime) on: all inline number values, data labels, `.stat-sub`, `.scenario-target`, `.scenario-prob`, `.legend-pct`, `.meter-label span:last-child`, `<code>` elements, `.timeline-date`, `.tldr-sym`

---

## Typography — Italic Restriction

**Why:** Italic in body text reads as hesitancy or emphasis, clashing with the report's authoritative tone. In the Wisdom theme, italic is reserved exclusively for the hero tagline as a deliberate stylistic choice.

**What a violation looks like:** `<p style="font-style:italic">`, `<em>` tags in paragraphs, italic on list items, italic on verdict text, italic on section descriptions.

**How to fix:** Use `font-style: italic` **only** on `.hero-tagline`. Nowhere else. Use font-weight or color for any other emphasis.

---

## Typography — Label Visibility

**Why:** Stat labels on the parchment surface (`#EBE4D1`) need strong contrast. Using `var(--muted)` (`#6E5E48`) for labels or going below 11px font-size makes them illegible, especially for older readers or in print.

**What a violation looks like:** `.stat-label { color: var(--muted); }`, `.stat-label { font-size: 9px; }`, `.mini-stat-label { font-weight: 400; }`

**How to fix:** Both `.stat-label` and `.mini-stat-label` must always use:
```css
color: var(--color-primary);   /* #1E3B6F — high contrast on parchment */
font-weight: 700;
font-size: 11px;               /* minimum; never lower */
letter-spacing: 1.2px;
text-transform: uppercase;
font-family: var(--font-family-display);
```

---

## Color — Surface Tokens

**Why:** Pure black and white surfaces break the parchment aesthetic. The Wisdom theme uses warm off-white tones everywhere — pure black/white look like copy-paste from a generic template.

**What a violation looks like:** `background: #ffffff`, `background: #000000`, `color: #000`, `background-color: white`

**How to fix:** Always use palette tokens:
- Page background → `var(--color-bg)` (#F4EFE2)
- Card surface → `var(--color-surface)` (#EBE4D1)
- Alternate surface → `var(--color-surface-alt)` (#DDD5BC)
- Primary text → `var(--color-text)` (#1C1812)
- Text on hero → `var(--color-text-on-primary)` (#F4EFE2)

Never introduce a new hex value that is not in the token palette.

---

## Color — Value Color-Coding

**Why:** Numbers without color are harder to scan. Consistent color-coding lets readers assess health at a glance without reading every figure.

**What a violation looks like:** All stat values in the same color. Revenue growth and net loss both rendered in `var(--color-text)`.

**How to fix:** Apply these CSS classes to `.stat-value` (and inline number spans where no class is available):
- `val-green` → positive number, growth, profit, beat
- `val-red` → negative number, loss, miss, decline
- `val-yellow` → mixed signal, guidance range, cautionary figure

---

## Anti-Pattern — No Left-Border Stripe on Cards

**Why:** A thick left border is the default "callout box" pattern for warnings and errors in developer tools. It reads as "something is wrong here" rather than as a neutral card, undermining the visual authority of every section.

**What a violation looks like:**
```css
border-left: 4px solid var(--color-accent);
border-left: 3px solid #B8860B;
```

**How to fix:** Every card and box accent line must be a **top** border:
```css
border-top: 3px solid var(--color-accent);
```
Never use a left, right, or bottom accent border on any card.

---

## Anti-Pattern — No Gradient-Fill Headlines

**Why:** `background-clip: text` gradient headlines are heavily overused by AI-generated pages. They also fail in some print environments and browser rendering modes.

**What a violation looks like:**
```css
background: linear-gradient(90deg, #1E3B6F, #B8860B);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

**How to fix:** Use `color` and `font-weight` for emphasis on headings. The Cinzel display font at weight 700 is distinctive enough without decoration.

---

## Anti-Pattern — No Inline `background:` on Meter Fills

**Why:** Meter fill colors are semantic signals (green = good, yellow = caution, red = bad). Inlining the color on the fill div detaches it from the semantic color system and makes it impossible to retheme.

**What a violation looks like:**
```html
<div class="meter-fill" style="width:70%;background:#3D6E3A"></div>
```

**How to fix:** Set color via CSS class only:
```html
<div class="meter-fill green" style="width:70%"></div>
```
The CSS classes `green`, `yellow`, and `red` on `.meter-fill` map to `--color-success`, `--color-warning`, and `--color-error` respectively.

---

## Anti-Pattern — No Separate `.meter-score` Div

**Why:** Putting the score in a separate div breaks the label+score relationship and requires extra layout work to align them. The score belongs semantically with its label.

**What a violation looks like:**
```html
<div class="meter-label">Business Model Strength</div>
<div class="meter-score">7 / 10</div>
<div class="meter-track">...</div>
```

**How to fix:** The score is the second `<span>` inside `.meter-label`:
```html
<div class="meter-label"><span>Business Model Strength</span><span>7 / 10</span></div>
```

---

## Scorecard — High Score Means Good

**Why:** If metric names are ambiguous or inverted, readers misread scores. "Regulatory Risk: 8/10" could mean "high risk" (bad) or "well-scored on regulatory" (good). This creates dangerous confusion for investment decisions.

**What a violation looks like:** `Regulatory Risk`, `Competition Intensity`, `Debt Level`, `Valuation Risk` as metric names.

**How to fix:** Write every metric name so that a high score is unambiguously desirable:
- ~~Regulatory Risk~~ → **Regulatory Safety** (high = safe)
- ~~Competition Intensity~~ → **Competitive Moat** (high = strong moat)
- ~~Debt Level~~ → include as a sub-note on Profitability, not a standalone metric
- ~~Valuation Risk~~ → omit from scorecard (it is a market condition, not a business quality score)

Approved metric names: Business Model Strength, Revenue Growth, Profitability, Competitive Moat, Regulatory Safety, Management Execution, Long-Term Potential.

---

## Section Title — No Extra Suffix Text

**Why:** Adding `(0–10)` or `(%)` to section titles clutters the header. The scale context is clear from the content.

**What a violation looks like:** `Analyst Scorecard (0–10)`, `<h2>Scenario Analysis</h2>`, `<p class="section-title">...`

**How to fix:** Section title is always `<div class="section-title">Name Here</div>` — no scale suffixes, no `<h2>` or `<p>` tags. Editorial tags are the only allowed suffix (see below).

---

## Editorial Tags — Placement and Format

**Why:** Readers need to know which sections are verified facts vs. editorial opinion vs. model estimates. Without clear labelling, opinion can be mistaken for sourced data.

**What a violation looks like:** Tag text scattered inside body paragraphs or bullet points. Tags used inside stat values. A fourth tag type invented for a new case. The tag repeated multiple times within the same section.

**How to fix:** Place the tag **once** at the section title only. Use only these three tags:

| Tag | When |
|-----|------|
| `[EDITORIAL OPINION]` | Scenario probabilities, investor debate, verdict analogies, qualitative assessments |
| `[ANALYST ESTIMATE]` | Price targets, consensus ratings, forward guidance from analyst reports |
| `[MODEL ESTIMATE]` | Projected revenue mix, TAM estimates, growth rates extrapolated from partial data |

Tag HTML (copy exactly):
```html
<span style="font-size:10px;font-weight:600;letter-spacing:1.5px;color:var(--muted);font-family:var(--font-family-display);text-transform:uppercase;margin-left:8px">[EDITORIAL OPINION]</span>
```

Sections that always require a tag:
- Scenario Analysis (Overall) → `[EDITORIAL OPINION]`
- Hidden Catalyst scenario grid → `[EDITORIAL OPINION]`
- Investor Debate → `[EDITORIAL OPINION]`
- Bottom Line Verdict → `[EDITORIAL OPINION]`
- Wall Street Consensus → `[ANALYST ESTIMATE]`
- Revenue Breakdown Chart (when estimated) → `[MODEL ESTIMATE]`

---

## TL;DR — Symbol Alignment

**Why:** `+` and `-` are narrower glyphs than `!` and `►`. Without a fixed-width column for symbols, the text column starts at different positions for each row, making the list look ragged and unprofessional.

**What a violation looks like:**
```html
<span style="color:var(--green);font-weight:800">+</span> Text...
<span style="color:var(--yellow);font-weight:800">!</span> Text...
```

**How to fix:** Every symbol span must have `width:16px; text-align:center; flex-shrink:0; font-family:var(--font-family-mono)` so all symbols occupy the same column width:
```html
<span class="tldr-sym" style="color:var(--green)">+</span>
```
The `.tldr-sym` class (defined in html-theme.md) provides the required fixed-width alignment.

---

## Scenario Consistency — Unit Locking

**Why:** Mixing `$` and `%` impact values in the same scenario grid forces readers to mentally convert between units, breaking comparison. This is especially dangerous when bull case shows `+$15` and bear shows `-20%` — incomparable values.

**What a violation looks like:**
- Overall scenario grid where bull shows `$80–$100 target` but bear shows `-25% downside`
- Catalyst scenario grid where positive shows `+30%` but negative shows `-$5`

**How to fix:**
- **Overall scenario grid** → always `$` price target ranges (e.g. `$60–$80 target`)
- **Catalyst scenario grid** → always `%` impact (e.g. `+25% stock impact`)
- Never mix units within the same grid. Pick one unit for each grid and apply it to all three cards.

---

## Integrity — No Fabrication

**Why:** Invented numbers presented as fact can cause real financial harm to readers who act on them.

**What a violation looks like:** Writing `Revenue: $4.2B` when no source confirmed this figure. Describing a partnership that was not found in search results. Stating analyst consensus when no analyst data was found.

**How to fix:**
- If a figure was not found in a search result → write `[Data not found]` in the stat box
- If a whole section cannot be sourced → write `[No source found — this section could not be completed]`
- If no analyst consensus was found → write `No analyst consensus data available`
- Never estimate silently — label every estimate as `[MODEL ESTIMATE]` or as `[ANALYST ESTIMATE]`

---

## Integrity — No Stale Risks

**Why:** An investigation from a year-old article may have since been dropped, settled, or escalated. Presenting a resolved issue as an active risk misleads the reader about the company's current exposure.

**What a violation looks like:** Listing a regulatory issue as `[ACTIVE RISK]` based on a 14-month-old article without running a recency check. Including a `[RESOLVED]` item in the Risks card.

**How to fix:**
- Every risk listed in the Risks card must have passed Phase 2 recency verification
- Resolved risks must not appear in the Risks card at all — at most one brief mention in narrative text with `[RESOLVED]` label
- Every risk item must show: status label + last-verified month/year + source name

---

## Language — Kid-Friendly Requirement

**Why:** The audience includes non-professional investors and first-time readers. Jargon without explanation loses them. The report must be accurate and accessible simultaneously.

**What a violation looks like:** Writing "TTM EBITDA margin expanded 340bps YoY on operating leverage" without any explanation. Using terms like "dilutive issuance", "amortisation of intangibles", or "float" without defining them.

**How to fix:** Every technical term must be explained the first time it appears in parentheses or with an em-dash. Example: "EBITDA margin (how much profit the company keeps from every dollar of revenue before taxes and accounting costs) expanded this quarter." The TL;DR and "What Does This Company Actually Do?" sections must read at a 10-year-old level — no jargon at all in those sections.

---

## No Emojis

**Why:** The Wisdom theme is a scholarly, editorial aesthetic. Emojis undermine its authoritative tone.

**What a violation looks like:** `🚀 Revenue is growing`, `⚡ Fast execution`, `📈 Analyst upgrades`

**How to fix:** Use text icons (`★`, `→`, `⚠`, `►`) or no icon at all. Never use Unicode emoji characters anywhere in the report.
