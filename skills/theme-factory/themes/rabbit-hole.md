# rabbit-hole

Alice's Wonderland as horror vacui — the only theme in the catalog with `hierarchyClarity: low` *by design*: disorientation isn't a flaw to fix, it's the explicit goal ("the user should feel like they are falling").

## Core Concept
Ultra-dark void canvas (`#080611`) under a 4-layer background: purple/teal/rose radial gradient mesh plus a faint repeating conic checkerboard, "mimics the vortex spiral from the source image." IM Fell English's antique serif body against Cinzel Decorative's ornate display, VT323's pixel-mono for a Wonderland-clock-face register. Playing-card suits, chess logic, and clock motifs are named directly in `design.notes` as literal content devices, not just color inspiration. This is the rare theme where crowding every surface with meaning is correct, not an anti-pattern to fix.

## Color Role Guidance

### primary (`#9B2EE8` violet)
- When to use: the dominant "falling into the vortex" signal — primary buttons (`--gradient-button`, violet→rose), the strongest glow (`--glow-lg`, up to 120px spread combining violet and teal), headline text-shadow.
- Surface area: generous and unrestrained — this theme wants visual density, not minimalist restraint; primary should appear boldly and often.
- Don't: don't apply primary without heavy glow — every primary surface in the preset carries multi-layer glow; a flat violet fill undersells the psychedelic intensity.

### secondary (`#E8197A` hot pink/rose)
- When to use: a co-equal partner to primary in gradients — `--gradient-button` and `--gradient-text` both pair secondary directly with primary, not as a lesser accent.
- Surface area: substantial — secondary carries as much visual weight as primary in this maximalist system.
- Don't: don't treat secondary as subordinate — in the 5-stop `--gradient-text` (violet→rose→teal→gold→violet, a full loop), all colors are equals.

### accent (`#00E5C8` teal)
- When to use: the cooling counterpoint inside an otherwise hot violet/rose field — one background gradient layer, a stop in the multi-color gradients, secondary glow tint (`glowLg` combines violet AND teal).
- Surface area: moderate — enough to register as a genuine third voice, not just a highlight.
- Don't: don't isolate accent from the other colors — it's meant to appear woven through gradients alongside primary/secondary, part of the "color storm," not a standalone accent.

## When To Use
- Wonderland/fantasy/surreal narrative content, immersive storytelling experiences, or maximalist creative portfolios wanting genuine, sustained visual density.
- Content that can embrace *low* hierarchy clarity as a feature — experiential, mood-first content over information-hierarchy-first content.
- Illustrative content (`imageStyle: illustrative`) with room for literal Wonderland motifs (cards, chess, clocks, spirals).

## When NOT To Use
- Any content needing clear information hierarchy or scannable structure — this theme's `hierarchyClarity: low` is explicit and real; dashboards, documentation, or task-focused UI will actively fight this theme.
- Accessibility-sensitive or high-stakes content — deliberate disorientation is incompatible with clarity-first requirements.
- Restrained or minimalist branding — density and color-storm maximalism are the entire point; there's no "quiet" version of this theme.

## How To Use — Full Potential
- Layer the conic checkerboard pattern beneath the radial gradient mesh consistently — the combination (not either alone) is what creates the "vortex spiral" read the theme is built around.
- Use the full 5-stop looping gradient (`--gradient-text`: violet→rose→teal→gold→violet) on major headlines — its looping structure (ending where it started) reinforces the "falling/spiraling" concept better than a linear 2-stop gradient would.
- Lean into literal Wonderland iconography (playing cards, chess pieces, clock faces, spiral motifs) as content devices, not just color choices — the theme's identity depends partly on subject matter, not chrome alone.
- If only one thing: layer a radial gradient mesh over a faint conic checkerboard behind any content — the fastest way to summon the "falling down the rabbit hole" read.

## Apply-Mode Notes
- Step 4a: do NOT try to impose a clean, high-clarity color hierarchy on this theme during harmonize — `hierarchyClarity: low` is intentional; resist the instinct to "fix" visual density that reads as excessive in other themes.
- Step 4j: multi-layer glow and gradient effects are the theme's entire identity — under-applying them (in the name of restraint) is the most common way this theme gets flattened into a generic dark-purple theme.
