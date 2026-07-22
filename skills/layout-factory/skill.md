---
name: layout-factory
description: Manage structural layout presets — grids, spacing, composition, editorial hierarchy — to extract, browse, delete, and apply. Not colors or typography (use theme-factory for that); layout-factory owns structure only.
---

<what-to-do>

## Activation

This skill activates **only** when:

- User invokes the `/layout-factory` slash command, **or**
- User message contains the word **"layout"** paired with an action word (see table below)

A message containing "layout" alone (no action) is **not** a trigger — do not activate. ("I like this page's layout" is casual conversation, not a request.)

## Scope

layout-factory owns **structure only**: grid systems, spacing/rhythm, composition archetypes, region hierarchy, editorial devices (pull quotes, sidebars, footnotes, section breaks). It never sets color, font-family, shadow color, or gradient values — that is [theme-factory](../theme-factory/skill.md)'s job. The two compose: apply layout-factory to establish structure, then theme-factory to skin it (either order is safe — see coexistence rule in apply mode).

## Step 1: Detect Intent

| Mode       | Trigger (must include "layout" + one of these, or slash command)                                                                                            |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **create** | `layout extract` · `layout capture` · `layout save` · `layout design` · `layout create` · `create layout` · `design layout` · `make layout` · `new layout` · screenshot/HTML path + "layout" · "use the `<archetype>` layout for this" |
| **list**   | `layout list` · `list layouts` · `show layouts` · `browse layouts` · `what layouts`                                                                        |
| **delete** | `layout delete <name>` · `delete layout <name>` · `remove layout <name>`                                                                                    |
| **apply**  | `layout apply <name>` · `apply layout <name>` · `use layout <name>` · `layout <name> on <file>` · `restructure <file> as <name>`                            |

Ambiguous (has "layout" but action unclear) → ask: "Create, list, delete, or apply a layout?"

## Step 2: Execute Mode

### Create Mode

1. **Multi-layout check** — if source shows several distinct compositions, present a numbered list, wait for selection. "all" = extract each in sequence.
2. **Detect source** — Image / HTML file / Text or named archetype:
   - `.png/.jpg/.jpeg/.webp/.gif` or "screenshot" → **Path A**: read `modules/path-a-image-extraction.md`
   - `.html/.htm` or "from this HTML/page/file" → **Path B**: read `modules/path-b-html-extraction.md`
   - No file path, a text description, or a named archetype request ("Swiss grid", "Tufte-style") → **Path C**: read `modules/path-c-text-extraction.md`
3. For all paths, also read `modules/shared-grid-vocabulary.md` for grid/spacing terminology and `modules/shared-composition-archetypes.md` for the catalog of named archetypes to match or diverge from.
4. **Anti-pattern gate** — read `modules/anti-patterns.md`. Before writing anything, audit and silently fix all violations.
5. **Pick 2-3 theme-factory pairings** — check `modules/theme-pairing-log.md` for what's already been used, then pick real presets from `skills/theme-factory/themes/` that genuinely fit this archetype's family (prefer unused themes over convenient repeats; only repeat a theme when it's a strong fit for both presets). Pull actual color/typography/spacing values from the theme's file — never invent plausible-looking tokens. Add a row to `theme-pairing-log.md` after choosing.
6. **Write** preset HTML (using `modules/preset-template.html`) — demo content must explain the archetype (concept, hierarchy mechanism, best-fit use cases, when to reach for something else) through the actual regions being demonstrated, not fictional filler; the theme-preview tab row (defaulting to "No theme") lets the picked pairings be previewed live against the same structure; see the convention notes in `modules/preset-template.html` → **update** `index.html` LAYOUTS array → tell user the preset path and to open `~/.claude/skills/layout-factory/index.html` to preview

### List Mode

Tell the user: "Open [Layout Gallery](https://pakawatpanyakorn.github.io/Obs-Sandbox/skills/layout-factory/index.html) for global presets, or check `~/.claude/skills/layout-factory/layouts/` for local presets."

Do not read files, render previews, or summarize layouts.

### Delete Mode

1. Resolve path: `~/.claude/skills/layout-factory/layouts/<name>.html`
2. Check exists (Glob). If not: "No layout named '\<name\>' found."
3. Read file → show a structural summary (archetype, family, region count) as confirmation
4. Ask: "Delete layout **\<name\>**? This cannot be undone. Reply 'yes' to confirm."
5. On confirm: `Remove-Item "~/.claude/skills/layout-factory/layouts/<name>.html"`
6. Update `index.html`: remove the `{ filename: 'layouts/<name>.html', data: ... }` entry from `LAYOUTS` array, write back
7. Confirm: "Deleted layout **\<name\>**."

### Apply Mode

Read `modules/apply-mode-restructure.md` first — it is the entry point for every apply, regardless of target medium.

**Load layout** — read `~/.claude/skills/layout-factory/layouts/<name>.html`, parse JSON from `<script id="layout-data">`.

**Determine target medium**, then follow the matching branch in `modules/apply-mode-restructure.md`:

- **Existing HTML/CSS file** → do the shared content-mapping step, then hand off to `modules/apply-mode-html-implementation.md` for the CSS/markup implementation (signature markers, Path R vs Path F, theme-factory token coexistence).
- **Markdown/plain-text draft, or "help me write/structure this as a report/article"** (no file, or a non-HTML target) → content-restructuring branch in `modules/apply-mode-restructure.md`. No CSS involved — express regions/hierarchy/editorial devices directly in the target format.
- **Presentation/slide request** → slide-structuring branch in `modules/apply-mode-restructure.md`. Output a slide outline or slide markup, following the archetype's `mediaAdaptation.presentation` notes.

All branches run the full anti-pattern audit (`modules/anti-patterns.md`) against the result before reporting, and end with the structured change report described in `modules/apply-mode-restructure.md`.

</what-to-do>

<supporting-info>

Each preset is both a live browser preview and a JSON data store (`<script id="layout-data">`). Presets are named by composition archetype (e.g. `swiss-international-grid`, `magazine-well`), not by use-case — the same preset applies across report/analysis/presentation/article/web targets via `mediaAdaptation`.

</supporting-info>
