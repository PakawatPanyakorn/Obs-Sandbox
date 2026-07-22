# Path A: Image Extraction

Extract a composition archetype from a screenshot of a layout (a webpage, a report page, a slide, a magazine spread).

## Steps

1. **Read the image** (vision).
2. **Segment into named regions** — identify masthead/nav, lead/hero, body columns, rail/sidebar, footer, and any exhibits (charts/tables/images) using the region-naming conventions in `modules/shared-grid-vocabulary.md`.
3. **Estimate grid structure**:
   - Count visible alignment lines (where multiple elements share a left/right edge) to estimate column count.
   - Estimate `gutter` from the visible gap between aligned columns.
   - Estimate `maxWidth`/`marginInline` from how far content sits from the image edges.
   - Note whether spacing looks consistent (grid discipline) or ad hoc.
4. **Identify hierarchy** — what's biggest/boldest/most isolated first, second, third. Read `modules/shared-editorial-devices.md` → "Establishing hierarchy through structure alone" for the levers to check (scale, position, span, grouping).
5. **Check for visible editorial features** — pull quotes, captions, footnotes/sidenotes, callouts, section breaks, drop caps. Read `modules/shared-editorial-devices.md` for the full catalog.
6. **Map to the nearest catalog archetype** — read `modules/shared-composition-archetypes.md`. If the image doesn't cleanly match one entry, note it as a hybrid (e.g. "magazine-well with a Tufte-style sidenote column") rather than forcing a false match.
7. **Fill gaps with context** — if the image alone doesn't clarify intent (e.g. is this meant for print or web?), read `modules/shared-signal-table.md` and/or ask.
8. **Name** — ask the user, unless operating in an unattended/"all" batch extraction, in which case derive a descriptive slug from the matched archetype (e.g. `magazine-well-sidenote-hybrid`).
9. **Anti-pattern gate** — read `modules/anti-patterns.md`. Before writing, silently fix anything the source image itself got wrong (e.g. if the screenshot shows a uniform card grid being extracted, don't preserve that specific flaw in the preset — extract the underlying archetype it was reaching for, or ask).
10. **Write** using `modules/preset-template.html`, `source: "screenshot"`, `sourceFile: "<path>"` → update `index.html` LAYOUTS array.

## Notes

- Screenshots of your own past work (the "slop" you're trying to move away from) are valid extraction sources too — but flag if the source itself exhibits an anti-pattern, and ask whether to extract the flawed structure as-is (for reference/comparison) or the corrected version.
- Multiple distinct compositions in one image (e.g. a full page containing both a hero section and a card-grid footer) → run the multi-layout check from `skill.md` Step 2 before proceeding.
