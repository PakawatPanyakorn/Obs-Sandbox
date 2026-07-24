---
name: stock-analyse
description: Research any stock and produce an HTML analysis page — fundamentals, revenue chart, scenario analysis, TL;DR, and hidden catalyst deep dive — themed and structured per-report from theme-factory/layout-factory presets picked to fit the company and avoid repeating recent reports. Saved to static/analysis/<TICKER>_<month><year>.html.
argument-hint: "<TICKER> e.g. AAPL, NVDA, TSLA"
disable-model-invocation: true
---

<what-to-do>

## Execution — Four Phases

### Phase 1 · Research

Read `~/.claude/skills/stock-analyse/modules/data-schema.md`.
Follow all research steps defined there (parallel queries → risk verification → data model population).
Do not proceed to Phase 1.5 until the full data model is populated.

### Phase 1.5 · Select Theme & Layout

Read `~/.claude/skills/stock-analyse/modules/style-selection.md` and follow it fully. It picks one theme-factory theme and one layout-factory layout that fit this specific company (sector, growth stage, risk profile), while avoiding whatever the last several reports already used — so reports don't all end up looking the same. This step is silent: don't narrate the selection process to the user. Carry the two chosen names (and the layout's family) into Phase 2.

### Phase 2 · Write HTML

Read these three modules **in order** before writing a single line of HTML:

1. `~/.claude/skills/stock-analyse/modules/html-theme.md` — how to pull the Phase 1.5 theme's tokens/fonts in, plus every component's token-only CSS
2. `~/.claude/skills/stock-analyse/modules/layout.md` — how to blend the Phase 1.5 layout's structure in, plus section order and HTML structure templates
3. `~/.claude/skills/stock-analyse/modules/ruleset.md` — anti-patterns, naming rules, and integrity constraints

Write the complete HTML file in a single pass after reading all three modules.
Apply every rule in `ruleset.md` silently — do not narrate fixes.

### Phase 3 · Save, Log & Confirm

**Output path (fixed):**

```
~/.claude/skills/stock-analyse/analysis/<TICKER>_<MMMyy>.html
```

- `<TICKER>` = uppercase (e.g. `HIMS`, `NVDA`)
- `<MMMyy>` = 3-letter lowercase month + 2-digit year, **no separator** (e.g. `jun26`, `jan27`)
- Example: `~/.claude/skills/stock-analyse/analysis/NVDA_jun26.html`

Always save to `~/.claude/skills/stock-analyse/analysis/`. Create the directory if it does not exist.

**After saving the HTML file, update `~/.claude/skills/stock-analyse/index.html`:**

Insert a new `<a class="report-card">` entry inside `<div class="report-grid" id="report-grid">`, immediately before the closing `</div>` of that grid. Use this exact template:

```html
    <a class="report-card" href="analysis/<TICKER>_<MMMyy>.html" data-name="<TICKER>" data-date="<YYYYMM>">
      <span class="card-ticker"><TICKER></span>
      <span class="card-company"><Full Company Name></span>
      <span class="card-date"><Mon YY></span>
    </a>
```

- `data-date` = `YYYYMM` as a 6-digit number (e.g. `202606`)
- `<Mon YY>` = 3-letter capitalised month + space + 2-digit year (e.g. `Jun 26`)
- Do not add a card if the same ticker+date already exists in the grid.

**Append the style pick to history** — add the new row to `~/.claude/skills/stock-analyse/modules/style-history.md` as described in Step 6 of `style-selection.md`, if not already done during Phase 1.5.

**Final reply — three lines only, nothing else:**

```
Saved: ~/.claude/skills/stock-analyse/analysis/NVDA_jun26.html
Style: <theme-name> theme · <layout-name> layout
Next event to watch: <date> — <event name and brief description>
```

Do not produce a summary, section recap, or explanation after saving the file.

</what-to-do>
