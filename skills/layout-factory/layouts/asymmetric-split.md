# asymmetric-split

**Archetype:** asymmetric-split · **Family:** grid-discipline

## Core Concept
Two columns run in parallel for the entire page length — an 8-of-12 dominant body and a 4-of-12 quiet rail — and never merge, stack, or box-and-shadow the rail into a competing element. The hierarchy mechanism is the ratio itself: 2:1, never 50/50. The tell that someone got it wrong: if the rail widens toward half the page, or gets boxed/shadowed like a card, it stops reading as marginalia and starts reading as a second column fighting the body for attention.

## When To Use
- Essays or opinion columns that want citations, related links, or running commentary to stay visible beside the argument instead of jumping to endnotes — the rail's whole point is that supporting material never has to be looked up separately.
- Analyst reports/research briefs with one dominant exhibit in the body and a textual glossary or caveat list running beside it in the rail.
- Documentation or product pages wanting a persistent "related pages" or spec-sheet rail beside the main content, as plain text, never thumbnails.

## When NOT To Use
- Content where the "supporting" material is actually just as important as the primary column — forcing a real second argument into the 4-column rail cramps it; use a genuine two-column layout (e.g. `two-column-academic`) instead.
- Anything needing per-line footnote anchoring — this archetype's rail runs parallel to a *section*, not pinned to one exact sentence; that precision belongs to `tufte-sidenote`.
- Chart-heavy content where a second chart would naturally belong in the rail — a chart at one-third width reads as a competing dashboard tile, not supporting marginalia; keep the rail textual only.

## Region / Component Guidance
- **masthead** (`1 / 13`, full width): small and quiet, sits above the split, never itself carries the 2:1 ratio. Don't inflate it into a hero — its only job is a section/identity label.
- **body** (`1 / 9`, always exactly 8 of 12 columns): the dominant argument. Gets the largest type, the page's only pull quote, and its only captioned exhibit. If you find content wanting a second pull quote or exhibit, that content probably belongs in a different archetype, not squeezed into this one's rail.
- **rail** (`9 / 13`, always exactly 4 of 12 columns): text-only, hairline-ruled entries — citations, related links, running notes, metric definitions. Never boxed or shadowed (that's the uniform-card-grid anti-pattern creeping back in). Runs the full length of the body beside it, not row-locked to it.

## Content-Type Notes
- **textHeavy**: body becomes continuous essay/narrative; rail becomes short running notes loosely tied to the section beside them (never pinned to one exact line — that's `tufte-sidenote`'s job, not this one's).
- **chartHeavy**: body carries the narrative plus the page's one dominant captioned exhibit; rail becomes metric definitions and data caveats — textual only, never a second chart.
- **cardOrListHeavy**: body holds the primary article/spec/list in running prose; rail becomes a "related"/"see also" list of plain text links with one-line descriptions — no thumbnails, no boxes.

## Medium Notes
- Print: the page margin literally becomes the rail — a real running margin column beside the main text block on every page, not footnotes collected at the bottom.
- Markdown has no native parallel-column mechanism — the ratio is lost entirely; rail content degrades to a trailing "Notes" or "Related" heading at the document's end, replacing the visual ratio with a location cue.
- Presentation: the 2:1 split becomes a permanent per-slide template zone (body = slide argument, rail = persistent citation/related panel) rather than one continuous scroll.

## Pairing Notes
- `bauhaus-geometry` — bold primary-color hierarchy and hard offset shadows give the body real visual weight while everything else stays flat; its own "shape should mean the content" logic maps directly onto argue-vs-support.
- `dead-letter-office` — postal marginalia (routing codes, rubber stamps) has always lived in a narrow column beside a letter; its typewriter register reads naturally as citations running down the rail.
- `verdigris-patina` — its own gimmick is structure communicating time top-to-bottom; here the 2:1 imbalance communicates emphasis left-to-right instead, brass body vs. quieter rail.
