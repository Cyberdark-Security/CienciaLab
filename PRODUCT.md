# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack
Existing codebase: static HTML/CSS/JS built from TypeScript via `tsc` + `esbuild`, with HTML assembled by Perl macro-expansion (`prep_html.pl` + `macros.html`). No backend, no database. Deployed via GitHub Actions to GitHub Pages (`Cyberdark-Security/CienciaLab`), fully static output in `build/`.

## Users
General curious public, not necessarily formal physics students — visitors browsing out of curiosity rather than following a course or classroom assignment. No assumed prior physics background.

## Product Purpose
CienciaLab is a Spanish-language interactive physics simulation lab: a fork of myPhysicsLab (pendulums, springs, collisions, rigid-body engine2D, roller/ramp paths, PDE strings, misc/experimental sims) with a full `es` locale added throughout, so visitors can explore and manipulate real-time physics simulations entirely in Spanish.

## Positioning
The distinguishing value is being **the Spanish-language version** of myPhysicsLab — the same real-time interactive physics engine, but usable by a Spanish-speaking audience who would otherwise only get English (or German). It is not a different simulation engine or a curated subset; it is the same ~100 simulations, translated.

## Operating Context
The raw build output includes a developer test index (`index-{locale}.html`, one link per app, no styling) inherited from the upstream project — this is not the public-facing homepage and should not be treated as one. The public entry point is a new dashboard landing page (in scope for the current work) that organizes the same simulations by physics topic for a general visitor, replacing that raw index as the site root.

## Capabilities and Constraints
- All ~100 simulations already exist and work; this work is presentation/navigation, not new simulation features.
- **License constraint (binding):** code is Apache License 2.0, copyright Erik Neumann. The published site must retain a copyright/license notice somewhere in the actual deployed pages (not only in the GitHub README) — this is a legal requirement of the license, not a design choice. It can be small/unobtrusive (e.g. a footer line) but must not be removed from the live site.
- Categories for the dashboard (confirmed): Péndulos, Resortes y Osciladores, Colisiones y Cuerpos Rígidos, Movimiento en Rampas/Curvas, Ecuaciones Diferenciales, Experimental. Category-to-source-folder mapping: Péndulos ← `sims/pendulum`; Resortes y Osciladores ← `sims/springs`; Colisiones y Cuerpos Rígidos ← `sims/engine2D`; Movimiento en Rampas/Curvas ← `sims/roller`; Ecuaciones Diferenciales ← `sims/pde`; Experimental ← `sims/experimental` and `sims/misc`.
- Site is public and free to run: GitHub Pages + GitHub Actions on a public repo, no paid services.

## Brand Commitments
Name: "CienciaLab" (repo `Cyberdark-Security/CienciaLab`). No existing logo/visual identity beyond the inherited myPhysicsLab logo image (`src/images/myphysicslogo.png`), which belongs to the upstream project.

## Evidence on Hand
- Existing translated source: every simulation class already has `es_strings` (Spanish UI labels) wired into `Util.LOCALE === 'es'`.
- `src/index_order.txt` likely lists app ordering/paths used by the existing build tooling.
- No user testimonials, analytics, or usage data exist yet — this is a new public launch.

## Product Principles
- The Spanish translation is the product's whole reason to exist — never regress it or bury it behind English-first defaults.
- Respect upstream license/attribution obligations without letting them dominate the visitor-facing design.
- Organize for a curious general visitor's mental model (physics topics), not the codebase's folder structure.
- Don't invent simulations, categories, or claims beyond what already exists in the codebase.
