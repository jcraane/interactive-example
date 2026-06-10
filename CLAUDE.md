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

- `exponential-growth.html` — exponential growth, as a bacteria-in-a-jar simulation: time
  slider, auto-play with teaching breakpoints, live growth curve (SVG), canvas particle animation.
- `three-door-problem.html` — the Monty Hall problem ("Het driedeurenprobleem").
- `birthday-paradox.html` — the birthday paradox: group-size slider, exact probability curve,
  and a Monte Carlo "run 100 rooms" simulation that converges on the theory.
- `compound-interest.html` — compound interest vs. linear saving: two savers racing on a shared
  curve, showing that starting early beats saving more.
- `simpsons-paradox.html` — Simpson's paradox: draggable scatter clusters whose per-group
  regression lines reverse direction when combined.

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

## Testing

Open the file in a browser. There is no test suite, lint, or build to run.
