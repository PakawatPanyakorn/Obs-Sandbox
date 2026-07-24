# tokyo-screentone

Japanese graphic-novel print production, not a "manga-inspired" gesture — a dense 8px screentone dot-grid simulating genuine halftone printing, manga-ink black, vermillion, and manga-blue, with zero softening anywhere.

## Core Concept
Warm paper canvas (`#F8F5EE`) under an unusually dense 8px dot-grid (`patternOpacity: 0.12`) — per `design.notes`, "much denser than typical dot-grid to simulate print screentone," distinguishing it from softer botanical dot-grids elsewhere in the catalog (e.g. [[moss-cottage]]'s 18px sage grid). Big Shoulders Display's condensed ultra-bold (900wt) against Mulish's light body. `motion.easing: steps(4)` is unique in the catalog — a stepped, non-eased transition that mimics manga panel-to-panel cuts rather than smooth animation. `gradients.*: none`, `borderRadius: 0px`, hard offset shadows only (`4px 4px 0 #C8C0B0`) — total zero-softening discipline.

## Color Role Guidance

### primary (`#181410` manga-ink near-black)
- When to use: this is the "ink line" — headlines, primary text, structural borders. Like several other themes in the catalog, primary here is a neutral ink tone rather than a saturated brand hue.
- Surface area: extensive — ink black is the dominant structural color, appropriate for large use.
- Don't: don't lighten primary or add any softness (glow, gradient) — flat, hard-edged black ink is the entire premise.

### secondary (`#D42A20` vermillion)
- When to use: the "action/impact" ink — secondary buttons, `--shadow-colored` (vermillion offset shadow), the one warm chromatic punch against the ink/paper duo.
- Surface area: moderate — a bold, deliberate hit, used the way manga uses a single spot-color for emphasis panels.
- Don't: don't soften vermillion with any glow — its impact depends on being flat and hard, like screen-printed spot color.

### accent (`#1890CC` manga blue)
- When to use: a cooler counterpoint to vermillion — a second spot-color option for differentiating content categories or moods within the same stark register.
- Surface area: small to moderate — the third color in the system, less frequent than ink black or vermillion.
- Don't: don't blend accent and secondary into a single "colorful" treatment — each should read as a distinct, deliberate spot-color choice, not part of a gradient or blend.

## When To Use
- Manga, graphic novel, Japanese pop-culture, or comic-adjacent content wanting genuine print-production authenticity.
- Bold, high-contrast editorial or portfolio content wanting stark impact without any softening.
- Content that can sustain stepped, non-eased motion (`steps(4)`) — panel-cut-style transitions rather than smooth animation, appropriate for comic-reading interactions.

## When NOT To Use
- Soft, warm, or approachable branding — every choice (zero radius, hard shadows, dense halftone) is stark and unforgiving by design.
- Content needing smooth, fluid motion — the stepped easing is a deliberate, unusual choice that will feel jarring if applied to conventional UI expecting smooth transitions.
- Long-form dense reading — Big Shoulders Display at 900-weight is built for short, high-impact headlines, not body text.

## How To Use — Full Potential
- Keep the dense 8px screentone dot-grid visible across the full page at its specified density — a sparser grid loses the "print halftone" authenticity this theme is built around.
- Use `steps(4)` easing on any transition/interaction — the stepped, panel-cut motion is a distinctive, easily-overlooked signature; default easing curves undersell the manga-production concept.
- Reserve vermillion and manga-blue as two distinct spot-colors for differentiating content, never blended or gradiented together — this mirrors real manga spot-color printing constraints.
- If only one thing: apply the dense 8px screentone dot-grid behind a Big Shoulders Display 900-weight headline with a hard offset shadow — the fastest way to signal tokyo-screentone.

## Apply-Mode Notes
- Step 4j: motion easing is part of this theme's identity — apply `steps(4)` (or a similarly stepped curve) to transitions during harmonize rather than defaulting to a smooth cubic-bezier.
- Step 4d/4j: zero gradients, zero glow, zero radius by design — any hero/colored-section harmonize must stay flat with hard offset shadows and the dense dot-grid texture only.
