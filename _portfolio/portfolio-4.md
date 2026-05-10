---
title: "Income-Quintile Inflation Indices for Mexico"
excerpt: "Constructs monthly inflation indices by household income quintile in Mexico, combining ENIGH 2024 expenditure structure with INEGI INPC subrubro series.<br/><img src='/images/inflquintil_inflacion_quintiles_2026m4.png'>"
collection: portfolio
---

## Overview

This project produces **five monthly inflation indices for Mexico, one per household income quintile**, by combining the expenditure structure observed in the ENIGH 2024 household survey with monthly INPC subrubro series from INEGI. The output is a panel of quintile-specific consumer price indices and year-over-year inflation rates from 2019 onward, refreshed each month, that quantifies heterogeneous price exposure across the income distribution.

## Data Pipeline

The pipeline ingests two complementary sources and joins them through a product-level concordance.

- **INPC subrubros (INEGI BIE).** 95 subrubro-level monthly price series are pulled from INEGI's BIE portal in `000_datos_inpc.R`. Because the portal is an ASP.NET application, each request first scrapes the `__VIEWSTATE` and `__EVENTVALIDATION` tokens via `httr2` + `rvest`, then issues the gridwise POST to retrieve the data tables. The result is a wide-format monthly panel `inpc_subrubros_2025.rds` covering 2018 to the current month.
- **ENIGH 2024 (INEGI).** Household-level expenditure microdata: `concentradohogar.dta`, `gastoshogar.dta`, and `gastospersona.dta`, loaded with `haven`.
- **Concordance.** A helper script (`000_relacion_enigh_inpc.R`) builds the mapping between ENIGH product codes (`clave`) and INPC CCIF subrubros, including dual-periodicity items that report under more than one frequency.

## Methodology

1. **Periodicity-adjusted spending.** ENIGH records consumption at weekly, monthly, quarterly, and semi-annual frequencies. In `001_ingreso_gasto.R`, each record is rescaled to a common monthly equivalent before any aggregation.
2. **Income quintiles.** Households are ranked by deflated current income and partitioned into five quintiles, weighting by ENIGH's expansion factor (`factor`) so each quintile represents the same share of the underlying population.
3. **Expenditure weights.** In `002_ponderadores.R`, the weighted-mean monthly spending per subrubro within each quintile is divided by total spending in that quintile to obtain the share matrix `W (5 × S)`.
4. **Index construction.** With the INPC subrubro panel `P (T × S)`, the quintile index panel is computed as the matrix product

   $$I_{T \times 5} \; = \; P_{T \times S} \; W^{\top}_{S \times 5}$$

   Year-over-year inflation per quintile is then `I[t,q] / I[t-12,q] - 1`.
5. **Incidence decomposition.** In `003_incidencias.R`, the contribution of subrubro *s* to the monthly change of the index in quintile *q* is

   $$\text{inc}_{s,q,t} \; = \; \frac{P_{s,t} - P_{s,t-1}}{I_{q,t-1}} \times w_{s,q} \times 100$$

   This attributes month-on-month index movements back to individual subrubros and underpins the heatmap and top-5 visualizations.

## Code Architecture

Six R scripts, run in order by `Master_quintiles.R`:

1. `000_datos_inpc.R` — scrape and cache INPC subrubro series from the BIE portal.
2. `001_ingreso_gasto.R` — load ENIGH 2024, normalize spending periodicity, map products to subrubros, build quintiles.
3. `002_ponderadores.R` — compute per-quintile expenditure weights and the quintile-level inflation indices.
4. `003_incidencias.R` — decompose monthly variation into subrubro contributions; build heatmaps (current month vs. 12-month rolling average).
5. `004_incidencia_top5_serie.R` — time series of the top-5 contributing subrubros.
6. `005_stack_anual_mismomes.R` — stacked year-over-year same-month comparison.

A helper, `000_relacion_enigh_inpc.R`, rebuilds the ENIGH ↔ INPC product concordance and is run manually when codes change between ENIGH waves.

## Outputs — April 2026

![Annual inflation by income quintile, 2019–2026](/images/inflquintil_inflacion_quintiles_2026m4.png)
*Year-over-year inflation rate of the consumer price index by income quintile, monthly from January 2019 through April 2026.*

![Total monthly incidence by quintile](/images/inflquintil_incidencias_quintiles_2026m4.png)
*Total monthly incidence (contribution to the month-on-month change of the index) for each quintile, April 2026.*

![Heatmap of subrubro contributions, Panel A](/images/inflquintil_panel_a_2026m4.png)
*Heatmap, Panel A: top 10 subrubros by absolute contribution to the monthly change in each quintile's index. Two facets show the current month (April 2026) and the trailing 12-month rolling average.*

![Top-5 incidence subrubros over time](/images/inflquintil_top5_va_2026m4.png)
*Time series of the five subrubros with the largest contribution to the year-over-year change of each quintile's index, with the latest observation in April 2026.*

![Stacked same-month year-over-year comparison](/images/inflquintil_stack_mismomes_2026m4.png)
*Stacked composition of the annual inflation rate for the month of April across recent years, decomposed by subrubro group, for each income quintile.*

## Tools

R (`tidyverse`, `data.table`, `haven`, `httr2`, `rvest`, `xml2`, `ggplot2`, `furrr`, `future`), ENIGH 2024, INEGI BIE.
