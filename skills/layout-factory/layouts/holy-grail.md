# holy-grail

**Archetype:** holy-grail · **Family:** dashboard-legitimate

## Core Concept

A five-band page chrome — full-width header, a narrow left navigation rail, a dominant body, a narrow right contextual rail, and a full-width footer — where the body is the only region that ever changes shape and both rails are pinned in place around it. The hierarchy mechanism is role, not scale: the left rail is where you go (it changes pages), the right rail is what's true about where you already are (it describes the current page). The tell that someone got it wrong is a right rail that reads identically no matter which page is open — that's decoration wearing navigation's clothes, and the fix is either giving it real page-scoped content or deleting it and falling back to `dashboard-with-rail`'s single rail.

## When To Use

- Documentation platforms and product docs sites where a persistent left nav tree coexists with a per-page "On this page" anchor list on the right (Stripe/Linear-style docs, but with the fuller four-zone chrome rather than just body + rail).
- Analytics/BI app shells where the outer chrome (header, section nav, footer) is stable across many reports, and only the report inside the body — plus a small page-scoped filter/legend in the right rail — actually changes.
- Admin consoles and CMS-style back-offices where the left rail browses categories/facets across a whole record set and the right rail shows detail on whichever single record is currently open.

## When NOT To Use

- Content with only one real navigable facet. Manufacturing a second rail just to look more "complete" is the specific failure mode this archetype invites — if the right rail's content would be identical regardless of the current page, drop to `dashboard-with-rail` instead.
- Static reports or single-author documents with no genuine navigable structure at all — reach for `magazine-well` or `data-dense-report-grid`, where any numbers live in running text or captioned exhibits, not orbiting rails.
- Anything destined for print or slides as its primary medium — two live rails have no printed or projected equivalent; see Medium Notes.

## Region / Component Guidance

- **`.lf-hg-header`** (`masthead`, spans `1 / 13`): brand/product name, a short top-level nav (2-4 items, not a full sitemap), and a right-aligned actions/status cluster. Keep it to one row — the judgment call people get wrong is adding a second header row of breadcrumbs or search, which starts competing with the left rail's job.
- **`.lf-rail`** (`rail`, spans `1 / 3`): grouped into `.lf-rail-section` blocks, each with a `.lf-rail-label` and either `.lf-rail-nav` (page links, one `.active`) or `.lf-rail-stats` (session-level numbers only — nothing page-scoped belongs here). The judgment call: this rail's contents must survive a page change unchanged in structure, only the `.active` item moves.
- **`.lf-body`** (`body`, spans `3 / 11`): the only region using `.lf-hero-panel` / `.lf-hero-exhibit` / `.lf-summary-zone` — the archetype's single allowed moment of visual weight. The judgment call: resist adding a third internal column here even when content feels cramped; split into two pages instead.
- **`.lf-rail-right`** (`sidenote`, spans `11 / 13`): reuses the same `.lf-rail-section`/`.lf-rail-label` vocabulary as the left rail, but its content (`.lf-rail-nav` as an anchor list, or `.lf-rail-meta` as a detail panel) must be scoped to the current body content specifically. The judgment call people get wrong most often: treating this as "more nav" and duplicating left-rail links into it.
- **`.lf-hg-footer`** (`footer`, spans `1 / 13`): 2-4 short facts (prev/next, last-updated, data source) in `.lf-hg-footer`'s flex row — never a full link sitemap, which belongs to a real site footer outside this app shell.

## Content-Type Notes

**textHeavy**: the left rail becomes the page tree; the right rail becomes an auto-generated `.lf-rail-nav` of on-page anchors, but only render it once the body has three or more `<h2>`s — a two-heading page gets no right rail at all rather than a token one-item list. The footer becomes prev/next plus a last-updated stamp.

**chartHeavy**: keep persistent, cross-page numbers (uptime, error rate) in the left rail's `.lf-rail-stats`, exactly as in `dashboard-with-rail`. The right rail instead holds a `.lf-rail-meta` scoped-metadata block or a small `.lf-rail-nav`-styled legend (series toggles) — never a second stats stack. The body still follows the summary-zone → hero-exhibit → smaller-exhibits sequence.

**cardOrListHeavy**: the left rail is category/status facets over the whole set (`.lf-rail-nav`); the body is `.lf-record-list`/`.lf-record-row` with one row carrying `.selected`; the right rail is that selected row's `.lf-rail-meta` detail panel and nothing else — it should visibly change every time a different row is selected, which is the clearest proof this rail is earning its place.

## Medium Notes

`mediaAdaptation.markdown` degrades harder here than in `dashboard-with-rail` because there are two "always visible" zones to lose, not one — render the left rail as a bullet list before the body and the right rail as a small table or short list immediately after the H1, and accept the persistent-visibility quality is gone entirely in a flat document. For print/slides, don't attempt a literal translation at all: extract the body alone and re-run it through a print-native or slide-native archetype instead of forcing this shell onto a page or projector.

## Pairing Notes

- **titanium-cloud** — reach for this when the deliverable really is a developer-platform docs site or SaaS app shell; its restrained grid and enterprise register read as the default "serious app" skin for this archetype.
- **prussian-blueprint** — reach for this when you want the two rails to feel like literal technical annotation (dimension ticks, leader lines) rather than app chrome — good for internal/ops tooling that wants to look deliberately instrumented.
- **bloc-brutus** — reach for this as the stress test: an unapologetically raw, structural register proving the five-band shell holds up even without any SaaS polish at all.
