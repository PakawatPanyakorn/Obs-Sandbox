# Apply Mode: Restructure (entry point, medium-agnostic)

This is the first file to read for every apply. It covers the judgment work that's the same regardless of where the result ends up, then dispatches to the medium-specific branch.

## 1. Determine target medium

| Target | Branch |
|---|---|
| An existing HTML/CSS file | **HTML branch** — do the content-mapping below, then read `modules/apply-mode-html-implementation.md` for the CSS/markup mechanics |
| Existing Markdown/plain-text draft, or "help me write/structure this as a report/article" with no file, or any non-HTML document | **Content-restructuring branch** (this file, §3) |
| A presentation/slide request | **Slide-structuring branch** (this file, §4) |

All three read from the **same preset** — `composition`, `grid`/`spacing` (HTML branch only), `editorialFeatures`, and `mediaAdaptation`. One preset serves every medium; that's why the gallery is seeded by archetype, not by use-case.

## 2. Content-mapping judgment (do this first, all branches)

Before touching the target's format, decide the structural mapping:

1. **Audit the existing or planned content** — what sections/topics/claims/data exist, in what order, of what length, and which of three mixes it's closest to: mostly prose, mostly charts/tables/exhibits, or a set of comparable items (a card/list shape). Real content is often a blend — note the dominant mix.
2. **Read the preset's `contentTypeVariants` field** (`textHeavy` / `chartHeavy` / `cardOrListHeavy`) and use whichever entry matches the dominant mix from step 1 as the concrete basis for region assignment — it already specifies how this archetype's regions adapt, what the content is best suited for, and what to avoid for that mix (usually: don't let a chart-heavy adaptation drift into a dashboard, or a card-heavy one into a uniform grid).
3. **Assign content to the preset's `composition.regions`** per the matched variant — which passage becomes `lead`, which becomes `river` entries, what (if anything) belongs in `rail`/`sidenote`. If the target has more or less content than the archetype's region count assumes, adapt the count rather than forcing a mismatch (e.g. three findings into a two-region archetype → either add a region of the same kind, or pick the next-closest archetype).
4. **Assign hierarchy** — decide what's genuinely `primary`/`secondary`/`tertiary` per `composition.hierarchy`, using the levers in `modules/shared-editorial-devices.md` ("Establishing hierarchy through structure alone"). This is a judgment call about the *content*, not a mechanical copy of the preset's example hierarchy.
5. **Select editorial devices** — per `modules/shared-editorial-devices.md` → "Selecting devices for a given piece of content." Only add a pull quote, sidenote, footnote, etc. if the actual content earns it — don't apply the preset's full device list decoratively.
6. **Set `readingOrder` and `entryPoint`** for this specific content.

This mapping is what actually solves "my output is slop" — the CSS/markup or prose formatting that follows is just the expression of a decision already made here.

## 3. Content-restructuring branch (Markdown / plain-text / prose targets)

No CSS. Express the mapping from §2 directly in the target's native format:

| Region/device | Markdown/prose expression |
|---|---|
| `masthead` | Title + subtitle/byline block at the top |
| `lead` | Opening section, given a full heading and the most space |
| `river` | A sequence of smaller subsections, each a shorter heading + shorter body |
| `rail` / `sidenote` | A clearly marked aside — blockquote, a "Note:" callout, or (if the renderer supports footnote syntax) an actual footnote |
| Pull quote | Blockquote (`>`) set apart from surrounding prose |
| Callout | Bolded lead-in or a blockquote styled as a note/warning |
| Footnote | Numbered reference + an endnote list at the document's end |
| Section break | A horizontal rule (`---`) or a clear heading-level jump, not identical spacing throughout |
| Numbering | `1.`, `2.` on sections/figures only if the document is long/structured enough to warrant cross-reference |

Consult the preset's `mediaAdaptation.markdown` field for archetype-specific notes (written when the preset was created) before improvising.

Output the restructured content directly — this branch produces prose/Markdown, not a code file.

## 4. Slide-structuring branch

Propose a per-slide layout using the preset's slide-relevant fields:

1. If the preset is a **deck-level** archetype (`slide-master-deck-grid`) — apply its fixed title/body/footer zone margins across every slide, then pick a **per-slide content archetype** (commonly `slide-rule-of-thirds` or `poster-broadside` for title/section slides) for each slide's internal content.
2. If the preset is a **single-slide content** archetype (`slide-rule-of-thirds`, `poster-broadside`) — apply it per slide directly.
3. Map content: one idea/finding/section per slide, following the region assignment from §2 — resist compressing a `river` of 5 findings onto one dense slide; one slide per `river` entry is usually correct for presentations even when it wouldn't be for a web page.
4. Consult `mediaAdaptation.presentation` for archetype-specific notes.
5. Output format matches what the user is authoring in — a slide outline (heading per slide + bullet notes), or actual slide markup (reveal.js HTML — hand off to `modules/apply-mode-html-implementation.md` for that specific case since it is HTML — or Markdown-slide syntax).

## 5. Anti-pattern audit (all branches)

Read `modules/anti-patterns.md` and run the full checklist (all 4 categories + medium-mismatch) against the result before reporting. This catches both authoring flaws and medium-mismatch specifically — check the "medium mismatch" row against whichever branch was used.

## 6. Report

```
Applied layout <name> to <target>

Archetype:                <name> (<family>)
Branch:                    html | content-restructuring | slide-structuring
Regions mapped:            <N> — <region: content-source mapping list>
Hierarchy:                 primary=<region/content>, secondary=<region/content>
Editorial devices added:   pull quotes: N, callouts: N, sidebars/sidenotes: N, footnotes: N
Grid system:               <columns-col / gutter / maxWidth container, if HTML branch>
Anti-pattern audit:        <pass | N issues fixed: list>
Medium adaptation used:    <mediaAdaptation field consulted>

Manual review needed: <e.g. content that didn't map cleanly to the region count,
images needing recropping, tables not yet reflowed, breakpoints not verified>
```
