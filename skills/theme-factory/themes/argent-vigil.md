# argent-vigil

A knight's polished steel shield held over iron-night black — heraldic without being cartoonish, forged rather than fantastical.

## Core Concept
Iron-black canvas (`#14161b`) with a near-invisible crosshatch pattern (`patternType: crosshatch`, opacity `0.035`) evoking chainmail links, engraved Cinzel titling caps (`fontFamilyDisplay`) over an EB Garamond italic body. The palette reads as literal heraldry: brushed-steel primary (the shield), war-banner crimson secondary, antique-gold accent (the heraldry itself) — every color name in the demo copy ("Blazon of Colours," "War Banner," "The Armoury") reinforces the metaphor rather than decorating it.

## Color Role Guidance

### primary (`#b6bfcc` brushed steel)
- When to use: structural authority — the hero's brushed-steel gradient (`.tf-header`, `--gradient-hero`), primary buttons (`.tf-btn-primary`, itself a steel gradient not a flat fill), card headings (`.tf-card h3`).
- Surface area: large structural surfaces are appropriate — this theme wants steel to feel like armor plating, not a small accent chip.
- Don't: don't render primary as a flat fill without its gradient — every primary surface in the preset (`--gradient-hero`, `--gradient-button`, `--gradient-text`) is a subtle metallic gradient; flattening it loses the "brushed steel" read entirely.

### secondary (`#8b1a2e` heraldic crimson)
- When to use: the "war banner" — secondary buttons (`.tf-btn-secondary`), `--shadow-colored`'s tint, anything that should read as an active call to arms rather than passive structure.
- Surface area: buttons and status accents — a deep, saturated color meant to punctuate the steel/black field, not cover large areas.
- Don't: don't pair crimson with a light/optimistic tone — it's specifically a "siege/war" signal here, reserved for urgency and standing out against the cool steel palette.

### accent (`#c9a24b` antique gold)
- When to use: the "heraldry" note — crest labels (`.tf-crest`), section titles (`.tf-section-title`), the warning-state color, gradient endpoints (`--gradient-accent` runs crimson→gold).
- Surface area: small ornamental text and thin strokes — gold reads as "detailing," never a large fill.
- Don't: gold and `warning` share the same hex (`#c9a24b`) intentionally — don't introduce a separate warning color, and don't treat gold as decorative-only; it's doing double duty as the theme's caution signal too.

## When To Use
- Fantasy/historical games, guild or order-themed communities, premium editorial content wanting gravitas without literal medieval kitsch.
- Dark-mode products that want a "forged," high-craft feel — the heavy shadows (`shadows.elevation: dramatic`) and near-zero border radii (`borderRadius: 2px`) read as deliberate, not accidental starkness.
- Content that can sustain a consistent metaphor throughout (siege/vigil/heraldry) — the theme's demo content shows how far the conceit should extend into copy, not just color.

## When NOT To Use
- Playful, rounded, or consumer-friendly products — the sharp near-zero radii and forged shadows actively resist a friendly read.
- Content needing more than 3 chromatic roles — accent/warning sharing one hex means a 4th distinct semantic color has no natural home without inventing one.
- Fast-moving, high-frequency-interaction UIs — `motion.feel: subtle` and `durationSlow: 420ms` are tuned for weight and gravitas, not snappy feedback loops.

## How To Use — Full Potential
- Lead with `.tf-header`'s full stack: brushed-steel gradient background + top hairline (`border-top: 2px solid rgba(182,191,204,0.5)`) + diagonal sheen overlay (`.tf-header::after`) — this is the theme's "polished shield catching light" effect and is lost if any layer is dropped.
- Use `.tf-crest`'s wide letter-spacing (`0.42em`) uppercase label above the main heading — this exact spacing value is what makes a label read as "engraved" rather than just uppercase.
- Reserve `--shadow-colored` (crimson-tinted) specifically for the one most urgent action per view (`.tf-btn-secondary`, alert badges) — using it everywhere dilutes its "war banner" signal.
- If only one thing: apply the brushed-steel gradient (`--gradient-hero`) with a top hairline highlight to any header — it's the single fastest way to make a surface read as forged rather than flat.

## Apply-Mode Notes
- Step 4d (colored sections): the hero treatment here is a metallic gradient, not a hue-based brand gradient — when harmonizing a target's hero section, don't substitute a flat primary-color fill; reconstruct the multi-stop steel gradient or the "shield" read is lost.
- Step 4a color distribution: accent and warning intentionally share one value — don't force a separate warning color onto this theme during harmonize; the overlap is by design (gold heraldry = caution).
