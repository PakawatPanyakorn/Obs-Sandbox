# cover-and-contents

**Archetype:** cover-and-contents · **Family:** editorial-narrative

## Core Concept
A ceremonial two-page opening — a full-bleed title cover, then a flatter numbered contents index, separated by a literal page-break seam. The seam is what makes this two committed pages, not one scroll with a big headline at the top. Only the cover ever receives the theme's hero gradient/shadow; the contents page stays flat by rule.

## When To Use
- Long-form reports, whitepapers, board memos, research monographs — any document that argues something across multiple sections and benefits from the reader knowing the shape before starting.
- Quarterly reviews or analyst reports needing a title page followed by both a section index and a numbered "Figures" index for exhibits readers will flip to by number.
- Vendor shortlists, board packets, or portfolio/case-study indexes formal enough to warrant a cover page in front of a comparison list.

## When NOT To Use
- Short content, or content that doesn't need the reader to know its shape before starting — the ceremonial two-page opening is overhead a single-page piece doesn't need.
- Anywhere the instinct is to pad the contents list to look fuller — five honest sections beat nine invented ones; the same restraint applies to adding cover artwork just to fill space when the content is text-only.
- Contents lists that want to become a 3-up card grid once entries reach the page — the numbered list *is* the structure; boxing entries duplicates the numbering and reintroduces the uniform-card tell.

## Region / Component Guidance
- **cover** (full-bleed, `1 / 13`): kicker, headline, attribution — nothing else. The only region that gets the theme's hero gradient/shadow at full strength. One pull quote is allowed here (echoing a book jacket blurb), styled large italic with a left rule, no quotation marks.
- **seam** (`1 / 13`): a literal page-break indicator — dashed rule plus folio numbers. Chrome-only structural marker, not a content region; needs a full section-gap so it reads as a genuine page break, not a mere section divider.
- **contents** (`1 / 13`): a numbered/sectioned table-of-contents index, deliberately flatter register than the cover — restraint, not oversight. Entries are a hairline-rule list with dot leaders, never boxed cards, even in the card/list-heavy variant.

## Content-Type Notes
- **textHeavy**: contents runs narrative sections in argument order (Executive Summary → Recommendation) each with a one-line descriptor; cover drops any visual apparatus — kicker + headline + dek + attribution only.
- **chartHeavy**: contents page gains a second, smaller "Figures" index beneath the section list, each exhibit numbered and one-line captioned (same discipline as `magazine-well`'s well entries) — never bare numbers with no caption. Cover itself stays purely typographic.
- **cardOrListHeavy**: contents entries become the comparable items themselves (candidates, vendors, portfolio pieces) rather than chapter names — still a numbered, hairline-rule list with variable-length descriptions, never uniform cards.

## Medium Notes
- Print: a literal two-page pairing — page 1 has no running header/footer (full bleed), page 2 gets real page numbers and folio marks in the running header, with `page-break-before: always` on the contents page.
- Markdown: page 1 becomes an H1 + italic kicker sub-line + attribution as a horizontal rule; page 2 becomes an ordinary numbered list of section headings — since dot leaders and page numbers don't survive, each entry's one-line description is what preserves the "annotated contents" feel.
- Presentation: page 1 becomes the deck's title slide; page 2 becomes the agenda slide with descriptions dropped to titles only.

## Pairing Notes
- `nocturne-nouveau` — ornate, formal Art Nouveau register reads as ceremonial front matter; the dark radial-nebula hero and dramatic elevation shadow give the cover real weight without needing a photo.
- `embassy-gold` — its own "institutional cover-page authority" framing is a direct fit; navy/gold restraint and Cormorant display read as board-document gravitas.
