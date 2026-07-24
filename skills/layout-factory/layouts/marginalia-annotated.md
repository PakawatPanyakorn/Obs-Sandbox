# marginalia-annotated

**Archetype:** marginalia-annotated · **Family:** data-dense-report

## Core Concept
A running manuscript column paired with a dense gloss column that argues back — not sparse citations locked one-per-paragraph, but frequent claim-level commentary (challenge/clarify/query/agree) whose density tracks actual editorial attention. The gloss column free-flows in document order rather than row-locking to the paragraph it faces: several entries can stack beside one contentious sentence while other paragraphs carry none at all. That's the key distinction from `tufte-sidenote`, which anchors one note per paragraph on a fixed grid row.

## When To Use
- Draft manuscript review, editorial peer review, thesis/dissertation supervisor comments, legal or contract redlining — anywhere a reviewer argues with specific claims rather than leaving a general comments field.
- Analyst notes or research writeups under review, where methodology questions need to sit beside the exact claim they challenge.
- Requirements/spec documents under review or structured proposals with per-clause reviewer sign-off.

## When NOT To Use
- Sparse, reference-style citations that belong one-per-paragraph on a fixed grid — that's `tufte-sidenote`'s job, not this archetype's free-flowing claim-anchored commentary.
- Anywhere the instinct is to invent a gloss entry for every paragraph just to fill the column — an entry with no real claim behind it reads as decoration, same tell as a forced sidenote on every row.
- Content where the gloss column risks becoming a second column of mini-cards running parallel to the body — that recreates a two-column card grid wearing a margin-note costume; entries must stay plain text with hairline rules only.

## Region / Component Guidance
- **body** (`1 / 8`): the primary reading column — full sentence-level prose, section subheads, the document's single pull quote (styled deliberately *unlike* a gloss entry, so it's never mistaken for someone else's commentary), the flagship exhibit in chart-heavy content, a plain hairline list in card/list-heavy content.
- **sidenote** (`8 / 13`): dense, claim-anchored commentary — challenge/clarify/query/agree entries keyed to marked phrases in the body. Never a citation margin, never navigation. Free-flows in document order rather than sharing a locked grid row with a single paragraph, which is what lets density cluster where editorial attention actually was.

## Content-Type Notes
- **textHeavy**: full density — several stacked gloss entries per contentious paragraph, none at all where nobody flagged anything. Each entry categorized (challenge/clarify/query/agree), not left undifferentiated.
- **chartHeavy**: body keeps one numbered, captioned exhibit; gloss entries attach to specific claims about it (a methodology caveat, an excluded cohort, a causal-attribution question) — not running commentary on every sentence. Most exposed to dashboard-trope drift: every entry must name the specific claim or number it's challenging, never a floating caveat with nothing to anchor to.
- **cardOrListHeavy**: comparable items become a plain hairline-separated list in the body; gloss entries attach only to items that raised a question, items nobody flagged carry no entry.

## Medium Notes
- Print: a genuine critical-edition layout — the gloss column becomes the actual page margin, widened on the outer edge of each spread (recto/verso swap), dense enough to carry several stacked glosses per page like a scholarly apparatus criticus.
- Markdown: degrades to inline blockquote comments directly beneath the sentence they annotate (`> **[Challenge]** ...`) rather than collected in an endnote list — preserving the "commentary interrupts, right here" feeling, unlike a sparser citation archetype that wouldn't need to interrupt this way.
- Presentation: poor fit as a persistent two-column slide — convert each marked claim into its own annotated-quote slide (the claim as a large pull quote, its gloss entries as a comment list beneath), never force a standing margin column onto a slide master.

## Pairing Notes
- `rabbit-hole` — "falling down a rabbit hole of annotations" is literal here; Wonderland's own horror vacui makes a heavily-glossed manuscript feel like this theme's natural home.
- `vesper-furrow` — its own demo content is already land-register entries, parcel references, and surveyor notes against a formal record, a close sibling of reviewer commentary.
- `crypt-scholastic` — "dark gothic academic" with a rare-books register; a critical edition of an old manuscript, glossed by a scholar's hand, is exactly this theme's implied use case.
