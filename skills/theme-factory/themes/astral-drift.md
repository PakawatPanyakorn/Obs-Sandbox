# astral-drift

Deep-space psychedelia rendered as an "interdimensional navigation console" — a 6-layer nebula mesh, counter-rotating conic mandala rings, and a CSS-only glitch-text hero that together commit fully to a mystic-sci-fi conceit rather than dabbling in it.

## Core Concept
Deep-indigo canvas (`#08061A`) under a fixed 6-layer radial nebula (magenta/pink/cyan/chartreuse/gold/violet), with Cinzel Decorative's carved-stone display face reserved for the hero glitch title and Philosopher's contemplative italic serif carrying body copy. The theme's discipline: the full 4-stop chromatic gradient text (`--gradient-text`) is used *only* on the hero title — h2/h3 fall back to solid `--color-primary`/`--color-text` (per `design.notes`). Breaking that restraint (rainbow-gradient-clipping every heading) is the fastest way to make this theme look cheap instead of dimensional.

## Color Role Guidance

### primary (`#CC00FF` electric violet)
- When to use: the "crown"/highest-frequency signal — glitch-title base color, primary buttons (`.btn-primary`), the outer mandala ring's dominant hue, `status-surging`.
- Surface area: hero elements and the single most "activated" state per view — this theme wants violet to feel like the peak of a spectrum, not a flat brand color.
- Don't: don't apply primary without its glow (`--shadow-colored`, `--glow-md`) — every primary surface in the preset carries luminescence; a shadowless violet block reads as an incomplete import.

### secondary (`#E8B040` astral gold)
- When to use: the "solar plexus" register — secondary buttons (`.btn-secondary`), one gradient stop, mid-frequency data points (`.sig-amp`).
- Surface area: text and outline treatments, one specific frequency-bar color — always positioned as a *warm* counterpoint inside an otherwise cool violet/cyan field.
- Don't: don't let secondary compete with `warning` (`#FFB000`) — they're deliberately close in hue; keep secondary to narrative/data roles and warning to genuine caution states.

### accent (`#00EEFF` neon cyan)
- When to use: the "throat"/witness register — `status-ascending`, accent buttons (`.btn-accent`), the second glitch-layer color (`.glitch-wrap::before`).
- Surface area: small high-contrast hits and the second voice in any two-color pairing with primary (glow shadows explicitly combine violet + cyan: `--glow-md`).
- Don't: don't use accent and primary as interchangeable "any bright color" — cyan specifically pairs with violet in glows/glitch layers; using it alone loses that paired-frequency read.

## When To Use
- Spiritual-tech, astrology/tarot, music-frequency, or "consciousness"-branded products — the theme's own content (chakra frequencies, dimensional entities, Saturn Return) names its genre outright.
- Experimental art, festival, or generative-music sites wanting maximal, unapologetic psychedelic density.
- Dark-mode surfaces that can sustain real motion (the preset ships `@keyframes` for spin, pulse, glitch, drift, flicker) — this theme is built assuming animation is available, not just static color.

## When NOT To Use
- Any content requiring calm, credible, or clinical tone — the glitch text and 6-layer nebula are maximalist by design and cannot be toned down without becoming a different theme.
- Static/print/PDF output — several signature effects (`ring-system` rotation, glitch-slide, orb pulse) are pure CSS animation with no meaningful static fallback.
- Data-dense business content — the theme's tables (`.signal-table`) are built for evocative pseudo-data (frequencies, phases, Ψ amplitudes), not literal business metrics; forcing real KPIs into this chrome undersells both.

## How To Use — Full Potential
- Lead with the hero's two-part signature: glitch-text title (`.glitch-wrap` + `::before`/`::after` clip-path animation) paired with the counter-rotating `.ring-system` (three conic-gradient rings, masked to rings, spinning at different speeds/directions) — this is the theme's single most distinctive combination and should anchor page one.
- Use `.entity-card`'s per-card custom properties (`--card-glow`, `--card-aura`, `--drift-dur`, `--drift-del`) to give each card its own color and drift timing rather than one uniform card style — the staggered animation is what makes a grid of cards feel like independent floating entities.
- Reserve the full 4-stop `--gradient-text` for the page's single hero title only, per the theme's own restraint rule — use solid `--color-primary` italic (`.t-h2` style) for every other heading.
- If only one thing: pair a glow-bearing badge (`.status-surging`, `box-shadow: var(--glow-sm)`) with its accent color text — the smallest unit that still reads as "astral-drift" at a glance.

## Apply-Mode Notes
- Step 4j (gradients/glow/effects) needs the restraint rule preserved: gradient-clipped text belongs on the hero headline only; if the target file has multiple headings, harmonize should apply solid primary/accent color to the rest, not repeat the 4-stop gradient everywhere.
- This theme assumes motion is available — if applying to a context where animation must be disabled (print, reduced-motion), flag to the user that the ring system and glitch title have no meaningful static equivalent rather than silently rendering them motionless.
