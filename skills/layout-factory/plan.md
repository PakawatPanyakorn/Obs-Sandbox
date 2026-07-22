# layout-factory — plan & handoff

Written 2026-07-23 so a fresh session can continue this without re-deriving context. Read this file first if you're picking the work back up.

## Goal

The user's AI-assisted output (reports, analyses, presentations, articles, web pages) kept reading as "slop" — uniform card grids with no real composition. `layout-factory` is a companion skill to the existing `theme-factory` (which manages color/typography presets): it manages a browsable gallery of **structural** presets — grids, spacing, composition archetypes, editorial hierarchy — kept strictly separate from color/type so the two skills compose (layout sets the bones, theme skins them).

Workflow the user wants: (1) seed a gallery of layout presets organized by composition archetype, browsable and self-explaining, each previewable with real theme-factory skins; (2) once the gallery exists, reuse the same skill later in **apply mode** to restructure actual work (a report draft, an HTML page, a slide deck).

## Status: Phase 2 complete (10/10 presets), Phase 3 and verification not started

### Done
- Full skill scaffold: `skill.md`, all `modules/*.md`, `modules/preset-template.html`, `index.html` gallery shell.
- `magazine-well.html` — the first preset, iterated ~10 rounds directly with the user until approved. **This file (plus `modules/preset-template.html`) is the authoritative reference for every convention** — structure, CSS classes, the 4-view/4-theme tab picker, Full View button, full theme-token set, anti-pattern discipline. Read it before building anything else.
- All 10 Phase-2 archetypes built and live in the gallery (`index.html` LAYOUTS array + `modules/theme-pairing-log.md` both updated):
  - `magazine-well` (editorial-narrative)
  - `swiss-international-grid` (grid-discipline)
  - `single-column-editorial` (editorial-narrative)
  - `split-hero` (grid-discipline)
  - `dashboard-with-rail` (dashboard-legitimate)
  - `masthead-feature-river` (editorial-narrative)
  - `asymmetric-split` (grid-discipline)
  - `tufte-sidenote` (data-dense-report)
  - `data-dense-report-grid` (data-dense-report)
  - `two-column-academic` (grid-discipline)

### Not done yet
1. **Verify apply-mode** (from the original plan, never executed): test-apply one Phase-2 preset end-to-end against (a) an HTML target — Path F injection per `modules/apply-mode-html-implementation.md` — and (b) a non-HTML target — content-restructuring branch per `modules/apply-mode-restructure.md`, e.g. a Markdown report draft. Also confirm theme-factory coexistence: apply a theme-factory preset to the same HTML file (before or after the layout apply) and verify no token collisions in either direction. This should happen **before** Phase 3, since it's the real test of whether the schema/instructions actually work, not just whether the gallery looks good.
2. **Phase 3 — remaining 10 archetypes** (full descriptions in `modules/shared-composition-archetypes.md`, entries 11–20):
   - `marginalia-annotated` (data-dense-report) — main text + inline annotation column, denser/more review-commentary-oriented than tufte-sidenote's citation focus.
   - `bento-mosaic` (grid-discipline) — deliberately varied-size grid cells, valid ONLY when size maps to a real hierarchy signal, never decorative.
   - `timeline-river` (editorial-narrative) — chronological spine, alternating emphasis, for case studies/changelogs/retrospectives.
   - `card-catalogue-index` (grid-discipline) — the one legitimate "grid of items" case, expressed as a real table/aligned list, not decorative cards.
   - `poster-broadside` (grid-discipline) — single dominant typographic statement, scale-only hierarchy, for covers/section dividers/title slides.
   - `cover-and-contents` (editorial-narrative) — two-page pairing: full-bleed cover (poster-broadside) + structured TOC page.
   - `masonry-photo-essay` (editorial-narrative) — variable-height image blocks sized by real aspect ratio/narrative weight, for photo essays/galleries.
   - `slide-rule-of-thirds` (grid-discipline) — presentation-specific single-slide content layout (visual 1/3 + text 2/3), replaces the generic bullet-list slide.
   - `z-pattern-landing` (grid-discipline) — Z eye-scan path for marketing/landing pages driving toward one CTA; web-primary, doesn't translate to print/slides.
   - `slide-master-deck-grid` (grid-discipline) — deck-level meta-grid (fixed title/body/footer zones across every slide), pairs with a per-slide archetype like `slide-rule-of-thirds`.
3. **Optional, not yet requested**: expose the skill globally via junction (do not run without asking first):
   ```powershell
   New-Item -ItemType Junction -Path "C:\Users\pakaw\.claude\skills\layout-factory" -Target "Z:\GitHub\Obs-Sandbox\skills\layout-factory"
   ```

## The build recipe that worked (reuse this for Phase 3)

Building each preset by hand is slow and expensive; building all of Phase 2 sequentially would have taken far longer than doing it in parallel. This is what worked:

1. **Pre-assign theme pairings before dispatching**, matched by family/aesthetic fit, favoring **currently-unused** themes (see pool below) so the gallery doesn't lean on the same handful of themes repeatedly. Check `modules/theme-pairing-log.md` for what's already used.
2. **One general-purpose agent per archetype, dispatched in parallel** (multiple `Agent` tool calls in a single message, default background mode). Each agent's prompt must include, in full:
   - Required reading list: `modules/preset-template.html` (full file), `layouts/magazine-well.html` (full file, the quality bar), `modules/anti-patterns.md`, and the 2-3 real theme-factory theme files (full files, not just their JSON blocks — pull-quote and "alt card" conventions live in the markup, not the JSON).
   - The archetype's spec pasted directly from `modules/shared-composition-archetypes.md` (don't make the agent go find it).
   - Explicit instruction to design **new** archetype-specific CSS classes for the archetype's actual regions rather than reusing magazine-well's `.lf-lead`/`.lf-well` unless the region shape is genuinely the same.
   - Explicit instruction to copy the generic parts verbatim: the 3 end-of-body `<script>` blocks (view-tab toggle, theme-tab toggle, fullview toggle), the Full View CSS block, the `.lf-page` wrapper structure.
   - **DO NOT touch `modules/theme-pairing-log.md` or `index.html`** — parallel agents editing the same shared file races and corrupts it. Each agent writes only its own `layouts/<name>.html` and reports back its theme picks / regions / grid / density / anti-pattern result in a structured summary.
3. **After all agents report, consolidate centrally**: append rows to `theme-pairing-log.md` and entries to `index.html`'s `LAYOUTS` array yourself, in one pass, from the agents' structured reports.

### Gotcha: session/rate-limit false failures
Mid-Phase-2, 4 of 9 parallel agents hit the account's session usage limit and reported `status: failed`. Two of them had **already finished writing their file** — the failure happened while generating the final summary, after the real work was done. Before treating a "failed" agent as having produced nothing:
- `Glob` the `layouts/` directory to check if the file exists.
- If it does, check it's complete (`tail`/read the last ~20 lines for a proper `</html>` close, not a truncation).
- If complete, read the file's own `<script id="layout-data">` JSON block directly to recover the theme names, `why` reasoning (may need to reconstruct from the JSON's `exampleThemePairings[].why` field), regions, grid, and density — you don't need the agent's report if the file itself has everything.
- Only re-dispatch an agent for archetypes that truly have no file on disk.

## Theme pool bookkeeping

43 themes total in `skills/theme-factory/themes/`. 30 are used as of end of Phase 2 (3 on magazine-well + 27 across the 9 Phase-2 builds — full list in `theme-pairing-log.md`). **13 remain fully unused:**

`tokyo-screentone`, `moss-cottage`, `ultraviolet-rave`, `rabbit-hole`, `velvet-noir`, `astral-drift`, `acid-garden`, `solarpunk-utopia`, `synthwave-84`, `cosmica`, `copper-alchemist`, `nocturne-nouveau`, `biolumen-depths`

Phase 3 has 10 archetypes needing 2-3 pairings each (20-30 slots) but only 13 fully-fresh themes remain — **Phase 3 will necessarily reuse some already-used themes.** That's fine per the log's own guidance ("only repeat a theme when it's a strong fit for both"), but pick reuses deliberately: favor the 13 unused ones first, and when reuse is unavoidable, only reuse a theme for an archetype in a **different family** than where it was already used (avoids two similar-register archetypes converging on the same skin).

## File map

```
skills/layout-factory/
├── plan.md                               # this file
├── skill.md                              # mode dispatch (create/list/delete/apply) — stable, no changes needed since Phase 2
├── index.html                            # gallery — LAYOUTS[] array, update after every new preset
├── modules/
│   ├── preset-template.html              # skeleton + all house-style conventions in HTML comments — READ FIRST
│   ├── theme-pairing-log.md              # which theme-factory preset used in which layout preset + why — check before assigning new pairings
│   ├── anti-patterns.md                  # 4-category severity-tiered gate, run before finishing any preset or apply
│   ├── shared-composition-archetypes.md  # the master catalog — Phase 3 entries are #11-20
│   ├── apply-mode-restructure.md         # entry point for apply mode, medium-first dispatch (not yet exercised — see verification task)
│   ├── apply-mode-html-implementation.md # HTML/CSS-specific apply mechanics (not yet exercised)
│   └── (other shared-*.md modules — grid vocabulary, editorial devices, signal table, path A/B/C extraction)
└── layouts/
    └── <name>.html                       # one preset per archetype — 10 exist as of this writing
```
