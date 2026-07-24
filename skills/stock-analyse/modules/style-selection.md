# Style Selection — Theme & Layout

Run this after Phase 1's data model is fully populated and before any HTML is written. Goal: pick **one** theme-factory theme and **one** layout-factory layout that genuinely fit this specific company, and that haven't been used to death on recent reports. This step is silent — do not narrate it to the user; the choice shows up in the file, and gets one line in the final reply (see `skill.md` Phase 3).

## 1. Build the context signal

Compress the populated data model into one short context string, the same shape theme-factory/layout-factory's own `recommend` mode expects:

```
Financial analyst report for <full_name> (<ticker>), sector <sector>, growth stage <growth_stage>.
Key risk: <key_risk_label>. Mood: <derived mood — see below>.
Content shape: data-dense financial report — stat tiles, scenario/debate cards, a revenue donut,
a risk/catalyst timeline, and long-form narrative sections (business story, verdict, investor debate).
```

**Derive the mood word(s)** from the data model rather than inventing one:
- `growth_stage: "Profitable"` + low/moderate risk severity → *stable, institutional, blue-chip*
- `growth_stage: "Growing"` or `"Pre-profit"` + a genuinely large hidden-catalyst TAM → *speculative, high-growth, frontier*
- `growth_stage: "Turnaround"`, or 2+ `[ACTIVE RISK]` items with severe language → *distressed, high-stakes, contested*
- Sector-specific texture worth folding in when present: biotech/deep-tech → *technical, clinical*; consumer/retail → *approachable, consumer-facing*; industrials/energy → *industrial, structural*; fintech/crypto-adjacent → *fast-moving, digital-native*

Don't force a mood that isn't supported by the data — a boring profitable industrial company should read as boring-and-credible, not get dressed up as "frontier."

## 2. Read the history log

Read `modules/style-history.md` in full. Take the **last 6 rows** (most recent). Collect their `Theme` and `Layout` values into two exclude-first sets. These are the names to avoid unless nothing else fits.

## 3. Pick the theme

Follow `../theme-factory/modules/recommend-mode.md`'s process using the context string from step 1:

1. Read `../theme-factory/modules/SUMMARY.md`, score every row against **Aesthetic / Personality / Tone / Best For / Avoid When**. Disqualify any row whose **Avoid When** matches this being a dense financial/business report (several themes explicitly rule this out — respect that).
2. Narrow to the top 4-5 candidates.
3. **Apply the history filter**: drop any candidate whose name is in the last-6 theme set from step 2, unless fewer than 2 candidates would remain — repetition-avoidance loses to genuine fit only when the shortlist would otherwise collapse to nothing.
4. Open the surviving top 2-3 candidates' `../theme-factory/themes/<name>.md` docs (**When To Use** / **When NOT To Use** / **Color Role Guidance**) to confirm the fit holds up.
5. Pick exactly 1. Note one sentence of reasoning (for your own bookkeeping — not shown to the user).

## 4. Pick the layout

Follow `../layout-factory/modules/recommend-mode.md`'s process, same context string:

1. Check `../layout-factory/modules/shared-signal-table.md` for any named-archetype hint (rare for this skill, but respect it if the user's request mentions one, e.g. "make it feel like a Bloomberg terminal" → dashboard family).
2. Read `../layout-factory/modules/SUMMARY.md`, score against **Family / Best For / Avoid When / Medium Fit**. This is a static, non-filterable, single-page HTML report — disqualify `dashboard-with-rail` unless the request specifically asks for a persistent nav/filter feel; its own **Avoid When** rules out exactly this content shape by default.
3. Narrow to top 4-5, apply the history filter from step 2 the same way as the theme (drop last-6-layout names unless the shortlist would collapse).
4. Open the surviving top 2-3 candidates' `../layout-factory/layouts/<name>.md` docs to confirm fit and pull concrete **Region / Component Guidance**.
5. Pick exactly 1.

## 5. Resolve the family for blend guidance

Note the chosen layout's `family` field (from its SUMMARY.md row or JSON): `data-dense-report`, `editorial-narrative`, `grid-discipline`, or `dashboard-legitimate`. Phase 2 (`layout.md`) uses this to decide how to blend the report's existing stat-card/scenario-card components into the chosen structure — see `layout.md`'s "Structural Blend" section.

## 6. Record the pick

Before finishing Phase 3, append one row to `modules/style-history.md`:

```
| <TICKER> | <Mon YYYY> | <theme-name> | <layout-name> |
```

Insert it as the new last row. Never edit or reorder existing rows.

## Output

Carry forward two values into Phase 2: the chosen theme name and the chosen layout name (+ its family). Nothing about this process is shown to the user mid-flow.
