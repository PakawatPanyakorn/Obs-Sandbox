# layout-factory — plan & handoff

Written 2026-07-23 so a fresh session can continue this without re-deriving context. Read this file first if you're picking the work back up.

## Goal

The user's AI-assisted output (reports, analyses, presentations, articles, web pages) kept reading as "slop" — uniform card grids with no real composition. `layout-factory` is a companion skill to the existing `theme-factory` (which manages color/typography presets): it manages a browsable gallery of **structural** presets — grids, spacing, composition archetypes, editorial hierarchy — kept strictly separate from color/type so the two skills compose (layout sets the bones, theme skins them).

Workflow the user wants: (1) seed a gallery of layout presets organized by composition archetype, browsable and self-explaining, each previewable with real theme-factory skins; (2) once the gallery exists, reuse the same skill later in **apply mode** to restructure actual work (a report draft, an HTML page, a slide deck).

## Status: Phase 2 complete (10/10 presets), apply-mode verified, Phase 3 complete (20/20 presets)

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

### Apply-mode verification — done 2026-07-24

Ran the full loop end-to-end in a scratch dir (not committed — throwaway test fixtures, not gallery content) before starting Phase 3, per the original plan's ordering:

1. **HTML target, Path F** — applied `asymmetric-split` to a bare analyst-note HTML page (no theme-factory, no layout-factory markers). Content-mapping: prose intro + finding → `body` (8/12), supporting-signals list + citations → `rail` (4/12, hairline-ruled), one sentence promoted to a real `<blockquote>` pull quote. Injected the `--layout-*` token block + signature comment + `data-layout` attribute, `grid-template-areas` matching region ids, `data-region` attributes, a real `@media` breakpoint collapsing to single column. **Caught a real bug in my own first pass**: introduced a new hardcoded `#d8d8d8` for rule colors instead of reusing the file's existing `#ccc`/`#222` — exactly the "no inline hardcoded values introduced while restructuring" check in `apply-mode-html-implementation.md`'s verification section exists to catch. Fixed before finalizing. Conclusion: **the instructions work as written**, including catching a mistake a careless apply would ship.
2. **Theme-factory coexistence** — applied `bauhaus-geometry` (theme-factory) Path F to the *same* file, in the recommended layout-then-theme order. Added a second `:root` block under its own `/* Theme: ... - applied by obs-theme-factory */` marker, left the `--layout-*` block untouched, remapped hardcoded colors/fonts in the shared markup (masthead rule, rail borders, citation font, pull-quote border) to the new theme's tokens pulled from the real `bauhaus-geometry.html` file. Verified by grep: both signature comments present, zero variable-name overlap between `--layout-*` and `--color-*`/`--font-*`/etc namespaces. **Conclusion: coexistence works as designed** — but see gap noted below.
3. **Markdown target, content-restructuring branch** — applied `data-dense-report-grid` (chartHeavy variant) to a plain-prose investor-letter draft with inline stats and an end-of-doc source list. Remapped to `brief` (opening thesis + the archetype's required one pull-quote-in-the-brief, which I initially omitted and had to add back after re-checking the preset's own `editorialFeatures.pullQuotes` field) + `exhibit-stream` (4 numbered `## Fig. N — Caption` sections, each a real Markdown table followed by a commentary paragraph, per the preset's own `mediaAdaptation.markdown` note) + one occasional sidenote-style `> **Note:**` callout attached to the exhibit it cites (not a persistent rail, per this archetype's citation convention). Conclusion: **content-restructuring branch works as written**, including the "don't skip a field just because it wasn't in the first draft" discipline.

**One real gap found, left as a follow-up, not blocking**: `apply-mode-html-implementation.md`'s coexistence section is written entirely from layout-factory's point of view ("if theme-factory present, don't touch its block"). `skills/theme-factory/`'s own skill.md and modules have **zero mention of layout-factory** — grepped the whole directory, no hits. In practice this doesn't cause a collision today (disjoint token namespaces, theme-factory only ever touches color/font/shadow/radius properties), but if theme-factory's harmonize steps (4a-4k) were ever extended to touch spacing or layout-ish properties, nothing on that side would tell it to leave a `data-region`/`grid-template-areas` block alone. Worth a one-line addition to theme-factory's own apply-mode docs at some point; not urgent since the current instructions produce zero actual collisions.

### Phase 3 — done 2026-07-24 (10/10 archetypes)

Built via the parallel-agent recipe below, one general-purpose agent per archetype, all dispatched in a single batch. All 10 landed clean on the first pass — no truncated files, no re-dispatches needed. `theme-pairing-log.md` and `index.html`'s `LAYOUTS` array were then updated centrally, in one pass, from the agents' structured reports (never by the agents themselves). Full descriptions were entries 11–20 in `modules/shared-composition-archetypes.md`:

- `marginalia-annotated` (data-dense-report) — main text + dense claim-level gloss column, deliberately denser/more review-commentary-oriented than tufte-sidenote's sparse citation focus. Themes: `rabbit-hole`, `vesper-furrow`, `crypt-scholastic`.
- `bento-mosaic` (grid-discipline) — deliberately varied-size grid cells; legitimacy enforced via an explicit "shuffle test" (if you can rearrange tiles without changing the meaning, it's decorative, not bento) baked into the Concept tab itself, not just asserted. Themes: `acid-garden`, `cosmica`.
- `timeline-river` (editorial-narrative) — literal vertical spine, river entries alternating left/right, exactly one entry promoted to pivotal scale. Themes: `biolumen-depths`, `copper-alchemist`.
- `card-catalogue-index` (grid-discipline) — the one legitimate "grid of items" case, expressed as a real `<table>` with hairline rules, never boxes. Themes: `moss-cottage`, `alpha-signal`.
- `poster-broadside` (grid-discipline) — single dominant typographic statement, scale-only hierarchy, for covers/section dividers/title slides. Themes: `velvet-noir`, `astral-drift`.
- `cover-and-contents` (editorial-narrative) — two-page pairing: full-bleed cover + structured numbered TOC page, separated by a literal page-break seam. Themes: `nocturne-nouveau`, `embassy-gold`. (Built before `poster-broadside` landed, so its cover page uses its own fresh `.lf-cover-*` classes rather than `poster-broadside`'s `.lf-broadside` — cosmetic naming divergence only, not a functional issue, since presets are self-contained files.)
- `masonry-photo-essay` (editorial-narrative) — variable-height image blocks sized by real aspect ratio/narrative weight (explicitly distinguished from bento-mosaic's importance-driven sizing). Themes: `tokyo-screentone`, `verdigris-patina`.
- `slide-rule-of-thirds` (grid-discipline) — presentation-specific single-slide content layout (visual 1/3 + text 2/3), replaces the generic centered bullet-list slide. Themes: `synthwave-84`, `ultraviolet-rave`.
- `z-pattern-landing` (grid-discipline) — Z eye-scan path for marketing/landing pages driving toward one CTA; honestly marked web-primary, doesn't translate to print/slides. Themes: `solarpunk-utopia`, `eigenvalue`.
- `slide-master-deck-grid` (grid-discipline) — deck-level meta-grid (fixed title/body/footer zones across every slide), demoed with 2-3 mini slide mockups proving identical zoning holds while body content varies; pairs with a per-slide archetype like `slide-rule-of-thirds`. Themes: `vault-theorem`, `thermal-fade`.

All 20 presets (Phase 2 + Phase 3) are now live in `index.html`'s `LAYOUTS` array with `tags` chosen from the fixed vocabulary, and every pairing above is logged in `modules/theme-pairing-log.md`.

### Optional, not yet requested

Expose the skill globally via junction (do not run without asking first):
```powershell
New-Item -ItemType Junction -Path "C:\Users\pakaw\.claude\skills\layout-factory" -Target "Z:\GitHub\Obs-Sandbox\skills\layout-factory"
```

## Gallery conventions added after Phase 2 shipped (already baked into every existing file — just don't break them)

Since the Phase-2 write-up above, `index.html` and every file in `layouts/` (plus `modules/preset-template.html`) picked up two additions. Both are already present everywhere as of this writing — nothing to retrofit — but Phase 3 presets must keep doing both:

1. **Live iframe thumbnails via `?fullview=1`.** `index.html`'s gallery cards no longer show an abstract region diagram — each card embeds `<iframe src="${filename}?fullview=1">`, scaled down, showing the actual rendered preset. This requires every preset file to read its own URL on load: if `location.search` matches `/[?&]fullview=1/`, add both `lf-fullview` and `lf-embed` to `<body>` and set the Full View button's text to "Exit Full View" immediately (no click needed). `lf-embed` additionally hides the Full View button itself via `body.lf-embed .lf-fullview-toggle { display: none; }` (no interactive affordance needed inside a non-interactive thumbnail). This is already in `preset-template.html`'s script/CSS — if you copy the template's fullview block verbatim (as instructed below), you get this for free. Don't strip it out.
2. **A `tags` facet with a controlled vocabulary.** Every `index.html` LAYOUTS entry now carries a `tags: [...]` array (job/use-case labels, not part of the preset's own JSON schema — it lives only in the gallery mirror). The vocabulary is fixed in `index.html`'s `JOB_TAG_LABELS`: `essay-long-form`, `analyst-report`, `academic-research`, `documentation-reference`, `dashboard-analytics`, `newsletter-digest`, `marketing-landing`, `portfolio-showcase`. When consolidating a new preset into `index.html`, pick 2-3 of these that genuinely fit (don't invent new tag strings — the "Best for" filter row only renders labels from this fixed map, so an unrecognized tag value silently won't get a filter chip).

## The build recipe that worked (reuse this for Phase 3)

Building each preset by hand is slow and expensive; building all of Phase 2 sequentially would have taken far longer than doing it in parallel. This is what worked:

1. **Pre-assign theme pairings before dispatching**, matched by family/aesthetic fit, favoring **currently-unused** themes (see pool below) so the gallery doesn't lean on the same handful of themes repeatedly. Check `modules/theme-pairing-log.md` for what's already used.
2. **One general-purpose agent per archetype, dispatched in parallel** (multiple `Agent` tool calls in a single message, default background mode). Each agent's prompt must include, in full:
   - Required reading list: `modules/preset-template.html` (full file), `layouts/magazine-well.html` (full file, the quality bar), `modules/anti-patterns.md`, and the 2-3 real theme-factory theme files (full files, not just their JSON blocks — pull-quote and "alt card" conventions live in the markup, not the JSON).
   - The archetype's spec pasted directly from `modules/shared-composition-archetypes.md` (don't make the agent go find it).
   - Explicit instruction to design **new** archetype-specific CSS classes for the archetype's actual regions rather than reusing magazine-well's `.lf-lead`/`.lf-well` unless the region shape is genuinely the same.
   - Explicit instruction to copy the generic parts verbatim: the 3 end-of-body `<script>` blocks (view-tab toggle, theme-tab toggle, fullview toggle), the Full View CSS block, the `.lf-page` wrapper structure.
   - **DO NOT touch `modules/theme-pairing-log.md` or `index.html`** — parallel agents editing the same shared file races and corrupts it. Each agent writes only its own `layouts/<name>.html` and reports back its theme picks / regions / grid / density / anti-pattern result in a structured summary.
3. **After all agents report, consolidate centrally**: append rows to `theme-pairing-log.md` and entries to `index.html`'s `LAYOUTS` array yourself, in one pass, from the agents' structured reports. Each new `LAYOUTS` entry also needs a `tags: [...]` array — pick 2-3 from the fixed vocabulary in the section above.

### Gotcha: session/rate-limit false failures
Mid-Phase-2, 4 of 9 parallel agents hit the account's session usage limit and reported `status: failed`. Two of them had **already finished writing their file** — the failure happened while generating the final summary, after the real work was done. Before treating a "failed" agent as having produced nothing:
- `Glob` the `layouts/` directory to check if the file exists.
- If it does, check it's complete (`tail`/read the last ~20 lines for a proper `</html>` close, not a truncation).
- If complete, read the file's own `<script id="layout-data">` JSON block directly to recover the theme names, `why` reasoning (may need to reconstruct from the JSON's `exampleThemePairings[].why` field), regions, grid, and density — you don't need the agent's report if the file itself has everything.
- Only re-dispatch an agent for archetypes that truly have no file on disk.

## Theme pool bookkeeping

43 themes total in `skills/theme-factory/themes/`. **All 43 have now been used at least once** as of end of Phase 3 (30 across Phase 2 + magazine-well, the remaining 13 previously-unused ones — `tokyo-screentone`, `moss-cottage`, `ultraviolet-rave`, `rabbit-hole`, `velvet-noir`, `astral-drift`, `acid-garden`, `solarpunk-utopia`, `synthwave-84`, `cosmica`, `copper-alchemist`, `nocturne-nouveau`, `biolumen-depths` — each spent exactly once across Phase 3). 8 themes were deliberately reused across a different family than their original pairing (`vesper-furrow`, `crypt-scholastic`, `alpha-signal`, `embassy-gold`, `verdigris-patina`, `eigenvalue`, `vault-theorem`, `thermal-fade` — see `theme-pairing-log.md` for the specific `why` on each reuse). Full pairing list, 51 rows total, lives in `theme-pairing-log.md`.

If the catalog grows again in a future phase, every theme has now been used at least once — pick the reuse candidate that's the strongest genuine fit for the new archetype rather than defaulting to "least-used," per the log's own guidance.

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
│   ├── apply-mode-restructure.md         # entry point for apply mode, medium-first dispatch — verified 2026-07-24, see "Apply-mode verification" above
│   ├── apply-mode-html-implementation.md # HTML/CSS-specific apply mechanics — verified 2026-07-24
│   └── (other shared-*.md modules — grid vocabulary, editorial devices, signal table, path A/B/C extraction)
└── layouts/
    └── <name>.html                       # one preset per archetype — all 20 catalog archetypes exist as of this writing
```

## Status as of 2026-07-24: everything in this plan is done

Both outstanding items from the original handoff (apply-mode verification, Phase 3's remaining 10 archetypes) are complete. What's left is optional and not yet requested: the global-junction step above, and the one documentation gap noted in the apply-mode verification section (adding a layout-factory-awareness note to theme-factory's own apply-mode docs). Neither blocks anything — the skill is fully seeded and apply mode is confirmed working end-to-end.
