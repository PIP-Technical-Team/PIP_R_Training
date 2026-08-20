# Plan: Combine R + Stata PIP decks into one

Create a new deck `PIP_In_R_and_Stata.qmd` that shows the shared intro once, then presents every language-specific topic as a single slide with an **R** tab and a **Stata** tab (Quarto `panel-tabset`), with both engines executing live on render.

## Steps

1. **Scaffold the file** — Copy the YAML header from the R deck; set title to "Poverty and Inequality Platform (PIP): an introduction using R and Stata", author to Diana C. Garcia Rojas only, keep `custom.css`, `simple` theme, logo, slide numbers.
2. **Combined setup chunk** — One `{r}` chunk loading `Statamarkdown`, `pipr`, `tidyverse`, `ggthemes`; then a `{stata, collectcode=TRUE}` setup chunk (`set linesize 200`, `pip cl, clear`).
3. **Shared intro (Sections 1–2)** — Single copy: Outline (reworded to "R and Stata"), Poverty data at WB, The PIP, Motivation, Transparency ×2, Publications, Data on inequality, Welfare-measure image slides + the detailed **Steps 1–5 panel-tabset** (from R deck), process3–7 images, "Accessing via UI".
4. **Section 3 — Accessing PIP (tabset per topic)** — For each aligned topic, one slide with `::: panel-tabset` → **R** tab (executing `{r}` chunk + inline output) and **Stata** tab (executing `{stata}` chunk + any exported `.svg`). Topics: Installation, Country-level estimates, Variables, Ghana estimates (+notes, +2017 PPP), Different/Multiple poverty lines, Selected countries, Interpolated/extrapolated, Poverty by welfare type, by reporting level, Within-country comparability, LIS, Global/regional estimates, Global poverty plot, Many more functions. *Shared conceptual slides* ("Two main functions" text, "Extrapolation for Ghana" image) stay single, no tabs.
5. **Language-only topics** — R-only (`get_aux` dictionary, Versioning) and Stata-only (Shared Prosperity/inequality) rendered as single-language tabs (see consideration 1).
6. **Section 4 — Exercises** — Same two exercises; each Results slide uses a `panel-tabset` with **R** and **Stata** tabs, each tab containing its code chunk then its plot (R inline, Stata via exported `.svg`) to avoid nested tabsets.
7. **Section 5 — Resources + Acknowledgment + Thank you** — Single copy (lists are near-identical).

## Relevant files

- `PIP_In_R_and_Stata.qmd` (new) — the combined deck.
- `PIP_In_R.qmd` — source for R chunks, YAML header, Steps 1–5 tabset.
- `PIP_In_Stata.qmd` — source for Stata chunks; note the `collectcode=TRUE` chain must keep document order.
- `custom.css`, `_quarto.yml` — reused as-is.

## Verification

1. `quarto render PIP_In_R_and_Stata.qmd` completes without errors (requires R + pipr and Stata + Statamarkdown on the render machine).
2. Open the generated HTML: confirm each Section 3/4 slide shows working R and Stata tabs with real output, and Stata `.svg` plots display.
3. Confirm Stata collectcode-dependent slides (e.g. `describe`, within-country `keep if`) still produce correct output in combined order.

## Decisions

- Tabset-per-slide structure; both languages execute live; author = Garcia Rojas only; detailed Welfare Steps 1–5 included.

## Further Considerations

1. Language-only topics (`get_aux`/versioning R-only; Shared Prosperity Stata-only; "Many more functions" is an image in R but `pip tables` output in Stata). Recommendation: keep them as a single-language tab with a short note. Option A: single tab as-is / Option B: add an equivalent in the other language / Option C: drop them.
2. Thank-you slide contacts — the two decks list different people. Recommendation: keep the full combined contact list. Option A: full list / Option B: Garcia Rojas only.
3. Exercise results layout — Recommendation: R/Stata tabs each holding code+plot. Option A: this / Option B: flat tabs (R Code, R Plot, Stata Code, Stata Plot).
