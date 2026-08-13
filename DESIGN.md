# Design

<!-- impeccable:design-schema 1 -->

## World

Editorial science-magazine table of contents. The homepage (`src/dashboard-es.html`,
copied to `build/index.html` at deploy) reads as a Spanish-language print magazine's
department spread, not an app dashboard — refuses the flat white-card / single-blue-accent
SaaS-dashboard default and the chalkboard-physics-classroom cliché.

## Typography

- Display/headings: **Piazzolla** (serif, italic wordmark, department titles), loaded via Google Fonts.
- Body/UI: **Public Sans** (sans, body copy, labels, search input, footer).
- One settle-in keyframe animation on the masthead wordmark only (`@keyframes settle`); no other motion.

## Color

Strategy: **Full palette**, six named department roles, each owning a full-width header
band (not a scattered accent). Paper ground `#f2efe7` / `#eae5d8`, ink `#1b1a17` /
`#55524a`, rule `#d8d2c1`.

| Role | Hex | Used for |
|---|---|---|
| Péndulos | `#8f5a1e` | dept-pendulos header band |
| Resortes y Osciladores | `#1f7a6c` | dept-resortes header band |
| Colisiones y Cuerpos Rígidos | `#a83a2e` | dept-colisiones header band |
| Movimiento en Rampas y Curvas | `#2456a6` | dept-rampas header band |
| Ecuaciones Diferenciales | `#6b3f8f` | dept-edp header band |
| Experimental y Miscelánea | `#4a4f57` | dept-experimental header band |

All six pass WCAG AA (≥4.5:1) against the white header text (`#fbf9f3`) at body-copy
size; verified by computing relative luminance directly (`Péndulos` was originally
`#b9782a` at 3.45:1 and was darkened to `#8f5a1e` for this reason — don't lighten it
back without re-checking contrast).

Each department also has a darker `-ink` variant (e.g. `--c-pendulos-ink`) used only as
link-hover text color on the paper background, never as a background fill.

## Layout / Components

- Masthead: wordmark + small-caps kicker line, 3px bottom rule, never reflows on scroll.
- Cover band: one serif editorial sentence + a plain-text stat line (count of sims/sections) — status is printed text, never an icon or badge.
- Search: single text input, client-side substring filter (normalizes accents), filters only on each entry's own label text (not department name — matching by department name was tried and reverted, see history, because it surfaced unrelated entries).
- Departments: numbered kicker (`01`–`06`) + title + one-line blurb + simulation count, in a solid-color band; entries below in a 3/2/1-column responsive grid (breakpoints 860px, 560px) on the paper-deep ground, with a colored left-border on hover matching that department's role color.

## Constraints

- Static HTML only, no build step for this page — self-contained (`<style>`/`<script>` inline), so it never depends on the Perl macro pipeline or `tsc`/`esbuild`.
- License notice (`© Erik Neumann 2020, Apache 2.0`) must stay in the footer of the live site — this is a license requirement, not a design choice; don't remove it, only keep it visually quiet.
- Links point at the `-es.html` build output paths (`sims/<category>/<App>-es.html`) — if an app is renamed/added/removed in `src/sims/`, this page's link list needs a matching manual update (no dynamic generation).
