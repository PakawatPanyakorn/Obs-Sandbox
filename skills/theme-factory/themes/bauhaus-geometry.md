# bauhaus-geometry

Shapes ARE the UI — not decoration applied to components, but the component system itself, built from 16 named CSS-only geometric primitives each carrying a specific semantic meaning.

## Core Concept
Classic Bauhaus red/blue/yellow triad on warm-white exhibition paper, zero border-radius, hard 2D offset shadows (`4px 4px 0 #1A1918`, no blur — `elevation: flat`). The theme's defining move is the **shape-as-meaning system**: circle = closed/complete (ring charts, counts), hexagon = cell/network/hierarchy (team rosters, tier badges), shield = protection/authority (trust cards, permission badges), arrow/chevron = direction/sequence (pipelines), diamond = rarity/value. Picking a shape because it looks interesting rather than because it means the content is the theme's core anti-pattern.

## Color Role Guidance

### primary (`#E63329` Bauhaus red)
- When to use: the "done"/highest-urgency state — primary buttons (`.bh-btn-primary`), notification-count badges (`.sb-circle`), the first/completed step in a process flow (`.ps-red`).
- Surface area: whole shape fills are normal here (this theme is unafraid of large flat color blocks), but reserve red specifically for completion/primary-action semantics, not as a generic "main brand color."
- Don't: don't use red interchangeably with blue/yellow for arbitrary visual variety — the Latin-square shape directory (`.shape-cell:nth-child`) proves the palette rotates deliberately, not randomly; any UI reusing the pattern should rotate with the same discipline.

### secondary (`#1B47D4` Bauhaus blue)
- When to use: structural/systemic elements — hexagon tier badges (`.sb-hex`), shield trust cards (`.shield-card`), the "active/in-progress" step in a pipeline (`.ps-blue`).
- Surface area: large fills are fine; blue reads as "the system," red reads as "the action."
- Don't: don't use blue for warnings or errors — this theme's `error` token reuses primary red; blue is purely structural/neutral-positive.

### accent (`#F5C400` Bauhaus yellow)
- When to use: the "pending/queued" or "rare/valuable" register — diamond rarity badges (`.sb-diamond`), the third/queued pipeline step (`.ps-yellow`), warning states (accent doubles as warning-adjacent).
- Surface area: needs dark text (`--bauhaus-black`) for contrast wherever it's a fill — the preset explicitly swaps shape/label colors to black on every yellow cell (`.shape-cell:nth-child(3) .sh` etc.) — never place light text on yellow.
- Don't: don't treat yellow as purely decorative — in the pipeline/badge system it specifically means "not yet, but coming."

## When To Use
- Design-system documentation, component libraries, or educational/reference content where naming and taxonomy matter — the "Shape Directory" (16 named primitives with their CSS method shown) is built for exactly this.
- Products that want unmistakable, joyful geometric confidence — team rosters, pipelines, status dashboards, tier/plan pages — anywhere a shape's meaning can do real communicative work.
- Content that benefits from hard offset shadows and zero radius reading as "structural, not soft" — flat, confident, poster-like layouts.

## When NOT To Use
- Any content where shapes would be purely decorative — if you can't state why a hexagon (not a circle, not a square) fits a given piece of content, per this theme's own discipline, don't use a non-rectangular shape at all.
- Soft, calming, or luxury contexts — the flat primary triad and hard shadows are deliberately blunt and playful, the opposite of subtle.
- Long-form dense reading — `bodyWeight: 400` Josefin Sans at `letterSpacing: 0.015em` with uppercase headings throughout is tuned for short labels and display text, not paragraphs.

## How To Use — Full Potential
- Match shape to meaning using the theme's own vocabulary: circle for ratios/completeness, hexagon for hierarchy/network, shield for trust/authority, arrow/chevron for sequence, diamond for scarcity — this mapping (spelled out in `.sc-use-why`/`.badge-context-why`) is the single most valuable asset in the preset; reuse it rather than inventing new shape meanings.
- Use the masthead's 5-panel asymmetric grid (`.bh-masthead`: dark title spanning 2 rows + 4 colored shape panels) as the template for any hero — it's the strongest demonstration of "shapes as UI" in the preset.
- Reuse the hard-shadow button interaction (`transform: translate(-2px,-2px)` on hover, `translate(2px,2px)` + no shadow on active) — it's a tactile, theme-native affordance, not just a color change.
- If only one thing: apply one shape (hexagon, shield, or diamond) with `clip-path` to a badge whose meaning matches the shape's semantic — this single choice communicates the entire theme philosophy in one component.

## Apply-Mode Notes
- Step 4a (color distribution): map primary/secondary/accent to completion-state semantics (red=done, blue=active, yellow=queued) wherever the target file has any sequential/status data — this theme has an opinionated built-in mapping, don't default to a generic 60/30/10 split.
- Step 4d/4j (gradients/effects): this theme has zero gradients and zero glow by design (`elevation: flat`) — preserve the hard offset shadow as the *only* elevation cue; adding blur-based shadows or gradients during harmonize breaks the "flat, structural" premise.
