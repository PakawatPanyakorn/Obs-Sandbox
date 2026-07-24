# Layout Doc Template

Every layout preset gets a companion `layouts/<name>.md` file, written when the layout is created (Create Mode step 6) and consulted again during Apply Mode. Its job is to capture judgment calls that the layout's JSON data cannot express on its own — not to restate `description` or copy `contentTypeVariants.bestFor/avoid` verbatim.

**Before writing one:** read the target layout's `.html` file in full — the JSON block *and* the rendered markup. Region guidance needs to cite the file's actual region names/classes and `regionSpans`, not generic composition advice.

**Bar for acceptance:** if a sentence would be equally true of a different layout with the names swapped, it's too generic — rewrite it with something specific to this archetype's actual grid, regions, or editorial devices.

**Relationship to `modules/shared-composition-archetypes.md`:** that file is the abstract, pre-file catalog consulted during Path C authoring of *new* layouts — the master definition of the archetype's *shape*. This doc is concrete guidance for *this exact built preset* — real class names, real region spans, real breakpoint behavior. Don't duplicate the archetype catalog's prose; build on it.

## Sections (use this exact structure)

```markdown
# <name>

**Archetype:** <archetype> · **Family:** <family>

## Core Concept
2-4 sentences restating the structural idea in plain terms — what hierarchy mechanism it uses (size, position, reading order, density) and why it isn't decorative. Name the specific "tell" that signals someone got it wrong (e.g. a shuffle test, a uniform-card-grid regression).

## When To Use
- Concrete content shapes/genres this fits — build on `contentTypeVariants.*.bestFor` but go further: describe the actual shape of content that fits, not a category label.

## When NOT To Use
- Concrete anti-fits — build on `contentTypeVariants.*.avoid` and `antiPatternCheck.notes`, explain the specific failure mode this archetype invites when misused.

## Region / Component Guidance
For each region in `composition.regions`: what real content belongs there, how much of it, and the one judgment call a user is likely to get wrong. Cite the actual region name/class and its `regionSpans` value.

## Content-Type Notes
One paragraph per `contentTypeVariants` key (textHeavy / chartHeavy / cardOrListHeavy), going beyond bestFor/avoid into "how to actually fill each region for this content type."

## Medium Notes
Only where `mediaAdaptation` has a real gotcha not obvious from the field itself (e.g. a fixed markdown degrade order, a slide-splitting rule).

## Pairing Notes
One line per entry in `exampleThemePairings`: when to reach for that pairing specifically vs. a different theme.
```
