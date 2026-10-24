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
- Screen text (menus, `Y1=`, status bar, results) follows the language of the book's screens; see
  "Screen language" below. The explanation around it is always Dutch.
- Show a `gr-screen` with what the learner should *see* when it went right, so they can compare.
- The x-variable is typed with `X,T,θ,n`; never tell them to type the letter X via ALPHA.

## Screen language

A CE can be set to English or Dutch. Copy whatever the book's screenshots show, because the
learner compares the lesson with the book. Getal & Ruimte H12 (Rijen) shows a Dutch-language CE;
the H13 lessons use English.

- **Dutch screens:** use the Dutch text and name the English term once per tab, in the form
  "Antw (Engelstalige GR: Ans)". Each tab must make sense on its own, so a second tab may repeat it.
- **Key labels stay English** in both cases, because that is what is printed on the keys and above
  them: `2nd` `WINDOW` (TBLSET), `2nd` `GRAPH` (TABLE), `MODE`.
- **Don't guess Dutch menu text** the book doesn't show. Describe the item instead ("de regel met
  de grafiektypes", "de functiemodus (Engelstalige GR: FUNCTION)").

| Engels | Nederlands (zoals in G&R H12) |
|---|---|
| `NORMAL FLOAT AUTO REAL RADIAN MP` | `NORM DRIJF AUTO REËEL RAD WN` (let op de Ë, en WN in plaats van MP) |
| `Ans` | `Antw` |
| `SEQ` (MODE) | `RIJ` |
| `TYPE: SEQ(n) SEQ(n+1) SEQ(n+2)` | `TYPE: RIJ(n) RIJ(n+1) RIJ(n+2)` |
| `PRESS + FOR ΔTbl` | `DRUK OP + VOOR ΔTbl` |
| `PRESS ENTER TO EDIT` | `DRUK OP ENTER VOOR BEWERKEN` (cursor op een kolomkop) |

## Settings

| Doel | Toetsen |
|---|---|
| Radialen / graden | `MODE` → pijl naar `RADIAN` of `DEGREE` → `ENTER` → `2nd` `MODE` (QUIT) |
| Aantal decimalen | `MODE` → regel `FLOAT 0 1 2 …` → kies → `ENTER` |
| Functiemodus (standaard) | `MODE` → `FUNCTION` (bij rijen: `SEQ`) |
| Terug naar startscherm | `2nd` `MODE` (QUIT) |

Status bar on a CE shows the mode: `NORMAL FLOAT AUTO REAL RADIAN MP` (Dutch:
`NORM DRIJF AUTO REËEL RAD WN`). A lesson that depends on the angle unit should show this bar in
the `gr-screen`.

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
| Vorig antwoord | `2nd` `(−)` (ANS) | Op een Nederlandstalige GR staat er `Antw` op het scherm |

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

Screen text below is English; for a Dutch-language book use the table in "Screen language"
(SEQ → RIJ, Ans → Antw).

### Without sequence mode

| Doel | Toetsen | Valkuil |
|---|---|---|
| Recursief doorrekenen op het basisscherm | beginterm → `ENTER`, dan de formule met `2nd` `(−)` (ANS) op de plaats van uₙ₋₁ (bv. `1.05*Ans−100`) → `ENTER`, `ENTER`, … | Na k keer `ENTER` sta je bij u_k: dat is de (k + 1)e term. Begint de invoer met + − × ÷, dan zet de GR zelf `Ans` ervoor |
| Directe formule in een tabel | `Y=` → formule met `X,T,θ,n` voor n → `2nd` `WINDOW` (TBLSET) `TblStart=0`, `ΔTbl=1` → `2nd` `GRAPH` (TABLE) | X is het rangnummer n, niet de telling: bij beginterm u₀ hoort X = 9 bij de tiende term |

### Sequence mode

| Doel | Toetsen |
|---|---|
| Rijenmodus aan | `MODE` → regel `FUNCTION PARAMETRIC POLAR SEQ` → `SEQ` → `ENTER` → `2nd` `MODE` (QUIT) |
| Rij invoeren | `Y=` toont `TYPE: SEQ(n) SEQ(n+1) SEQ(n+2)`, `nMin=`, `u(n)=`, `u(nMin)=`. De labels tonen het echte getal: bij `nMin=0` staat er `u(0)=` en `u(1)=` |
| u, v, w typen | `2nd` `7` / `8` / `9`; n met `X,T,θ,n` |
| Beginterm u₀ of u₁ | `nMin=0` met `u(0)=…`, of `nMin=1` met `u(1)=…` |
| Recursieve formule | `u(n)=1.05u(n−1)−100`, `u(0)=1000` |
| Formule als Pₙ₊₁ = … | TYPE `SEQ(n+1)` → `u(n+1)=1.25u(n)−100`, of herschrijf tot `u(n)=1.25u(n−1)−100` |
| Twee begintermen (Fibonacci) | `u(n)=u(n−1)+u(n−2)` met de tweede beginterm bij `u(nMin+1)=` |
| Directe formule | `u(n)=2n²−3n+4`, beginterm leeg laten |
| Tabel | `2nd` `WINDOW` (TBLSET) → `TblStart` = nMin, `ΔTbl=1` → `2nd` `GRAPH` (TABLE); kolommen `n` en `u(n)` |
| Somrij Sₙ | `u(n)=…` en `v(n)=v(n−1)+u(n)` met `v(nMin)=u(nMin)`; de tabel toont `n`, `u(n)`, `v(n)` |
| Som vanaf n = a | `nMin=a`, `v(a)=u(a)`, `TblStart=a` (of S_b − S_{a−1} uit één tabel vanaf 0) |
| Terug naar functies | `MODE` → `FUNCTION` → `ENTER` |

Classic mistakes worth a "Let op":
- `nMin` stays on its last value (1 after a reset). With beginterm u₀, set it to 0 first.
- A recursive `u(n)` with an empty `u(nMin)` gives an error in the table.
- `u` typed via `ALPHA` is a variable, not the sequence: always `2nd` `7`.
- A table cell shows at most 6 characters (`17226.9` → `17227`). Put the cursor on the cell to see
  the full value at the bottom of the screen.
- "De hoeveelste term" is n + 1 when the beginterm is u₀; "vanaf welke n" is the rangnummer itself.
- Return to `FUNCTION` mode afterwards. Forgetting this breaks the next chapter's graphs, so the
  callout should say so.

Book convention (G&R): in the uitwerking the learner writes down what they enter, e.g. "Voer in
u(n) = 1,05u(n − 1) − 100 met nMin = 0 en u(0) = 1000".
