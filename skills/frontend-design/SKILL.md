---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces with high design quality. Only invoke when explicitly called via /frontend-design slash command — do not auto-trigger from user requests.
---

Create distinctive, production-grade frontend interfaces. Avoid generic "AI slop" aesthetics. Implement real working code with exceptional aesthetic precision.

## Design Thinking

Before coding, commit to a bold aesthetic direction across four axes:

- **Purpose**: what problem does this solve and who uses it?
- **Tone**: pick an extreme — brutally minimal, maximalist, retro-futuristic, editorial, brutalist, art deco, soft/pastel, industrial, etc.
- **Constraints**: framework, performance, accessibility requirements.
- **Differentiation**: the one thing someone will remember.

Execute the chosen direction with precision. Bold maximalism and refined minimalism both work — intentionality is the requirement, not intensity.

## Aesthetics

- **Typography**: distinctive display + refined body font pair. Never Inter, Roboto, Arial, system fonts, or Space Grotesk.
- **Color**: cohesive palette via CSS variables; dominant hues with sharp accents over timid even distributions.
- **Motion**: CSS-only for HTML; Motion library for React. One orchestrated page-load with staggered reveals beats scattered micro-interactions. Surprise on hover and scroll.
- **Layout**: asymmetry, overlap, diagonal flow, grid-breaking elements, generous negative space or controlled density.
- **Backgrounds**: depth over solid colors — gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows.

Never reuse the same aesthetic across generations.

## Interactivity & Diagram

- **Always interactive**: every output includes hover states, click handlers, transitions, or toggles — never purely static HTML.
- **Always include a diagram**: append a visual structure diagram (component tree, layout map, or flow) as a commented ASCII block or inline SVG at the end of every output.

## Color Themes

- Implement at least 3 named themes via CSS custom properties on a `data-theme` attribute on `<html>`.
- Include a visible theme-switcher control in the UI.
- Themes must be meaningfully distinct — not just hue-shifted clones. Required theme types:
  - **At least 1 formal/professional theme**: clean, restrained palette (e.g. neutral grays, off-white), structured typography, minimal decoration — conveys trust and clarity.
  - **At least 1 super-creative theme**: bold unexpected color combinations, expressive typography, strong visual personality — something that would stop a designer mid-scroll (e.g. neon-on-black, maximalist gradients, retro psychedelic, vaporwave, risograph print aesthetic).
  - Remaining themes can be anything meaningfully distinct (e.g. dark mode, high-contrast, seasonal).
