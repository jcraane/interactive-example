# InteractiveExamples

A collection of interactive HTML visualizations that explain a single concept each. Each
example teaches one idea (exponential growth, the Monty Hall problem, …) through a hands-on,
animated, browser-based simulation.

## Core constraint: one self-contained file per example

Every example is a **single `.html` file** with all CSS and JavaScript inlined — no build
step, no bundler, no `<script src>` or `<link href>` to local files. Open the file directly
in a browser (`file://`) and it just works.

- Inline `<style>` in `<head>`, inline `<script>` before `</body>`.
- **No frameworks, no dependencies, no npm.** Vanilla JS, the DOM, `<canvas>`, and inline SVG only.
- External resources are limited to optional CDN web fonts (e.g. `three-door-problem.html`
  pulls Google Fonts via `@import`). Avoid other external assets; everything else must be
  embedded so the file works offline and stays portable.
- No backend, no persistence, no network calls for data.

## Files

All examples are in **Dutch** (`lang="nl"`).

- `index.html` — the landing page linking every example, with a one-line Dutch teaser each.
  Cards are generated from an `examples` array in the inline script; add a new example by
  appending one entry (`file`, `icon`, `title`, `tagline`, `accent`).
- `exponential-growth.html` — exponential growth, as a bacteria-in-a-jar simulation: time
  slider, auto-play with teaching breakpoints, live growth curve (SVG), canvas particle animation.
- `three-door-problem.html` — the Monty Hall problem ("Het driedeurenprobleem").
- `birthday-paradox.html` — the birthday paradox: group-size slider, exact probability curve,
  and a Monte Carlo "run 100 rooms" simulation that converges on the theory.
- `compound-interest.html` — compound interest vs. linear saving: two savers racing on a shared
  curve, showing that starting early beats saving more.
- `simpsons-paradox.html` — Simpson's paradox: draggable scatter clusters whose per-group
  regression lines reverse direction when combined.
- `false-positive-paradox.html` — base rate fallacy: a population grid where false positives
  visibly outnumber true positives for a rare condition, with prevalence/sensitivity/specificity sliders.
- `schelling-segregation.html` — Schelling's segregation model: a canvas grid of two agent
  types that self-sorts into clusters even at a low same-neighbour preference.
- `survivorship-bias.html` — survivorship bias (Wald's WWII planes): a hit simulation whose
  "returned planes" view shows holes avoiding the vital zones, revealing where armor really belongs.
- `evolution-of-trust.html` — the iterated prisoner's dilemma: play against AI personalities
  (copycat, grudger, …), then run an evolutionary tournament where the rounds-per-encounter
  slider decides whether cheaters or cooperators take over.
- `double-pendulum.html` — chaos theory / the butterfly effect: double pendulums released a
  thousandth of a degree apart diverge completely within seconds, with a live divergence meter.
- `coastline-paradox.html` — the coastline paradox: walk a shrinking ruler along a fractal
  coast and watch the measured length rise without limit (Richardson plot included).
- `regression-to-the-mean.html` — regression to the mean: praise the top scorers of a
  luck-based test and scold the worst, then watch both groups drift back to average; a
  skill-vs-luck slider controls how strong the effect is.
- `benfords-law.html` — Benford's law: first-digit histograms of embedded/generated datasets
  (country populations, powers of 2, Fibonacci, expenses) hug the logarithmic curve, while a
  "fabricated fraud" dataset trips the chi-square fraud gauge.
- `braess-paradox.html` — Braess's paradox: a live traffic network where opening a zero-cost
  shortcut makes every car's commute slower, with a central-planner button showing the system
  optimum vs. the Nash equilibrium.

Examples are independent — there is no shared library or cross-file dependency.

## Conventions (follow the existing files)

- **Structure:** `:root` CSS custom properties for the theme palette at the top of `<style>`,
  then component styles, then `@keyframes`. Markup in `<body>`, then a single `<script>` that
  grabs elements with `getElementById` and wires up `oninput`/`onclick` handlers.
- **Visual style:** rich, polished, animated. Gradient text, glassmorphism cards, CSS
  transitions for state changes, color-coded states (e.g. normal → `warning` → `danger`),
  `requestAnimationFrame` loops for continuous animation.
- **Pedagogy first:** the interaction should reveal the concept. Use staged reveals, insight
  callouts, milestone markers, and auto-play that pauses at key moments to let the idea land.
- **Intro card:** each example opens with a short (2–4 sentence) intro card placed after the
  title/subtitle and before the interactive widget. It frames the puzzle in plain language and
  teases the counterintuitive payoff — without giving away every number. Style it to match the
  file's palette and keep it readable (centered, ~560px max-width).
- **Language:** all examples are written in **Dutch** (`lang="nl"`). Keep every user-facing
  string — markup, button labels, messages, insight copy, number words (miljoen/miljard/…) —
  in natural Dutch. Element IDs, class names, and JS identifiers stay in English.
- **Self-documenting numbers:** format large/small values for humans (e.g. "1.2 billion",
  "< 0.001%") rather than raw figures.

## Adding a new example

1. Create one new `<concept-name>.html` (kebab-case) at the repo root.
2. Inline everything; depend on nothing local. Make it open-and-run.
3. Pick one concept and make the interaction *demonstrate* it — not just illustrate it.
4. Open with a short Dutch intro card (see Conventions); set `lang="nl"` and keep all
   user-facing copy in Dutch.
5. Register it on the landing page: add one entry to the `examples` array in `index.html`
   (`file`, `icon`, `title`, `tagline`, `accent`) with a one-line Dutch teaser.

## Testing

Open the file in a browser. There is no test suite, lint, or build to run.
