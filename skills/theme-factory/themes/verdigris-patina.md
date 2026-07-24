# verdigris-patina

A single palette that tells geological time — color literally ages as you scroll down the page, from fresh-cast brass at the header to deep oxidized verdigris by the footer, mirroring how real bronze weathers over centuries.

## Core Concept
Dark teal-black ground (`#0F1C18`) under a genuine 20-layer radial-gradient CSS texture simulating oxidation: bright verdigris splotches, dark shadow-pocket crevices, warm bronze-gold seams exposed through the oxide — `background-attachment: fixed`, making it "a true environmental background" the content scrolls over rather than with. Cormorant Garamond's light serif against Josefin Sans's geometric display. The theme's defining mechanic (shared conceptually with [[thermal-fade]]'s vertical decay, but color-shifting rather than opacity-fading): **content should visually age as it descends the page** — header zones lean toward fresh brass/gold, lower sections toward deep verdigris teal.

## Color Role Guidance

### primary (`#C8A830` fresh-cast brass) — also `warning`
- When to use: the "youngest" metal state — header-zone elements, primary buttons, the freshest/newest content on a page. Shares its hex with `warning`, so brass gold always carries a faint "recent/attention" connotation.
- Surface area: concentrated toward the top of a composition — per the theme's own vertical-aging concept, brass should thin out as content descends.
- Don't: don't apply brass uniformly across an entire long page — that flattens the theme's core "geological time" narrative into a static gold accent.

### secondary (`#3DC8B0` mid-patina teal) — also `success`
- When to use: the "middle-aged" oxidation state — mid-page sections, confirmed/settled content (shares hex with success).
- Surface area: the dominant tone for the bulk of typical content — this is effectively the theme's main working color, positioned between fresh brass and deep verdigris.
- Don't: don't skip straight from brass to the darkest verdigris — secondary's mid-patina teal is the necessary transitional state that makes the aging read as gradual, not binary.

### accent (`#60DCC8` bright verdigris highlight)
- When to use: mineral-deposit highlights — bright oxidation crystals against the darker ground, a lighter register of secondary's teal.
- Surface area: small — specific highlight moments (a called-out figure, a bright accent within a patinated section), not a general fill.
- Don't: don't use accent as a fourth independent hue — it's a brightness variant within the teal/verdigris family, consistent with the theme's tightly-controlled oxidation palette.

## When To Use
- Archaeological, historical, museum, or "deep time" narrative content where the vertical-aging device can do real storytelling work (e.g., a long-scroll history piece where content genuinely gets older as you scroll).
- Content wanting a distinctive, literal metaphor for scroll-based progression beyond generic parallax or fade effects.
- Editorial content with real geological/archaeological/material-science subject matter that benefits from the oxidation metaphor being literal, not just decorative.

## When NOT To Use
- Short pages or content without meaningful vertical scroll depth — the aging effect needs real page length to read as a progression, not a static gradient.
- Content where header and footer should carry equal visual weight — the theme inherently treats "top" as fresher/more prominent than "bottom."
- Fast-scanning or data-dense UI — `density: spacious`, `lineHeight: 1.7`, and the slow visual narrative are built for contemplative reading, not quick scanning.

## How To Use — Full Potential
- Actually implement the vertical color-aging, not just a static brass/teal palette — bias primary/brass toward the top third of a long page, secondary/teal through the middle, and darker verdigris tones by the bottom, so scrolling itself narrates the metaphor.
- Use the fixed-attachment 20-layer oxidation texture as the environmental background the whole page scrolls over — this is what makes the surface feel like real weathered bronze rather than a flat gradient.
- Reserve accent's bright verdigris highlight for specific "mineral deposit" moments — a called-out quote or key figure within an otherwise patinated section.
- If only one thing: apply a brass-to-teal color shift across a page's header-to-footer span — the fastest way to demonstrate verdigris-patina's core "geological time" mechanic, even on a shorter page.

## Apply-Mode Notes
- Step 4a: this theme's color distribution is positional, not just semantic — during harmonize, bias primary/brass toward the top of long content and secondary/teal toward lower sections, rather than distributing them evenly.
- Step 4k (background): preserve `background-attachment: fixed` — this is what makes the oxidation texture read as an environmental surface the content ages against, not just a decorative backdrop.
