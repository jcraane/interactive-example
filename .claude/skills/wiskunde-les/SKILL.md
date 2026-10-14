---
name: wiskunde-les
description: Turn a chapter or paragraph of a Dutch secondary-school math textbook (usually a PDF from Getal & Ruimte, Moderne Wiskunde or similar) into an interactive, single-file Dutch HTML lesson in this repo's `wiskunde/` folder, in the house style of `wiskunde/periodieke_verschijnselen.html`. The lesson has tabbed theory with live canvas explorers, a parameter lab, a step-by-step werkschema, TI-84 Plus CE keystroke callouts and auto-checked book exercises with a score. The skill also registers the lesson on the landing page under "Wiskunde". Use it whenever someone in this project hands over a wiskunde PDF, hoofdstuk, paragraaf, textbook pages or photos of them, or asks to "uitleggen", "een les maken van", "interactief maken" or add a new math topic, even without mentioning this skill, the template or HTML.
---

# Wiskunde-les

Turn a textbook chapter into an interactive lesson that a secondary-school student opens
**next to their book**. Every lesson in `wiskunde/` should feel like the same product. Two things
make that happen:

- the fixed shell in `assets/lesson-template.html`: header, tabs, helpers and exercise engine;
- the conventions below.

`wiskunde/periodieke_verschijnselen.html` is the full worked example of the format. Read it when
a component's use isn't clear from the template. The format is still being validated with a real
learner, so if the user gives feedback on a lesson, ask whether it should go into this skill too.

## What you produce

1. `wiskunde/<onderwerp-in-kebab-case>.html`, one self-contained file.
2. One entry in the `examples` array in `index.html`, with `category: 'Wiskunde'`.
3. One bullet in the **Files** list of `CLAUDE.md`.

Don't commit unless asked.

## Workflow

### 1. Read the whole chapter

Read the PDF with the Read tool's `pages` parameter (at most 20 pages per call; go through all
of them). Look at the page images, not just the text. Figure values, axis scales and the
exact numbers in examples come from the images, and the lesson stands or falls on those
numbers matching the book. If the request names a topic but gives no material, ask for the
pages. The lesson follows *this* book's order, terms and numbering.

### 2. Write a lesson plan before any HTML

Write `lesplan.md` in the scratchpad. A full lesson is ~1500–2000 lines, and without a plan it's
easy to drop a figure value or let a concept's colour drift halfway through. Cover:

```markdown
# Lesplan: Hoofdstuk <n> <titel> (<boek>, <niveau als bekend>)

## Kernbegrippen → conceptkleur
- evenwichtsstand → rose · amplitude → sky · periode → amber · startpunt → emerald

## Theorieblokken (in boekvolgorde)
- Theorie A (p. 12): <kern in één zin> | figuren: 13.2 (min 1 bij t=0, max 6 bij t=2,5) | voorbeeld: …
## Werkschema's / stappenplannen uit het boek
## Afspraken en valkuilen ("Let op", "Afspraak", typische fouten)
## GR-gebruik in het boek (welke handelingen, met welke toetsen als het boek ze geeft)

## Tabbladen
1. Basisbegrippen: <verkenner: wat beweegt, welke figuren als presets>
2. …
N. Oefenopdrachten (k)

## Oefenopdrachten
| # | Boek-ref | Type | Gegevens | Antwoord(en) | tol | Hint (aanpak) | Uitwerking |
```

### 3. Solve and check every exercise you include

Work out each answer yourself and check it numerically with a short `node -e` script. Books
often have no answer key in the chapter, and one wrong checker teaches the student that the
right answer is wrong. That damages trust far more than a missing exercise. If a value can only be
read off a figure, note the reading and give the checker a tolerance that fits.

### 4. Build from the template

Copy `assets/lesson-template.html` to `wiskunde/<naam>.html` and fill it in. What to keep and
what to change:

- **Keep as-is:** `<head>` styles, header, tab navigation pattern, back-link to `../index.html`,
  and everything under `HULPFUNCTIES` and `NAVIGATIE` in the script (`fmt`, `fmtPi`,
  `parseNum`, `approx`, `setupCanvas`, `drawGraph`, `setActiveButton`, `switchTab`), plus the
  exercise engine (`checkExercise`, `showUitwerking`, `updateScore`). Lessons look and behave the
  same because they share this code.
- **Replace:** every `{{…}}` placeholder and every block marked `✏️`. The template's demo content
  (parabolas) only shows how each component works. Delete what the chapter doesn't need.
- **Add:** extra tabs by copying the explorer card. Register each tab in `tabRenderers`.

Use `drawGraph` for every coordinate graph instead of hand-drawing axes. It handles retina
sharpness, Dutch tick labels (`xTick: fmtPi` for π-axes), clipping, dashed help lines, points
and asymptote jumps, and it returns `mapX`/`mapY` for custom overlays (a ferris wheel, a unit
circle, shading).

### 5. Verify

- Extract the inline `<script>` and run `node --check` on it.
- Run a node script that recomputes each exercise's answer from the book data and compares it to
  the targets in `exercises`. Also feed Dutch-notation inputs (`"0,5"`, `"¼π"`, `"−3"`) through
  `parseNum` to confirm they pass.
- If a browser tool is available, serve the folder over `http://` (Playwright blocks `file://`),
  click through every tab, check the console for errors and screenshot each tab once to judge
  the layout. If you can't, say that the lesson wasn't viewed in a browser.

### 6. Register and report

Add the `index.html` entry after the existing Wiskunde entries:

```js
{
  file: 'wiskunde/<naam>.html',
  icon: '<één emoji die het onderwerp vangt>',
  title: '<Onderwerp zoals in het boek>',
  tagline: '<Eén zin: wat je ziet gebeuren of wat verrast, plus wat erin zit (stappenplan, N oefenopdrachten).>',
  accent: '<hex die past bij het onderwerp>',
  category: 'Wiskunde',
},
```

Add the `CLAUDE.md` bullet in the same style as the others. Then report back in a few
lines: the file, the tabs, the number of exercises, and anything you skipped or weren't sure
about (an unreadable figure value, an exercise left out because it needs drawing on paper).
Suggest the user check it next to the book.

## Lesson structure

Use 4–6 numbered tabs. The order follows the student's path: understand → see → try →
practise. The student may jump straight to the exercises, so each tab must make sense on its own.

| Tab | When | What's in it |
|---|---|---|
| **1. Basisbegrippen** | always | The intro card is the first paragraph: 2–4 sentences on the everyday situation the chapter opens with and what the student will be able to do. Then one concept card per core concept, each in its concept colour with a formula chip. Then a **verkenner** of the chapter's opening figure(s): presets labelled "Figuur 13.2", toggles for help lines in the concept colours, and a live uitleg-box with the current numbers. |
| **Theory tabs** | one per theory block, in book order (merge small ones, split large ones) | A short explanation card and one verkenner. The verkenner must *demonstrate*: the student changes something and the concept becomes visible as a consequence. A picture that only illustrates is not enough. |
| **Formule-Lab** | when the chapter has a formula with parameters | Live formula in the dark pill, one slider panel per parameter in its concept colour, derived quantities shown live (periode = 2π / c), and presets "Voorbeelden uit het boek". |
| **Stappenplan** | when the book has a werkschema or a procedure the exercises keep using | Step buttons, a canvas that builds up cumulatively per step, an explanation panel with the actual numbers of the chosen example, Vorige/Volgende, and 2–3 presets (the book's voorbeeld plus exercises). |
| **Oefenopdrachten (k)** | always, last | See below. |

Put these inside the tab where they matter, not in a tab of their own:

- **GR callouts** (TI-84 Plus CE). Read `references/ti84-plus-ce.md`.
- **Let op callouts** (amber) for the book's afspraken and the classic mistakes.

When something is a must-do setting (radians!), give the callout a `border-2 border-amber-300` and a
"Cruciale afspraak" tag, as in the worked example.

## Exercises

Choose **8–12** exercises that together cover every theory block and every *type* of question
in the chapter. Prefer the book's own exercises with the book's numbers, labelled so the student
can find them: `Opdracht 5 • Opgave 5h (Figuur 13.4a)`. If you vary the numbers of a book
exercise, label it `Variant op opgave 7`.

Card types are in the template:

- **numeric:** 1–3 fields, optionally with a canvas that redraws the book figure;
- **multiple choice:** good for formula recognition and "wat gaat er mis?";
- **matcher:** adjust parameters until your graph covers the target. Use it once, as the final
  `Einduitdaging`.

Include at least one question built on a Let-op or GR pitfall.

The `exercises` object is declarative. Each entry has `fields`, `choice` or `check`, plus
`tol`, `hint`, `goed` and `uitwerking`. Rules:

- **The hint points at the method and the place in the lesson, never at the answer.** For example:
  "Gebruik periode = 2π / c (zie tab 3)." The worked solution appears only after a correct answer
  or after two wrong tries. If the first miss gives the answer away, practice turns into copying.
- **Accept how students actually type.** `parseNum` handles `0,5`, `1/4`, `¼`, `1½`, `−3`, `2π`
  and `pi/4`. Give multiple valid answers as an array (`'q9-d': [1, 3]`). Give rounded answers a
  matching `tol` (0,05 for "afronden op 1 decimaal", wider for values read off a graph).
- **State the expected form in the label** whenever there's ambiguity: "c (in π)",
  "afgerond op 2 decimalen", "in uren".
- The score in the header counts automatically from `exercises`. Keep the tab label's count
  `Oefenopdrachten (k)` equal to the number of cards.

## Graphs that match the book

- Reproduce each figure from points you can read off it, and leave the derivation in a comment:
  `// Fig 13.4a: max 20 bij t=1, min −10 bij t=4, periode 6 → a=5, b=15, d=−0,5`.
  The student compares the screen with the book. A curve that is slightly off reads as "I
  don't understand it", not as "the drawing is wrong".
- Use the book's axis ranges, steps and variable names (`t` in uren, `h` in meters), and π-ticks
  when the book uses them.
- Canvas `width`/`height` attributes are the logical size. Keep `class="w-full h-auto"`.
- Animations run in a `requestAnimationFrame` loop that only draws while its tab is visible
  (see `animateLoop`).

## Language and notation

- All visible text is Dutch, in **the book's terminology** ("evenwichtsstand", not
  "middenlijn"), in the je-form, with short sentences at the book's level. IDs and JS
  identifiers stay English or neutral, as in the template.
- Displayed numbers use a **decimal comma**. Run everything through `fmt` (also slider labels and
  canvas text). Formulas use book notation: `·`, `−` (U+2212), `½`, `¼π`, superscripts `²`.
- Formulas are text in `.mono`. The live/featured formula goes in the dark slate pill. Don't use
  MathJax or KaTeX.

## House style

These are fixed. They're what makes the lessons recognisable as one series.

- Use the Tailwind Play CDN plus the Inter / JetBrains Mono fonts exactly as in the template. This is
  a deliberate exception to the repo's no-dependency rule, agreed with the user for now. Add no
  other libraries, no `alert()` and no network calls.
- Light theme. Body is `slate-50`. Cards are `bg-white rounded-2xl p-6 shadow-sm border border-slate-200`.
  `h2` is `text-xl font-bold text-slate-800`. Body text is `text-slate-600`.
- Sticky indigo→violet header with a "Wiskunde • Hoofdstuk N" badge, the title, the score
  pill and the tab bar.
- **Colour has meaning.** Indigo is UI: buttons, active states and the student's own curve. Each
  core concept gets one colour from amber / rose / sky / emerald / violet / orange in the
  lesson plan, and keeps it *everywhere*: concept card, slider panel, toggle dot, canvas line,
  legend. The student learns "rose = evenwichtsstand" without being told. Neutral things are slate.
- Responsive: use `lg:grid-cols-12` splits (canvas 7–8, controls 4–5) and `md:grid-cols-2` exercise
  cards. The tab bar scrolls horizontally on phones.
