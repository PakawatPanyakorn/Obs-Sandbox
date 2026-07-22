# Shared Editorial Devices & Hierarchy Techniques

Reference for filling `editorialFeatures` in a preset, for the "no editorial structure" anti-pattern check, and for establishing hierarchy structurally (without relying on color/font — that stays theme-factory's job).

## Establishing hierarchy through structure alone

Hierarchy is a structural property, not a color/weight property, in layout-factory's scope. Available levers, roughly in order of strength:

1. **Scale/isolation** — the single most reliable signal. Give the primary element more space and fewer neighbors than anything else on the page. A `lead` region surrounded by whitespace reads as important before a reader processes a single word.
2. **Position** — content near the top-left (in LTR reading contexts) or at a Z-pattern's anchor points reads first. Use `readingOrder` and `entryPoint` to make this explicit rather than accidental.
3. **Column span / width** — a region spanning 8 of 12 columns reads as more important than one spanning 3, independent of anything else.
4. **Grouping/proximity** — related items placed close together and separated from unrelated items read as one unit; this is how a `river` reads as "the secondary stories" versus the `lead`.
5. **Repetition-with-variation** — a repeated pattern (e.g. `river` entries) with one deliberate break (a `lead` that doesn't follow the pattern) draws attention to the break.

`composition.hierarchy` (`primary`/`secondary`/`tertiary`) should be decided using these levers, and every region in `composition.regions` should trace back to a hierarchy level.

## Editorial devices catalog

| Device | What it is | When to use | Structural implementation notes |
|---|---|---|---|
| **Pull quote** | A short, quotable excerpt from the body text, pulled out and set larger/isolated | Long-form text (>~400 words) with at least one genuinely quotable line | Break the text column, insert as its own block spanning part or all of the column width; in `mediaAdaptation.markdown`, express as a styled blockquote |
| **Sidebar** | A bounded secondary zone running alongside the main content | Supporting info that's genuinely tangential (related links, definitions, a short bio) — not a dumping ground for content that just didn't fit | Use the `rail` region; keep it narrower than the main content column, never equal-width |
| **Callout** | An inline emphasized block within the main flow (warning, tip, key-takeaway) | A single important point that needs to interrupt the reading flow briefly | Full-width-of-column block, minimal but present visual separation (border or rule, not necessarily a filled box) |
| **Footnote** | A numbered reference resolved at the bottom of the page/document | Citations, sources, tangential clarifications that shouldn't interrupt reading | End-of-document list; number inline in `body` |
| **Sidenote** | A footnote displayed in the margin next to its anchor paragraph, not at the document end | Same content as a footnote, but for mediums with margin space (see `tufte-sidenote` archetype) — removes the "flip to the end" cost | Requires a dedicated `sidenote` region with per-paragraph vertical alignment to its anchor |
| **Section break** | A visual marker that a new section/topic is starting | Every top-level topic change in a document of meaningful length | Vary by archetype: a horizontal rule, a numeral, an ornament, or simply a larger-than-normal whitespace gap — never identical treatment to a normal paragraph gap |
| **Drop cap** | An enlarged first letter of a section's opening paragraph | Editorial/essay archetypes wanting a classic, considered opening signal | Single use per section max; never on every paragraph |
| **Caption** | Text identifying/describing a figure, image, or exhibit | Any `exhibit` region | Position and style should be consistent across all exhibits in one document — this consistency is itself a discipline signal |
| **Numbering** | Sequential numbers on sections and/or figures | Reports and data-dense documents where readers need to reference "Figure 3" or "Section 2.1" | Only commit to numbering if the document is long/structured enough to benefit — numbering a 3-section memo is noise |

## Selecting devices for a given piece of content

Don't apply every device to every document — that's its own kind of slop (decorative device-stacking). Pick devices the content actually earns:

- Text has a genuinely quotable line → pull quote. Doesn't → skip it, don't manufacture one.
- Content has real citations/sources → footnote or sidenote (sidenote if the archetype has margin space, footnote otherwise). No sources → neither.
- Document has 3+ clearly distinct topic sections → section breaks. Fewer → skip, a plain heading is enough.
- Numbers only when the document is long/structured enough that cross-referencing ("see Figure 2") is plausible.

The anti-pattern gate's "no editorial structure" check exists to catch *under*-use of these devices on content that clearly warrants them (long text with no pull quote, cited claims with no footnote) — not to mandate every device on every document.
