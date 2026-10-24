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

## Two kinds of example

Most files are **continuous animations** ("Animaties"): slide/drag to discover one idea live.
The project also has step-by-step **Kennisbank** explainers that walk through a worked
calculation one reveal at a time, and **Techniek** examples that demystify a technical/web
concept (CORS, HTTP, …) — both still single self-contained files in the same visual style.
A file picks its bucket on the landing page via the optional `category` field (see below);
no `category` means it lands in "Animaties". The known categories live in `categoryMeta`
(`Animaties`, `Techniek`, `Kennisbank`, `Wiskunde`); add a new key there to introduce another section.
**Wiskunde** examples are school-math lessons (explanation + practice) and live in the
`wiskunde/` subfolder; their `file` entry in `index.html` includes that path. They are built
from a textbook chapter with the `wiskunde-les` project skill (`.claude/skills/wiskunde-les/`),
which holds the shared template and house style. They use the Tailwind Play CDN — an accepted
exception to the no-dependency rule for this folder, for now.

## Files

All examples are in **Dutch** (`lang="nl"`).

- `index.html` — the landing page linking every example, with a one-line Dutch teaser each.
  Cards are generated from an `examples` array in the inline script; add a new example by
  appending one entry (`file`, `icon`, `title`, `tagline`, `accent`, and optional `category`
  and `paragraaf`). `paragraaf` (e.g. `'13.3'`) shows as a "§ 13.3" pill next to the card's icon;
  every Wiskunde lesson sets it so the student sees at once which book section it covers. A value
  that doesn't start with a digit is shown as-is, without the §-sign (`'H12 Voorkennis'`).
  Cards are grouped into sections by `category` (first-seen order); `categoryMeta` holds each
  section's label icon + tag. Omit `category` to fall under the default "Animaties" section.
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
- `moire-patterns.html` — Moiré interference: overlay two fine line gratings and rotate one a
  fraction of a degree to make giant fringe bands sweep across that exist in neither grid.
- `shepard-tone.html` — the Shepard tone (auditory barber-pole): octave-stacked sine partials
  under a fixed loudness bell glide upward and wrap, with a live spectrum/waterfall; Web Audio,
  starts only on a user gesture.
- `phantom-traffic-jam.html` — phantom traffic jams: cars on a ring road following an IDM model
  spontaneously break into a backward-traveling stop-and-go shock wave past a critical density.
- `pid-controller.html` — the PID controller: a cart-on-a-beam plant the user tunes with Kp/Ki/Kd
  sliders (plus presets) to see overshoot, steady-state error, and critically-damped settling.
- `cors-explained.html` — CORS as the browser's gatekeeper ("de poortwachter van je browser"): an
  animated request-flow simulator. The user composes a cross-origin call (method, JSON vs form body,
  custom header, cookies/credentials) and the server's response (`Access-Control-Allow-Origin` value,
  preflight approval), then a packet animates browser→server→back through a CORS gate while a live HTTP
  console logs the headers. Demonstrates the four teaching cases: simple call allowed, simple call
  blocked-but-the-server-still-ran (200 in the log, error in the console), preflight rejected (real
  request never sent), and credentials voiding a `*` wildcard. Scenario presets jump to each case.
- `kansverdeling-volleybal.html` — **Kennisbank** (`category: 'Kennisbank'`): a step-by-step
  derivation of the probability distribution of a volleyball best-of-5 (how many sets A the match
  lasts). A "Volgende stap" navigator reveals the derivation one block at a time; a live p-slider
  (Racing's per-set win chance) recomputes every number, a bar chart, and the running table so the
  three probabilities always sum to 1. Includes a set-sequence visualizer (drawing the orderings
  each combination counts) and an "x boven y" / nCr mini-widget with the cancel-down trick, the
  factorial formula, and a styled TI-84 Plus keystroke callout.
- `wiskunde/toepassingen-van-sinusoiden.html` — **Wiskunde** (`category: 'Wiskunde'`), §13.2 of
  Getal & Ruimte H13 and the follow-up to the §13.1 lesson: from graph or data to the formula
  y = a + b sin(c(x − d)) and calculating with it. The thread is "één periode = vier kwarten": an
  animated quarter-period explorer, a formula stappenplan where the student picks d and sees a
  falling crossing give the mirrored graph, a six-question explorer for Theorie B (max/min without
  GR, value, intersect, dy/dx, max slope, domain wrap) with a live TI-84 Plus CE screen, a year-model
  explorer for Theorie C (Napels, zeewater: data → a, b, c, d, dagnummers, time above a threshold),
  and 11 auto-checked book exercises ending in a graph matcher on figuur 13.15.
- `wiskunde/formules-herschrijven.html` — **Wiskunde** (`category: 'Wiskunde'`), §13.3 of
  Getal & Ruimte H13 "Allerlei formules" (the same chapter as the two sinusoid lessons): breuken
  herleiden, variabelen vrijmaken and formules combineren. The chapter has no figures, so the thread
  is "herleiden verandert de vorm, niet de waarde": an invul-controle explorer (pick a rewrite and see
  whether its graph covers the original everywhere, including a coincidence at x = y = 2), herleidings-
  ladders for Theorie A and B where every line shows its value for slider-chosen numbers and a
  "klassieke fout" toggle shows the wrong line breaking, a terugreken-graph for vrijmaken, a 4-step
  combineren stappenplan whose route dots line up on the combined formula, and 12 auto-checked book
  exercises (fill-in boxes in a given form) ending in a matcher on opgave A53c. Book-style fractions
  and roots come from a small `fm()` markup helper (`{teller|noemer}`, `√[…]`, `^[…]`, `#1`).
- **H12 Rijen** (Getal & Ruimte, five lessons). They share concept colours (beginterm u₀/b emerald,
  rekenkundige rij / verschil v / lineair sky, meetkundige rij / factor r / exponentieel rose,
  rangnummer n amber, somrij / Σ violet) and show the simulated TI-84 Plus CE screens in Dutch, as
  the book does (`NORM DRIJF AUTO REËEL RAD WN`, `Antw`, `RIJ(n)`, `DRUK OP + VOOR ΔTbl`), naming
  the English term once.
- `wiskunde/lineaire-en-exponentiele-groei.html` — **Wiskunde** (`category: 'Wiskunde'`,
  `paragraaf: 'H12 Voorkennis'`), the Voorkennis of H12 (Theorie A "Tabellen bij groei") and the
  run-up to §12.1. A deliberately compact lesson: three theory tabs plus exactly the 7 book
  exercises. The thread is "plus of keer": an editable book-table explorer that animates each step's
  difference and quotient and judges the table linear, exponential or neither (including the
  n = 2, 5, 9 table with unequal steps); a "hak de stap in stukjes" explorer that turns +12 / ×1,5
  per 3 uur into per-uur values (g = 1,5^⅓, g⁷ = 600/716) with a "1,5 : 3" classic-mistake toggle;
  a 4-step formula stappenplan on the three Theorie A examples; and opgaven 1–7, ending in a matcher
  where a line and an exponential curve both pass through (3, 320) and (7, 20).
- `wiskunde/rekenkundige-en-meetkundige-rijen.html` — **Wiskunde**, §12.1. The thread is "u₀ is de
  eerste term": a regelmaat explorer on opgave 1 (term strip with u-index, ordinal count,
  difference/quotient badges, hidden next term), a recursief-vs-direct explorer where [enter] steps a
  simulated TI-84 basisscherm (Antw) while a slider jumps straight to uₙ, Formule-Labs for rr
  (n treden van v, lineair verband) and mr (×r, exponentieel verband, rr comparison), a 5-step
  "de hoeveelste term?" stappenplan that separates "de hoeveelste term" (n + 1) from "vanaf welke
  n", and 12 auto-checked book exercises ending in a rr/mr matcher on the dots of opgave 14B.
- `wiskunde/notaties-en-rijen-op-de-gr.html` — **Wiskunde**, §12.2: beginterm u₀ of u₁, formules
  opstellen bij twee gegeven termen, notaties (Aₙ, u(n), uₙ₊₁) and the rijen-invoerscherm. The thread
  is "andere nummering of notatie, dezelfde rij": a u₀/u₁ explorer whose dots slide one place while
  (n − 1) appears in the formula, a 4-step stappenplan from two terms to the direct formule (checked
  against a third term), a notation translator with the "losse n wordt n + 1" mistake, and a TI-84
  Plus CE sequence-mode simulator with a small formula parser (type `1.05u(n-1)-100`, nMin, two
  initial values, RIJ(n+1)) feeding a table and a bounds-highlighting graph; 12 auto-checked book
  exercises end in a matcher.
- `wiskunde/toepassingen-van-rijen.html` — **Wiskunde**, §12.3: recursive formulas that mix a
  percentage factor with a fixed amount (uₙ = r · uₙ₋₁ + b) and patterns whose recursive formula is
  derived from the direct one. A bar explorer builds each term as ·factor then ±amount (opgave 41,
  the tank), a formula builder checks factor/amount/beginterm against the story with per-mistake
  feedback, a Rij-Lab shows the equilibrium line (orange), "constant houden" and a "first n where
  uₙ < …" search with a simulated TI-84 table, a pattern explorer (fig 12.2 cubes, triangular numbers
  with the fig 12.4 doubling), a 4-step direct → recursive stappenplan, and 12 auto-checked book
  exercises ending in a tank matcher.
- `wiskunde/somrijen.html` — **Wiskunde**, §12.4: the sigma notation and the somrij. The thread is
  "elke som is de vorige som plus één nieuwe term": a row-by-row counting animation (figuur 12.7
  tulpen, vak K, bierkratten), a sigma explorer that writes Σ out term by term with the book's
  underbraces, a stacking explorer for Sₙ = Sₙ₋₁ + uₙ with a live TI-84 screen (v(n)=v(n−1)+u(n),
  table, v(nMin) error toggle), an Sₙ-graph explorer for Σ from a to b (S_b − S_{a−1} vs. nMin = a)
  and "vanaf welke n", a 5-step stappenplan, and 12 auto-checked book exercises ending in a somrij
  matcher. A lesson-level `fs()` helper (markup: `data-fs`) extends `fm()` with `Σ[k = 0|5]`
  (bounds above and below the Σ) and subscripts (`u_k`, `u_[n − 1]`).

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

1. Create one new `<concept-name>.html` (kebab-case) at the repo root (Wiskunde topics go in `wiskunde/`).
2. Inline everything; depend on nothing local. Make it open-and-run.
3. Pick one concept and make the interaction *demonstrate* it — not just illustrate it.
4. Open with a short Dutch intro card (see Conventions); set `lang="nl"` and keep all
   user-facing copy in Dutch.
5. Register it on the landing page: add one entry to the `examples` array in `index.html`
   (`file`, `icon`, `title`, `tagline`, `accent`) with a one-line Dutch teaser.

## Testing

Open the file in a browser. There is no test suite, lint, or build to run.
