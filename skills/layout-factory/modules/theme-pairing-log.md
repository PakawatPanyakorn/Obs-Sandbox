# Theme Pairing Log

Tracks which theme-factory presets have been used as `exampleThemePairings` in which layout-factory presets, so new presets pick themes that genuinely fit rather than reaching for the same handful every time.

**Before adding theme pairings to a new preset:** check this table. A theme may be reused across layouts only when it is genuinely a strong fit for both — not because it's a convenient default. Prefer an unused theme that fits over a used one that's merely adequate.

| theme-factory preset | Used in (layout-factory preset) | Why it fit |
|---|---|---|
| `chalk-press` | `magazine-well` | "Typographic hierarchy does all the work" — matches magazine-well's core philosophy exactly. |
| `tobacco-road` | `magazine-well` | Field-journal editorial register, warm-vintage — distinct from chalk-press despite both being light/paper. |
| `obsidian-mono` | `magazine-well` | Dark austere counterpoint proving the archetype isn't tied to a light newspaper palette. |
| `bauhaus-konstrukt` | `swiss-international-grid` | Swiss International Style descends directly from Bauhaus/New Typography's grid-and-function ideology; its red/blue/yellow triad and zero-radius geometry read as this archetype's ideological ancestor made explicit. |
| `titanium-cloud` | `swiss-international-grid` | Its background is a literal fine cool-gray grid ("engineering graph paper"), and its restrained SaaS register favors structure over decoration without fighting the twelve-column module. |
| `prussian-blueprint` | `swiss-international-grid` | Its entire UI chrome (leader lines, dimension ticks, callout markers, a literal three-layer grid background) is a drafting-table rendering of the same modular grid this archetype formalizes for editorial content. |
| `wisdom` | `single-column-editorial` | Its own design notes call for "zero ornament beyond what reason dictates" — this archetype's philosophy stated as a theme brief; Cinzel's inscriptional caps make a quiet, dignified masthead without needing a single image. |
| `edo-stillwater` | `single-column-editorial` | Restrained, formal, built for stillness; Cormorant Garamond's light italic display gives the masthead a calligraphic quality without competing with 700 words of prose. |
| `harbor-clay` | `single-column-editorial` | The one modern-corporate register among the three proves the archetype isn't tied to a classical page — reads as a briefing memo or long-form report as easily as an essay. |
| `meridian-capital` | `split-hero` | Its own hero already leans on one dominant visual move (skewed gold accent panel + overlapping metric cards) — the same "one zone commands, everything supports" logic split-hero makes explicit. |
| `neon-foundry` | `split-hero` | Built around a single commanding hero block (left accent bar, orange glow, dark grid canvas) that reads immediately as a product-launch visual anchor. |
| `embassy-gold` | `split-hero` | A restrained navy hero field with a gold top-rule and Cormorant display type reads as institutional cover-page authority, suited to a content half that persuades through type alone. |
| `alpha-signal` | `dashboard-with-rail` | Its own description literally calls itself a "trading strategy / algorithm signal dashboard" with Bloomberg-esque data density — a rail confining live signals and stats is exactly what this theme was built to skin. |
| `vault-theorem` | `dashboard-with-rail` | Wealth-management "institutional allocation framework" with tiered navigation and a strategic allocation matrix — genuinely faceted content a rail's filters and stat modules are built to hold. |
| `eigenvalue` | `dashboard-with-rail` | A "quantitative algorithm lab" with live signal readouts sitting beside an asymmetric hero panel — the same persistent-readout-beside-content shape this archetype formalizes. |
| `soviet-agitprop` | `masthead-feature-river` | Constructivist propaganda posters are front-page composition in miniature — bold nameplate, one dominant image, dense columns of smaller notices beneath. |
| `prism-ledger` | `masthead-feature-river` | Its own component set literally is a broadsheet: centered masthead with a volume/issue dateline, a two-column feature spread, and a ruled ledger. |
| `riso-proof` | `masthead-feature-river` | A risograph zine front page is this archetype in miniature; misregistration shadows and its strict 3-ink discipline give the dense multi-column briefs a distinct small-press identity. |
| `bauhaus-geometry` | `asymmetric-split` | Bold primary-color hierarchy and hard offset shadows give the dominant body column real weight while everything secondary stays flat and undecorated. |
| `dead-letter-office` | `asymmetric-split` | Postal marginalia (routing codes, rubber stamps, postmarks) has always lived in a narrow column beside the main letter — reads naturally as citations/status running down a 1/3 rail. |
| `verdigris-patina` | `asymmetric-split` | Its own gimmick communicates progression top-to-bottom via color; here the 2/3:1/3 imbalance communicates emphasis left-to-right instead. |
| `crypt-scholastic` | `two-column-academic` | Its own description is literally "dark gothic academic" — a rare-books institution register that already reads as scholarly authority. |
| `bloc-brutus` | `two-column-academic` | Its background is a literal architectural grid overlay and "structure is truth" is its stated design philosophy — reads as a technical/engineering report register. |
| `vesper-furrow` | `two-column-academic` | Its own demo content is already formal report register — land-register entries, parcel references, surveyor notes — a close sibling to the academic paper this archetype is built for. |
| `vellum-codex` | `tufte-sidenote` | Illuminated manuscripts are the historical ancestor of the margin note itself; its antiquarian register and IM Fell English body face read as scholarly apparatus, not decoration. |
| `darkroom-safelight` | `tufte-sidenote` | Its frame-number/contact-sheet motif and chemical monospace notation already read as lab-notebook annotation, a natural register for a margin carrying methodology notes and citations. |
| `argent-vigil` | `tufte-sidenote` | Its own type sample literally names "marginalia, footnotes, the scribe's quiet hand" for small/muted text — a heraldic-archive voice suited to citation-dense writeups. |
| `thermal-fade` | `data-dense-report-grid` | Its receipt-ledger register (numbered TXN stamp, monospace line-item rows, dashed perforation dividers) is structurally the same discipline as a numbered exhibit stream. |
| `amber-signal` | `data-dense-report-grid` | Its dieselpunk phosphor console, with a literal transmission log and RSSI/frequency readouts, reads as instrumentation for a report rather than a product UI. |
| `cyber-terminal` | `data-dense-report-grid` | Green-on-black CRT terminal, monospace throughout, is the most literal "analyst workstation" register of the three — scanline texture reads as a terminal printing figures one at a time. |

## Guidance

- 2-3 pairings per preset is enough — this isn't meant to be exhaustive, just enough to demonstrate the archetype survives a real reskin.
- Favor variety across the *whole table*, not just within one preset: if `chalk-press` is already used twice, look elsewhere before a third use unless nothing else in `skills/theme-factory/themes/` fits as well.
- When picking, skim theme names/descriptions for aesthetic/personality tags that match the archetype's `family` (e.g. `editorial-narrative` archetypes lean toward themes tagged `editorial`; `data-dense-report` archetypes toward `technical`/analytical themes; `dashboard-legitimate` toward SaaS/product aesthetics).
- Add a row here immediately after adding `exampleThemePairings` to a preset — this file is the only record of what's already been used.
