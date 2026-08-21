# Plan: Combine R + Stata PIP decks into one

Create a new deck `PIP_In_R_and_Stata.qmd` that shows the shared intro once, then presents every language-specific topic as a single slide with an **R** tab and a **Stata** tab (Quarto `panel-tabset`), with both engines executing live on render.

## Steps

1. **Scaffold the file** — Copy the YAML header from the R deck; set title to "Poverty and Inequality Platform (PIP): an introduction using R and Stata", author to Diana C. Garcia Rojas only, keep `custom.css`, `simple` theme, logo, slide numbers.
2. **Combined setup chunk** — One `{r}` chunk loading `Statamarkdown`, `pipr`, `tidyverse`, `ggthemes`; then a `{stata, collectcode=TRUE}` setup chunk (`set linesize 200`, `pip cl, clear`).
3. **Shared intro (Sections 1–2)** — Single copy: Outline (reworded to "R and Stata"), Poverty data at WB, The PIP, Motivation, Transparency ×2, Publications, Data on inequality, Welfare-measure image slides + the detailed **Steps 1–5 panel-tabset** (from R deck), process3–7 images, "Accessing via UI".
4. **Section 3 — Accessing PIP (tabset per topic)** — For each aligned topic, one slide with `::: panel-tabset` → **R** tab (executing `{r}` chunk + inline output) and **Stata** tab (executing `{stata}` chunk + any exported `.svg`). Topics: Installation, Country-level estimates, Variables, Ghana estimates (+notes, +2017 PPP), Different/Multiple poverty lines, Selected countries, Interpolated/extrapolated, Poverty by welfare type, by reporting level, Within-country comparability, LIS, Global/regional estimates, Global poverty plot, Many more functions. *Shared conceptual slides* ("Two main functions" text, "Extrapolation for Ghana" image) stay single, no tabs.
5. **Language-only topics — add cross-language equivalents so every topic has both an R tab and a Stata tab:**
   - **Auxiliary data** (was R-only `get_aux`): add a Stata tab using `pip tables, clear` (list all auxiliary tables) and `pip tables, table(cpi) clear` (fetch a specific table, e.g. CPI). Include the short explanatory note: PIP's main data are household surveys but it also uses many auxiliary sources (GDP, CPI, population, etc.).
   - **Shared Prosperity / inequality** (was Stata-only): add an R tab using `get_stats(country = "GHA")` and selecting/filtering for `gini` and `pg`.
   - **Versioning** (`get_versions`, `release_version`): keep R-only (no direct Stata equivalent) with a brief note; do not fabricate a Stata command.
6. **Section 4 — Exercises** — Same two exercises; each Results slide uses a `panel-tabset` with **R** and **Stata** tabs, each tab containing its code chunk then its plot (R inline, Stata via exported `.svg`) to avoid nested tabsets.
7. **Section 5 — Resources + Acknowledgment + Thank you** — Single copy; Thank-you slide contacts = Diana C. Garcia Rojas only.

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
- Auxiliary data: give both languages — R `get_aux`, Stata `pip tables` / `pip tables, table(cpi)` with the auxiliary-data note.
- Shared Prosperity / inequality: give both languages — Stata as-is, R via `get_stats` selecting `gini` and `pg`.
- Versioning: R-only (no Stata equivalent), keep with a short note.
- Thank-you slide contacts: Diana C. Garcia Rojas only.
- Exercise results layout: R/Stata tabs each holding its code + plot.
