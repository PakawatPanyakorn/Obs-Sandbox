# Recommend Mode

Given free-text context about a project, suggest the top 3 best-fit existing layouts with reasons — without opening all 20 preset files.

## 1. Intake

**With context** (content shape, medium, genre) → proceed straight to filtering.

**Without context** (bare `layout recommend`) → ask 1-2 clarifying questions, e.g.: "What are you laying out, and for what medium (web page, report, slides)?" Don't ask more than 2 — proceed with what you have rather than interrogating the user.

Useful signals to listen for: content shape (text-heavy, chart-heavy, card/list-heavy, mixed), whether one item genuinely dominates the rest or everything is peer-weighted, target medium (web/print/presentation/markdown), and named-archetype references ("like the Economist", "Tufte-style") — these map directly via `modules/shared-signal-table.md`.

## 2. First-pass filter via shared-signal-table.md

If the request contains a named-archetype signal or a recognizable "like X" reference, check `modules/shared-signal-table.md` first — it maps loose phrasing straight to a starting archetype/family. Use this to narrow which family of `modules/SUMMARY.md` rows to weigh most heavily, not as the final answer (it's "a starting point, not a lookup that skips judgment," per its own framing).

## 3. Shortlist from SUMMARY.md only

Read `modules/SUMMARY.md` — do not open individual `.html`/`.md` files at this stage. Score every row against the intake signals using its **Family**, **Best For**, **Avoid When**, and **Medium Fit** columns:

- A layout whose **Avoid When** matches the request, or whose **Medium Fit** explicitly flags a poor fit for the requested medium, is disqualified regardless of how well the rest fits.
- Prefer rows whose **Best For** directly names the content shape described.
- Use **Family** to break ties or diversify the top 3 rather than returning three near-identical archetypes from the same family.

Narrow to the top 3-5 candidates.

## 4. Confirm against full docs

Open only the shortlisted candidates' `layouts/<name>.md` files (not all 20) — read **Core Concept**, **When To Use**, and **When NOT To Use** to confirm the SUMMARY.md-level match holds up in detail, and pull one sentence of concrete reasoning for the final report. Drop any candidate that turns out to conflict on closer read; re-pull from the `modules/SUMMARY.md` shortlist if needed to backfill to 3.

## 5. Output

Report exactly 3 layouts, ranked, each with one concrete sentence of reasoning tied to the request (not a restated description):

```
1. **<name>** — <why this fits the specific request>
2. **<name>** — <why this fits>
3. **<name>** — <why this fits>
```

**Bonus pairing (optional, non-blocking):** for each of the 3, check its own `exampleThemePairings` field in `layouts/<name>.html`'s JSON (already loaded from step 4 — no extra file read needed). If a pairing exists, add one line: "Pairs well with the `<theme-name>` theme ([theme-factory]) — <why, from the field>." Omit entirely if the field is empty — never block or caveat the layout ranking on it.
