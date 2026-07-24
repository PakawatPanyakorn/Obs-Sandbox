# Recommend Mode

Given free-text context about a project, suggest the top 3 best-fit existing themes with reasons — without opening all 43 preset files.

## 1. Intake

**With context** (project description, mood, medium, audience) → proceed straight to scoring.

**Without context** (bare `theme recommend`) → ask 1-2 clarifying questions, e.g.: "What's this for, and what mood should it carry?" Don't ask more than 2 — if the answer is still thin, proceed with what you have rather than interrogating the user.

Useful signals to listen for: content type (dashboard, portfolio, landing page, docs, dev tool), mood/tone words (serious, playful, warm, austere, loud, quiet), target medium, and anything explicitly ruled out ("not another dark-mode SaaS thing").

## 2. Shortlist from SUMMARY.md only

Read `modules/SUMMARY.md` — do not open individual `.html`/`.md` files at this stage. Score every row against the intake signals using its **Aesthetic**, **Personality**, **Tone**, **Best For**, and **Avoid When** columns:

- A theme whose **Avoid When** matches the request is disqualified regardless of how well the rest fits.
- Prefer rows whose **Best For** directly names the content type/genre described.
- Use **Tone**/**Aesthetic**/**Personality** to break ties or to rank when several themes technically fit the content type but differ in mood.

Narrow to the top 3-5 candidates.

## 3. Confirm against full docs

Open only the shortlisted candidates' `themes/<name>.md` files (not all 43) — read **Core Concept**, **When To Use**, and **When NOT To Use** to confirm the SUMMARY.md-level match holds up in detail, and pull one sentence of concrete reasoning for the final report. Drop any candidate that turns out to conflict on closer read; re-pull from the `modules/SUMMARY.md` shortlist if needed to backfill to 3.

## 4. Output

Report exactly 3 themes, ranked, each with one concrete sentence of reasoning tied to the request (not a restated description):

```
1. **<name>** — <why this fits the specific request>
2. **<name>** — <why this fits>
3. **<name>** — <why this fits>
```

**Bonus pairing (optional, non-blocking):** for the #1 theme, check `../layout-factory/modules/theme-pairing-log.md` for an existing pairing. If found, add one line: "Pairs well with the `<layout-name>` layout ([layout-factory]) — <why, from the log>." If layout-factory isn't installed/available or no pairing exists, omit this line entirely — never block or caveat the theme ranking on it.
