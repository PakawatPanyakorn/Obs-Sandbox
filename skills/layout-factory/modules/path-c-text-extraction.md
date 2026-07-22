# Path C: Text / Named-Archetype Extraction

Handles two distinct entry points: a **named archetype request** ("give me a Swiss grid layout") and a **loose description** ("I want something that feels like the Economist"). No visual or markup source is available, so this path leans hardest on the shared reference modules.

## Intent resolution

1. **Named archetype given** (matches or closely resembles an id/name in `modules/shared-composition-archetypes.md`) → resolve directly against that catalog entry. Use its structural summary, regions, and hierarchy as the preset's basis; don't re-derive from scratch.
2. **Loose description** (a feel, a comparison, a mood — "like a consulting report", "data-dense but readable") → read `modules/shared-signal-table.md` to map to a starting archetype, then verify the full entry in `modules/shared-composition-archetypes.md` before committing.
3. **No context at all** ("make me a layout", or a bare request with no medium/content clues) → **ask** before picking an archetype:
   - What medium(s) will this target — report, presentation, article, web, or several?
   - What shape is the content — long-form prose, mixed exhibits/charts, a parallel set of items, chronological entries, reference/lookup material?

   Only pick an archetype once you have real signal on at least one of these. Do not default to a card grid or a dashboard archetype when signal is absent — per the decision aid at the end of `shared-composition-archetypes.md`, default to `single-column-editorial` or `asymmetric-split` if genuinely forced to choose with minimal information, and say so.

## Steps

1. Resolve intent per above.
2. Read `modules/shared-grid-vocabulary.md` to flesh out concrete `grid`/`spacing` values (the archetype entry gives structural intent, not exact pixel/column numbers).
3. Read `modules/shared-editorial-devices.md` to decide which editorial devices this archetype/content combination actually earns — don't apply every device listed for the archetype if the content doesn't support it (e.g. no citations → no footnotes, even if the archetype commonly uses them).
4. Fill `mediaAdaptation` for every medium the user mentioned, or that the archetype is known to fit well (each catalog entry notes its medium fit) — leave a mismatched medium's field honestly noting the mismatch rather than forcing an adaptation that won't work.
5. **Name** — ask if not provided. Prefer archetype-descriptive names (`swiss-international-grid`, `masthead-feature-river`) over decorative ones, so the gallery stays scannable by structure rather than by vibe.
6. **Anti-pattern gate** — read `modules/anti-patterns.md`. Since this path has no source material to check against, the gate here is mostly about not over-decorating: don't add editorial devices, regions, or grid complexity beyond what the resolved intent actually calls for.
7. **Write** using `modules/preset-template.html`, `source: "text"` or `"archetype-request"`, `sourceFile: ""` → update `index.html` LAYOUTS array.

## Notes

- This path is the most common entry point for the initial gallery-seeding pass (building the ~20-archetype catalog upfront) — each seed preset is a Path C "named archetype request" against the catalog entry of the same name.
- When seeding from the catalog, resist adding invented flourishes not present in the catalog entry — the catalog descriptions in `shared-composition-archetypes.md` are the source of truth; the preset should express them faithfully, not embellish them.
