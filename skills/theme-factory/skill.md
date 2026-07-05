---
name: theme-factory
description: Manage visual theme presets to extract, browse, delete, and apply.
---

<what-to-do>

## Activation

This skill activates **only** when:

- User invokes the `/theme-factory` slash command, **or**
- User message contains the word **"theme"** paired with an action word (see table below)

A message containing "theme" alone (no action) is **not** a trigger — do not activate.

## Step 1: Detect Intent

| Mode        | Trigger (must include "theme" + one of these, or slash command)                                                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **create**  | `theme extract` · `theme capture` · `theme save` · `theme design` · `theme create` · `create theme` · `design theme` · `make theme` · `new theme` · screenshot/HTML path + "theme" |
| **list**    | `theme list` · `list themes` · `show themes` · `browse themes` · `what themes`                                                                                                     |
| **delete**  | `theme delete <name>` · `delete theme <name>` · `remove theme <name>`                                                                                                              |
| **apply**   | `theme apply <name>` · `apply theme <name>` · `use theme <name>` · `theme <name> on <file>`                                                                                        |

Ambiguous (has "theme" but action unclear) → ask: "Create, list, delete, or apply a theme?"

## Step 2: Execute Mode

### Create Mode

1. **Multi-theme check** — count distinct themes. Single → proceed. Multiple → present numbered list, wait for selection. "all" = extract each in sequence.
2. **Detect source** — Image / HTML file / Text:
   - `.png/.jpg/.jpeg/.webp/.gif` or "screenshot" → **Path A**: Read `modules/path-a-image-extraction.md`
   - `.html/.htm` or "from this HTML/page/file" → **Path B**: Read `modules/path-b-html-extraction.md`
   - No file path / describes theme in words → **Path C**: Read `modules/path-c-text-extraction.md`
3. For all paths, also read `modules/shared-color-slots.md` for the 14-slot color reference and `modules/shared-design-dna.md` for the design DNA taxonomy.
4. **Anti-pattern gate** — Read `modules/anti-patterns.md`. Before writing anything, audit and silently fix all violations.
5. **Write** preset HTML (using `modules/preset-template.html`) → **update** `index.html` THEMES array → tell user the preset path and to open `~/.claude/skills/theme-factory/index.html` to preview

### List Mode

Tell the user: "Open [Theme Gallery](https://pakawatpanyakorn.github.io/Obs-Sandbox/skills/theme-factory/index.html) for global presets, or check `~/.claude/skills/theme-factory/themes/` for local presets."

Do not read files, render swatches, or summarize themes.

### Delete Mode

1. Resolve path: `~/.claude/skills/theme-factory/themes/<name>.html`
2. Check exists (Glob). If not: "No theme named '\<name\>' found."
3. Read file → show swatch summary as confirmation
4. Ask: "Delete theme **\<name\>**? This cannot be undone. Reply 'yes' to confirm."
5. On confirm: `Remove-Item "~/.claude/skills/theme-factory/themes/<name>.html"`
6. Update `index.html`: remove the `{ filename: 'themes/<name>.html', data: ... }` entry from `THEMES` array, write back
7. Confirm: "Deleted theme **\<name\>**."

### Apply Mode

**First, detect if the file was previously themed by this skill** — grep for the comment pattern `/* Theme: <anything> - applied by obs-theme-factory */` inside the file's `<style>` block. If the pattern matches, use **Path R**; otherwise use **Path F**.

Read `modules/apply-mode-token-harmonize.md` for the full token template, harmonize steps, and report format.

**Load theme** — read `~/.claude/skills/theme-factory/themes/<name>.html`, parse JSON from `<script id="theme-data">`, note background lightness. Then proceed with the matched path below.

---

#### Path R: Re-theme (file already has a theme-factory `:root` block)

Fast swap — the structure is already harmonized; only values change.

1. **Replace token values** — find the existing `/* Theme: … - applied by obs-theme-factory */` `:root` block and overwrite every CSS variable value in-place with the new theme's values. Update the comment to the new theme name. Use `Edit`, never rewrite the whole file.
2. **Final touch** — scan for obvious mismatches only:
   - Hardcoded hex colors in JS/SVG blocks that clash with the new palette → swap to nearest theme token hex
   - Colored sections (hero, header, callout) whose gradient or bg now visually clashes → update to new theme's `--gradient-hero` or `--color-primary`
   - Background pattern: if new theme changes `background.type` (e.g. solid → pattern), update `body` background properties to match new `--bg-*` tokens
3. **Report** using the report format in `modules/apply-mode-token-harmonize.md` (note "Re-theme" in header)

---

#### Path F: First apply (file has never been themed by this skill)

The theme is a **starting point** — designer reskin, not find-replace. Goal: page looks intentionally designed for this theme with no visible seams.

**Production-grade means:** WCAG AA contrast everywhere; no color invisible after mode switch; JS SVG colors audited.

1. **Audit target file** — identify color mode, mode switch, shorthand vars, hardcoded colors, colored sections, JS hardcoded colors
2. **Inject `:root` block** — add token block at top of `<style>` using the template in `modules/apply-mode-token-harmonize.md`; use `Edit`, never rewrite whole file
3. **Harmonize** — follow steps 4a–4k in `modules/apply-mode-token-harmonize.md`
4. **Report** using the report format in `modules/apply-mode-token-harmonize.md`

</what-to-do>

<supporting-info>

Each preset is both a live browser preview and a JSON data store (`<script id="theme-data">`).

</supporting-info>
