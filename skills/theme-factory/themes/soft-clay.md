# soft-clay

Everything on this page is the same block of warm stone — some of it pushed out, some of it pressed in, none of it a different color.

## Core Concept

Soft Clay is the library's only true soft-UI/neumorphic treatment — it files under `aesthetic: "minimal"`, which is where the library folds soft-UI — and it takes the constraint seriously: `background`, `surface`, and every button's resting fill are all literally `#E4DED7` — the same hex. Depth comes entirely from the paired light/dark shadow (`--shadow-out-*` for resting elements, `--shadow-in` for wells and pressed states), never from a different surface color or a border. That's why `borderStyle: "none"` isn't a placeholder — a border would be a second visual language competing with the shadow, and this theme only speaks one. Terracotta (`primary`) is the single spot of saturation, and it shows up only as text or icon color on top of the extruded stone, never as a fill — a solid terracotta button would look like a different, ordinary theme wearing a neumorphic shadow as decoration.

## Color Role Guidance

### primary (#C67B5C)
- When to use: text/icon color on an already-extruded element — `.sc-btn-primary` text, `.sc-card-dial` numerals, the "Firing" status badge
- Surface area: typography-only. There is no `.sc-btn-primary` background fill in this theme — check `--gradient-button: none` and the button CSS, which paints every button the same stone `--color-bg`
- Don't: fill a card, header, or button background with primary — that reintroduces a second surface color and breaks the single-material illusion this theme depends on

### secondary (#8F8579)
- When to use: a quieter action's text color (`.sc-btn-secondary`), one step down in emphasis from primary
- Surface area: same rule as primary — text/icon only, never a fill
- Don't: use secondary to differentiate a surface (e.g., a "secondary panel" bg) — panels stay uniform stone regardless of role

### accent (#D99A7C)
- When to use: the lightest terracotta step, reserved for rare decorative touches (a thin progress fill, a hover-state tint) — this theme doesn't currently use it in a component, which is itself a signal: accent is optional garnish, not a required third role
- Surface area: minimal, decorative only
- Don't: force accent into a component that doesn't need it just because the slot exists

## When To Use
- Physical/tactile control-panel UIs — dials, toggles, booking boards, anything conceptually "pressable" (the `.sc-card-dial` circular inset numeral is the clearest example of the pattern)
- Product dashboards wanting warmth without color noise — with only one hue used sparingly, the interface stays calm even when dense
- Contexts that can tolerate a background slightly below the usual 90%-lightness floor (~87% here) in exchange for the shadow pair having room to work in both directions

## When NOT To Use
- Accessibility-sensitive contexts — low-contrast dual shadows are a known weak point of neumorphism; interactive elements here rely on shape/shadow more than color or border to signal "clickable," which some users will miss
- Content-dense reading or data-table UIs — the extrusion effect reads clearly on a handful of large tiles (`.sc-card-grid`) but turns muddy at small sizes or in tight repeated rows
- Alongside `fog-linen` in the same project — both are warm-neutral minimal-adjacent themes; stacking them together reads as indecision rather than two distinct products

## How To Use — Full Potential
- The outset/inset pair (`.sc-out-demo` / `.sc-in-demo` in the Extrusion section) is the whole theme in miniature — any new component should ask "is this a resting surface or a well," pick one shadow token, and stop there; never combine both on one element
- `.sc-btn:active` swaps `--shadow-out-sm` for `--shadow-in` — that press-state inversion is the single interaction every neumorphic component should have; a button that doesn't visibly "push in" on click isn't using this theme correctly
- If you only do one thing: keep every surface the exact same background hex and let shadows alone carry elevation — the moment two adjacent panels use different fill colors, it stops reading as Soft Clay and starts reading as a flat theme with some drop shadows

## Apply-Mode Notes
- Standard harmonize step 4a (">60% primary → introduce a counterpoint") doesn't apply the normal way: primary here is never a fill in the first place, so there's no fill-percentage to rebalance — the relevant check instead is "is primary ever used as a background?" (it shouldn't be)
- Skip gradient and glow harmonize steps entirely — both are `none` by design
- When re-theming a page that previously had bordered cards, expect to strip `border` properties wholesale and replace with the shadow pair, not just recolor the border — this is a structural swap, same caveat as fog-linen but in the opposite direction (shadow-heavy instead of border-only)
