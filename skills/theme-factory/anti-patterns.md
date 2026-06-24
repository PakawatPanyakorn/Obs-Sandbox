# Anti-AI Tells — Quick Reference

## Critical (ships as slop)

| Tell | Fix |
|------|-----|
| Purple-to-blue/pink gradient hero | Single hue. No gradient backgrounds. |
| Inter/Roboto as both display and body | Pair a distinctive display face with a body face. |
| 3-column icon-above-heading feature grid | Break the grid. Vary widths, heights, or drop cards entirely. |
| Card inside a card | One containment layer. Usually the outer one is wrong. |
| Gradient-fill headline (`background-clip: text`) | Solid ink. Use weight or italic instead. |
| Side-stripe card (4–6px colored left border) | Hairline border all around, or none. Never asymmetric thick stripe. |
| `min-height: 100vh` centred hero, one sentence, one CTA | Let height follow content. Bias left or right. Say more. |
| `#000000` or `#ffffff` surfaces | Tint toward your anchor hue. |
| AI nav (wordmark · 4 links centred · CTA right · sticky · hairline bottom) | Pick a nav shape that fits the genre. |
| AI footer (4 link columns · social icons · copyright) | Use a footer that closes the page, not a sitemap catalogue. |
| Aurora-blob mesh background (purple-pink-cyan) | Solid surface. Or subtle 2-stop gradient + SVG grain at <0.1 opacity. |
| Floating ambient 3D orbs | Cut them. Hero needs a typographic anchor, not depth. |
| Lazy-loaded LCP image | `fetchpriority="high"`. Lazy-load only below-the-fold. |

---

## Major (looks AI-generated)

| Tell | Fix |
|------|-----|
| Bounce/elastic easing on UI | Exponential ease-out only. |
| Everything centred, section after section | Break symmetry once — wide left margin, or the reverse. |
| Italic word dropped into every header | Headers are roman. Use weight or accent colour for emphasis. |
| Eyebrow label on every section (`01 / FEATURES`) | Zero eyebrows unless content is genuinely ordinal. Never two-column tag-left/header-right. |
| Coloured card glow shadow on dark background | Elevation via lightness (brighter surface = higher), not shadow. |
| Icon-tile feature card (rounded rect · coloured icon top-left · 2-line heading · copy) | Vary sizes and alignments, or drop the icon and lead with type. |
| Glassmorphism as decoration | Frosted glass only when it communicates depth over real content. |
| Animate-on-scroll on everything | One orchestrated entrance on load. After that, content just exists. |
| Mixed icon sets (Material + Heroicons + Lucide + emoji) | One library per project. Lucide for SaaS, Phosphor for weight variants. |
| Invented metrics ("10× faster", "50,000+ teams") | Use `—` placeholder, ask for the real number, or rebuild without the stat slot. |
| Generic emoji as feature icon (`✨ 🚀 ⚡`) | Pick an icon library. Or omit and lead with typography. |
| Re-drawn UI chrome (fake browser bar, phone frame, code window) | Real screenshot in `<figure>`. Typographic frame for code blocks. |
| Inline colour values drifting from the token set | Every colour and font must come through `var(--token-name)`. No inline hex mid-render. |
| Clickable text wrapping to two lines | Shorten the label. `white-space: nowrap`. Collapse nav below a threshold. |

---

## Microinteraction Tells

| Tell | Fix |
|------|-----|
| `transition-all` | Specify the properties explicitly. |
| `hover:scale-105` on every card | One signal per element — translate, colour shift, or underline. Never all. |
| Bouncy overshoot easings (`cubic-bezier(0.34, 1.56, ...)`) on buttons/modals | Reserve overshoots for drag-and-drop release only. |
| Auto-rotating carousel with no pause | Manual advance only, or pause-on-hover-and-focus. |
| Focus rings that animate in | Focus rings appear instantly. Never transition `outline` on focus. |
| Toasts that shift layout | Fixed position at viewport corner. Existing toasts don't move. |
| Spinner flashing for 50ms | Delay-show 150ms, or enforce 300ms minimum visible duration. |

---

## Minor (taste issues)

| Tell | Fix |
|------|-----|
| Straight quotes `"word"` in rendered text | Curly quotes `"word"`. |
| `--` instead of em-dash | `—` (U+2014). |
| `...` instead of ellipsis | `…` (U+2026). |
| Placeholder names "Jane Doe", "John Smith" | "Maya Okonkwo", "Sam Tan", "Elena Ruiz". |
| Product names "Nexus", "Pulse", "Seamless" | Concrete domain placeholder — "Maple Weekly", "Ridgeline Inventory". |
| `z-index: 9999` | Use a named 6-level z-scale. |
| Equal padding on every section | Vary. Tighten one, expand another. |
| `width: 100vw` | `width: 100%` with container padding. |
