# Design DNA

`aesthetic` and `personality` are a **closed vocabulary** — pick from the lists below, never invent a term. The gallery turns every distinct tag into a filter chip, so an invented word becomes a filter that matches exactly one theme. If nothing fits perfectly, the closest three listed tags still describe the theme better than a new word nobody can browse by.

| Dimension        | Values                                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| aesthetic        | **exactly one of:** editorial / ornate / crafted / technical / playful / glassmorphism / minimal / brutalist / corporate |
| personality      | **3 of the 21 below** (2 or 4 only when the theme genuinely warrants it)                                          |
| density          | compact / comfortable / spacious                                                                                 |
| elevation        | flat / subtle / layered / dramatic                                                                               |
| borderStyle      | none / hairline / subtle / bold                                                                                  |
| motionFeel       | instant / subtle / expressive; estimate duration-fast/base/slow ms                                               |
| surfaceTexture   | flat / frosted / gradient / noise / none                                                                         |
| iconStyle        | outlined / filled / rounded / sharp / duotone                                                                    |
| hierarchyClarity | low / medium / high                                                                                              |
| spaceUnit        | nearest 4px or 8px multiple                                                                                      |
| notes            | Anything distinctive not captured above                                                                          |

## Aesthetic — pick one

| Value | Means |
| --- | --- |
| `editorial` | print/publication reading surface; type does the work |
| `ornate` | decorative, historical ornament, luxury flourish |
| `crafted` | handmade/material/earthy, the making is visible |
| `technical` | instrument, terminal, blueprint, readout |
| `playful` | pop, toy, bright consumer energy |
| `glassmorphism` | glass, blur, glow depth |
| `minimal` | reductive and quiet (covers flat and soft-UI/neumorphic treatments) |
| `brutalist` | raw, hard-edged, confrontational |
| `corporate` | institutional, business, finance |

## Personality — pick 3

Plain-language mood words, chosen so a browser can filter by them. Grouped only to help you choose; the groups carry no meaning in the JSON.

| Group | Tags |
| --- | --- |
| era & mood | `retro` · `futuristic` · `aged` · `historic` · `moody` · `dreamlike` |
| light & color | `glowing` · `colorful` · `monochrome` |
| feel | `calm` · `soft` · `warm` · `bold` · `elegant` |
| making & structure | `handmade` · `industrial` · `geometric` · `type-led` |
| register | `formal` · `analytical` · `utilitarian` |

Two rules:

- **Don't restate another field.** `light`/`dark` belong to background lightness (the gallery derives its own Tone filter and strips those words). Never use an aesthetic name as a personality tag.
- **Don't describe the technique, describe the feel.** "misregistered", "phosphor", "wabi-sabi" belong in `notes` or the theme's `.md` doc, not in a tag someone has to browse by.
