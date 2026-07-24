# poster-broadside

**Archetype:** poster-broadside · **Family:** grid-discipline

## Core Concept
A single dominant typographic statement fills the page — hierarchy comes entirely from scale contrast between one giant headline and, at most, one small supporting line. No boxes, no color, no secondary content, no third region. The moment a second real idea needs its own region or box, this archetype has been outgrown — that constraint is deliberate, not an oversight.

## When To Use
- Chapter title pages, section dividers inside a long report or book, a single declarative section name between long-form pages.
- A deck's opening title slide built around one headline statistic, or a report cover page stating its single most important finding before exhibits begin.
- A category-divider page inside a catalogue/index, a "Part Two" interstitial, or a single-item spotlight cover with no comparison list attached.

## When NOT To Use
- Anywhere the support line risks growing into a paragraph "just this once" — a title page that argues a point has stopped being a title page; use `single-column-editorial` or `magazine-well`'s text variant for actual prose.
- Chart-heavy content wanting an actual chart, axis, or data table on the page — that turns a cover page into a report page wearing a poster's typography; real exhibits belong on `magazine-well`'s chartHeavy variant.
- Markdown as the primary target — markdown has no mechanism for scale contrast, so this archetype collapses to an indistinguishable plain H1; reserve it for HTML, slide, or print output only.

## Region / Component Guidance
- **lead** (`1 / 13`, centered): the single dominant typographic statement, the entire reason the page exists. Largest type on the page; nothing else competes with it in size.
- **support** (`4 / 11`, optional): a radically smaller supporting line — a date, edition mark, scope note, or one sentence of context. Omit entirely for a pure title-only page; never grows past one short line. If you find yourself wanting two items of equal weight on this page, that breaks the single-statement rule the archetype exists to enforce.

## Content-Type Notes
- **textHeavy**: lead becomes a single title line (chapter/section name); support becomes at most one sentence of transition text, never an opening paragraph. If content needs an opening paragraph, it's already become a different archetype.
- **chartHeavy**: lead becomes a single monumental statistic typeset as text at headline scale — never as a chart, axis, or table; support is a single sentence of context, nothing more.
- **cardOrListHeavy**: lead becomes a single category or part name, a divider between groups of items; support (if present) is a one-line scope note. The actual items live on the pages before and after, never on this one.

## Medium Notes
- Presentation: this archetype already IS a slide master — maps 1:1 onto a title slide or section-divider slide with zero adaptation. Every other archetype has to be adapted down to slide scale; this one starts there.
- Print: a full standalone page (cover or section-divider) with generous symmetric margins, no running header/footer, headline centered on both axes — never shares a page with body content.
- Markdown: degrades hard to a plain H1 with the entire scale-contrast value lost — don't target markdown output with this archetype; use a plain title line there instead.

## Pairing Notes
- `velvet-noir` — dark Art Deco maximalist with ornate serif hierarchy and dramatic gold glow; its own hero panel (Playfair Display headline, dark plum gradient, gold text-glow) is already this archetype's concept under a different name.
- `astral-drift` — its own hero is already a single dramatic typographic/visual statement (glitch-treated Cinzel Decorative headline over a psychedelic nebula with counter-rotating rings), exactly this archetype's concept at full theatrical strength.
