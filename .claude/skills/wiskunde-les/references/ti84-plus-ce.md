# TI-84 Plus CE — keystroke reference

The learner uses a **TI-84 Plus CE**. Every GR callout gives exact keystrokes for this model.

**Priority:** if the textbook chapter contains its own GR instructions ("Werken met de GR",
"GR-practicum", a TI box), follow the book: same order, same menu names. This file only fills
gaps. Menu *numbers* shift between OS versions; when unsure, name the menu item
(`MATH → logBASE(`) and leave the number out rather than guess.

## How to write keystrokes in a lesson

- Each physical key is a `<span class="key">…</span>` (styled in the template). Second
  functions are two keys: `<span class="key">2nd</span> <span class="key">TRACE</span>`, then the
  name in parentheses: "(CALC)".
- Menu choices are written as they appear on screen: `<span class="key">5:intersect</span>`.
- Screen text (menus, `Y1=`, results) is English on the calculator. Keep it English; the
  explanation around it is Dutch.
- Show a `gr-screen` with what the learner should *see* when it went right, so they can compare.
- The x-variable is typed with `X,T,θ,n`; never tell them to type the letter X via ALPHA.

## Settings

| Doel | Toetsen |
|---|---|
| Radialen / graden | `MODE` → pijl naar `RADIAN` of `DEGREE` → `ENTER` → `2nd` `MODE` (QUIT) |
| Aantal decimalen | `MODE` → regel `FLOAT 0 1 2 …` → kies → `ENTER` |
| Functiemodus (standaard) | `MODE` → `FUNCTION` (bij rijen: `SEQ`) |
| Terug naar startscherm | `2nd` `MODE` (QUIT) |

Status bar on a CE shows the mode: `NORMAL FLOAT AUTO REAL RADIAN MP`. A lesson that depends on
the angle unit should show this bar in the `gr-screen`.

## Typing

| Wat | Toetsen | Valkuil |
|---|---|---|
| Negatief getal | `(−)` (naast ENTER) | De aftrek-toets `−` geeft `ERR:SYNTAX` aan het begin |
| π | `2nd` `^` | |
| √ | `2nd` `x²` | |
| eˣ | `2nd` `LN` | |
| 10ˣ | `2nd` `LOG` | |
| Macht | `^` (kwadraat: `x²`) | Haakjes om negatieve grondtallen: `(−2)^2` |
| Breuk (stapel) | `ALPHA` `Y=` (F1) → `1:n/d` | |
| Uitkomst als breuk | `MATH` → `1:▶Frac` → `ENTER` | |
| log met grondtal | `MATH` → `logBASE(` (of `ALPHA` `WINDOW` (F2) → `logBASE(`) | |
| Vorig antwoord | `2nd` `(−)` (ANS) | |

## Graphs

| Doel | Toetsen |
|---|---|
| Formule invoeren | `Y=` → typ achter `Y1=` (x met `X,T,θ,n`) |
| Plotten | `GRAPH` |
| Venster instellen | `WINDOW` → `Xmin`, `Xmax`, `Xscl`, `Ymin`, `Ymax`, `Yscl` |
| Standaardvenster | `ZOOM` → `6:ZStandard` |
| Goniometrisch venster | `ZOOM` → `7:ZTrig` |
| Y passend maken | `ZOOM` → `0:ZoomFit` |
| Langs de grafiek lopen | `TRACE` + pijltjes |
| Tabel instellen | `2nd` `WINDOW` (TBLSET) → `TblStart`, `ΔTbl` |
| Tabel bekijken | `2nd` `GRAPH` (TABLE) |
| Y1 in een berekening | `ALPHA` `TRACE` (F4, YVAR) → `Y1` → typ `(3)` → `ENTER` |

## The CALC menu: `2nd` `TRACE`

| Doel | Keuze | Wat de GR vraagt |
|---|---|---|
| Functiewaarde | `1:value` | `X=` → typ waarde → `ENTER` |
| Nulpunt | `2:zero` | `Left Bound?` → `Right Bound?` → `Guess?` (telkens `ENTER`) |
| Minimum | `3:minimum` | `Left Bound?` → `Right Bound?` → `Guess?` |
| Maximum | `4:maximum` | `Left Bound?` → `Right Bound?` → `Guess?` |
| Snijpunt | `5:intersect` | `First curve?` `ENTER` → `Second curve?` `ENTER` → `Guess?` cursor bij het snijpunt → `ENTER` |
| Helling in een punt | `6:dy/dx` | `X=` → waarde → `ENTER` |
| Integraal | `7:∫f(x)dx` | `Lower Limit?` → `Upper Limit?` |

Classic mistakes worth a "Let op":
- Several intersections: the GR returns the one nearest the `Guess?` cursor. Move it first.
- The point isn't in the window → `ERR:INVALID` or a wrong point; adjust `WINDOW` first.
- Answers are decimal approximations: in exact-answer exercises ("bereken exact") the GR is only
  for checking.

## Numeric tools (MATH menu)

| Doel | Toetsen |
|---|---|
| Afgeleide in een punt | `MATH` → `8:nDeriv(` → bv. `nDeriv(Y1, X, 2)` |
| Integraal | `MATH` → `9:fnInt(` |
| Vergelijking numeriek oplossen | `MATH` → `Solver…` / `Numeric Solver…` (onderaan het MATH-menu) → vergelijking invullen → `SOLVE`. The input screen differs per OS version (`0=` vs `E1=`/`E2=`), so prefer the book's own steps or the intersect method |
| Max/min van een functie op interval | `MATH` → `fMin(` / `fMax(` |

## Probability (kansrekening)

| Doel | Toetsen |
|---|---|
| Combinaties nCr | `MATH` → tab `PRB` → `3:nCr` (snelmenu: `ALPHA` `WINDOW` (F2) → `nCr`) |
| Permutaties nPr | `MATH` → `PRB` → `2:nPr` |
| Faculteit | `MATH` → `PRB` → `4:!` |
| Kansverdelingen | `2nd` `VARS` (DISTR) → `binompdf(` / `binomcdf(` / `normalcdf(` / `invNorm(` |

On the CE the DISTR functions open a fill-in form (`trials:`, `p:`, `x value:` /
`lower:`, `upper:`, `μ:`, `σ:`). Name the fields as shown, e.g. "vul bij `trials` 5 in".
`binomcdf` gives P(X ≤ k). For P(X ≥ k) the learner computes `1 − binomcdf(n, p, k − 1)`, which
is a classic mistake and worth a "Let op".

## Statistics and regression

| Doel | Toetsen |
|---|---|
| Data invoeren | `STAT` → `1:Edit` → lijsten `L1`, `L2` |
| Gemiddelde, standaardafwijking | `STAT` → tab `CALC` → `1:1-Var Stats` → `List: L1` → `Calculate` |
| Lineaire regressie | `STAT` → `CALC` → `4:LinReg(ax+b)` |
| Exponentiële regressie | `STAT` → `CALC` → `ExpReg` |
| Lijst wissen | `STAT` → `4:ClrList` |

## Sequences (rijen)

`MODE` → `SEQ`, then `Y=` shows `u(n)=`, `u(nMin)=`. `n` via `X,T,θ,n`; `u` via `2nd` `7`.
Return to `FUNCTION` mode afterwards. Forgetting this breaks the next chapter's graphs, so the
callout should say so.
