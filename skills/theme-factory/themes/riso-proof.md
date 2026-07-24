# riso-proof

A genuine 2-drum risograph short-run print — only teal and fluorescent pink ink plus black, with deliberate misregistration (offset shadows in the "wrong" ink, as if the paper shifted between drum passes) as the theme's core visual device.

## Core Concept
Warm cream uncoated-paper canvas (`#F7F3E8`) with subtle grain (`patternType: noise`, "slightly toothy texture under the ink"), Space Grotesk for both body and display, Space Mono for code. This theme only has **2 real ink colors**: primary teal (`#00A693`, which also equals `success`) and secondary/accent pink (`#FF3E85`, which covers secondary, accent, AND `error`) — a true 2-drum riso print has no room for a third or fourth hue. The signature device is offset "misregistration" shadows: `--shadow-md: 4px 4px 0 #FF3E85` puts a *pink* shadow (not the element's own color) behind shapes, exactly like a riso press's second pass landing slightly off the first.

## Color Role Guidance

### primary (`#00A693` teal ink) — also `success`
- When to use: the first ink pass — primary buttons, structural elements, success/confirmation states (they share a hex).
- Surface area: generous — one of only two real chromatic inks, used broadly.
- Don't: don't introduce a separate success color — teal already carries that meaning; adding a third green during any edit breaks the authentic 2-ink constraint.

### secondary / accent / error (`#FF3E85` fluorescent pink) — one ink, three role names
- When to use: the second ink pass — the misregistration shadow color (`--shadow-sm/md/lg/xl` are ALL pink, regardless of what color the shadowed element is), plus error states and any accent emphasis.
- Surface area: everywhere shadows appear (structural, not just decorative) plus any accent/error need.
- Don't: don't invent a separate accent or error color — the theme's entire realism depends on there being exactly one non-teal ink; splitting it into three "different" pinks breaks the print-authenticity conceit.

## When To Use
- Zine, indie-print, DIY-publishing, or lo-fi design content wanting genuine risograph authenticity rather than a generic "2-color print" gesture.
- Content that benefits from the misregistration shadow technique as structural elevation, not just decoration — it doubles as the theme's entire depth system.
- Playful, handmade-adjacent editorial or event/poster content.

## When NOT To Use
- Any content needing more than 2 chromatic roles — the theme's authenticity depends on exactly one teal + one pink ink; a taxonomy needing 4 distinguishable hues has nowhere to go.
- Polished, corporate, or high-fidelity digital content — the entire point is imperfection (misregistration, paper grain, flat unblurred shadows).
- Content needing soft/rounded shapes — `borderRadius: 0px` throughout, consistent with riso printing's typically sharp-edged output.

## How To Use — Full Potential
- Use the misregistration shadow technique (a pink offset shadow behind a teal — or any — element) as the *primary* elevation mechanism, never a blur-based soft shadow — this single device is what makes the theme unmistakably riso-proof.
- Keep the paper-grain noise texture visible across the full page — it's what sells "uncoated stock," and a smooth background undermines the print-authenticity premise.
- Apply the offset text-shadow (`2px 2px 0 rgba(255,62,133,0.5)`) to headlines for the same "second ink pass slipped" effect at the type level.
- If only one thing: apply a `4px 4px 0 #FF3E85` offset shadow to a teal-colored element — the exact mismatch (pink shadow on a non-pink shape) is the theme's single most recognizable signature.

## Apply-Mode Notes
- Step 4a: preserve the exactly-2-ink constraint (teal=primary=success, pink=secondary=accent=error) — do not introduce a third or fourth distinct hue during harmonize, even for a target with more categorical states than 2 inks can naturally cover.
- Step 4j: hard offset shadows in the "wrong" ink are structural, not decorative — never convert them to soft blur-based shadows; that would erase the misregistration effect entirely.
