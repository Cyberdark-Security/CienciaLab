# Design

<!-- impeccable:design-schema 1 -->

## World

Dark neon physics lab. The homepage (`src/dashboard-es.html`, copied to `build/index.html`
at deploy) opens with a Persuade-mode hero: a glowing wordmark over a **live, real**
double-pendulum canvas simulation (not a decorative image — actual physics ODE
integration), then drops into an Operate-mode grid of six glowing department panels.

Replaced an earlier editorial-magazine (light/paper) direction after explicit user
rejection ("no me gusta, quiero algo más llamativo, más marketing"); this is a full
redesign, not an amplification of that world — see git history for the discarded
version if it's ever needed as a reference.

## Typography

- Display/headings: **Unbounded** (hero wordmark, department numbers/titles), loaded via Google Fonts.
- Body/UI: **Manrope** (body copy, search input, footer, buttons).
- Hero wordmark uses a `flicker-in` keyframe (power-on effect) once on load; respects `prefers-reduced-motion` (both the flicker and the canvas are disabled).

## Color

Strategy: **Drenched** dark ground (`--void #05060a`, panels `--panel #10131c` /
`--panel-deep #0b0d14`) with a **Full palette** of six named neon department colors,
plus a separate cyan/magenta gradient (`--hero-a #37e6ff` / `--hero-b #ff3df0`) reserved
for the hero and CTA only — never reused as a category color, so the hero reads as its
own signature rather than a seventh category.

| Role | Hex | Used for |
|---|---|---|
| Péndulos | `#ffb020` | dept-pendulos heading/number/left-border/hover |
| Resortes y Osciladores | `#2de6c0` | dept-resortes heading/number/left-border/hover |
| Colisiones y Cuerpos Rígidos | `#ff4d5e` | dept-colisiones heading/number/left-border/hover |
| Movimiento en Rampas y Curvas | `#3d8bff` | dept-rampas heading/number/left-border/hover |
| Ecuaciones Diferenciales | `#b573ff` | dept-edp heading/number/left-border/hover |
| Experimental y Miscelánea | `#7fe3ff` | dept-experimental heading/number/left-border/hover |

Category colors are used as saturated text/border accents on dark panels (glowing
instrument-readout feel) rather than solid full-bleed fills — solid neon fills at that
scale would fail body-text contrast, so the panels stay near-black with colored accents
instead. Verified contrast: body/blurb text (`--text-dim #8993a8`) on panel background
is ≈6:1 (passes WCAG AA); CTA button text (`#05060a`) on the hero gradient is ≈7:1.

## Layout / Components

- Hero: full-viewport-ish section, canvas absolutely positioned behind centered text, `text-shadow` glow on the wordmark, gradient pill CTA linking to `#departamentos`.
- Live canvas simulation: real semi-implicit-Euler double-pendulum integration (not a GIF/video), cyan bob + magenta bob with a fading magenta trail; disabled entirely under `prefers-reduced-motion: reduce`.
- Search: same client-side substring filter as before (unchanged logic), restyled dark with a cyan focus glow.
- Departments: dark panel headers with a colored left inset-border + colored heading/number text + a pill-shaped count badge; entries grid below on `--panel-deep`, each entry tinted with that department's color only on hover/focus (10% tint background + colored text + left border).

## Constraints

- Static HTML only, no build step for this page — self-contained (`<style>`/`<script>` inline).
- License notice (`© Erik Neumann 2020, Apache 2.0`) stays in the footer — legal requirement, kept visually quiet (small, dim text), not removed.
- Links point at `-es.html` build output paths (`sims/<category>/<App>-es.html`) — adding/removing an app in `src/sims/` needs a matching manual edit here (no dynamic generation).
- The double-pendulum canvas is decorative-but-real; don't replace it with a static image or GIF — that would make the copy ("no es una imagen: es una simulación corriendo ahora mismo") false.
