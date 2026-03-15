---
title: "Age-Period-Cohort Effects on Labor Market Trends in Mexico"
excerpt: "Decomposing Mexican labor market trends into age, cohort, and period effects using ENOE pseudo-panels (2005–2025).<br/><img src='/images/apc_figura1.png' alt='Labor participation and unemployment rates by education and gender'>"
collection: portfolio
---

## Overview

This project replicates and extends Duval-Hernández & Orraca Romano (2009) using quarterly data
from the ENOE (Encuesta Nacional de Ocupación y Empleo) spanning 2005–2025. The objective is to
decompose Mexican labor market trends into three structural components:

- **Age effect (α)** — life-cycle changes in labor market outcomes as workers age.
- **Cohort effect (κ)** — persistent generational differences between birth cohorts, holding age constant.
- **Period effect (τ)** — cyclical fluctuations tied to the macroeconomic environment.

**Variables analyzed:** labor force participation, unemployment, formal wage employment, informal
wage employment, self-employment, and overemployment (>40 hrs/week, original extension).

---

## Data & Pseudo-Panel Construction

Individuals are grouped into cells defined by gender (male/female), education level (basic ≤6 yrs,
intermediate 7–12 yrs, higher >12 yrs), age (20–70), and quarter (2005Q1–2025Q4). Cells with
fewer than 100 unweighted observations are dropped, yielding **36 models** (6 groups × 6 outcomes).

| Dimension | Categories |
|---|---|
| Gender | Male, Female |
| Education | Basic (≤6 yrs), Intermediate (7–12 yrs), Higher (>12 yrs) |
| Age | 20–70 |
| Period | 2005Q1–2025Q4 |

| Outcome | Numerator | Denominator |
|---|---|---|
| Labor force participation | Labor force (PEA) | Working-age population |
| Unemployment | Unemployed | Labor force |
| Formal wage employment | Salaried workers with social security | Employed |
| Informal wage employment | Salaried workers without social security | Employed |
| Self-employment | Employers + own-account workers | Employed |
| Overemployment *(extension)* | Salaried workers with >40 hrs/week | Salaried employed |

---

## Methodology

The model is estimated in log-odds form:

$$\text{logit}(p_{ct}) = \theta + \alpha_a + \kappa_c + \tau_t + \varepsilon_{ct}$$

Estimation is by **WLS**, weighting by cell size. The identification problem — age = year − birth
year creates perfect collinearity — is resolved via the **Deaton (1997)** normalization: period
dummies are replaced by T−2 orthogonalized dummies that absorb no linear trend, so all long-run
trends are attributed to age and cohort effects, while τ_t captures only cyclical deviations.
Coefficients satisfy Σ τ_t = 0 and Σ t·τ_t = 0.

Age and cohort profiles are plotted in probability scale via the inverse logistic transformation.
The **age profile** uses birth cohort 1956 as reference; the **cohort profile** uses age 42 as
reference. The period effect is shown in log-odds directly.

---

## Descriptive Trends (2005–2025)

![Labor participation and unemployment rates by education and gender](/images/apc_figura1.png)
*Figure 1. Time series of labor force participation and unemployment rates by education level and
gender, 2005–2025. Male participation is high and stable across all education groups. Female
participation shows a rising secular trend with a persistent education gap. The 2008–09 financial
crisis and the 2020 COVID-19 shock are visible as structural breaks in both series.*

![Employment shares by sector](/images/apc_figura2.png)
*Figure 2. Employment shares in formal wage, informal wage, and self-employment by education and
gender, 2005–2025. Formal employment shows a declining trend, especially among workers with basic
education. Informal wage employment has grown steadily and is concentrated in the lowest-education
group. Self-employment is relatively stable over time.*

![Raw life-cycle profiles — participation and unemployment](/images/apc_figura3.png)
*Figure 3. Raw life-cycle profiles for labor force participation and unemployment by age. Each line
represents a birth cohort. Male participation follows a classic inverted-U with little cohort
displacement. Female cohorts are widely spaced vertically — younger generations participate more
at every age. Unemployment is highest among the young and falls sharply toward age 30.*

![Raw life-cycle profiles — sectoral shares](/images/apc_figura4.png)
*Figure 4. Raw life-cycle profiles for sectoral employment shares by age. Formal employment peaks
early and declines with age. Informal wage employment is more common among the young. Self-employment
rises monotonically with age across all cohorts.*

---

## APC Decomposition — Labor Force Participation

![Age effect on labor force participation](/images/apc_fig_part_alpha.png)
*Age effect (α) — reference cohort: 1956. Male participation follows a classic inverted-U profile.
Female participation peaks around 40–45 and is substantially higher for workers with higher
education throughout the life cycle.*

![Cohort effect on labor force participation](/images/apc_fig_part_kappa.png)
*Cohort effect (κ) — reference age: 42. Younger female cohorts participate consistently more than
their predecessors at every age, reflecting the secular increase in women's labor market attachment.
Male cohort effects show no clear direction.*

![Period effect on labor force participation](/images/apc_fig_part_tau.png)
*Period effect (τ). The cyclical component shows clear contractions during the 2008–09 global
financial crisis and the 2020 COVID-19 shock. Recovery was faster for men than for women,
particularly in the intermediate and higher education groups.*

---

## APC Decomposition — Unemployment

![Age effect on unemployment](/images/apc_fig_desocu_alpha.png)
*Age effect (α) — reference cohort: 1956. Unemployment is markedly higher in youth and falls
sharply toward age 30, consistent with school-to-work transitions and experience accumulation.*

![Cohort effect on unemployment](/images/apc_fig_desocu_kappa.png)
*Cohort effect (κ) — reference age: 42. Younger cohorts face lower structural unemployment across
all education groups. The generational decline is most pronounced in the basic-education group:
among men, the unemployment rate at age 42 falls from ~8% in cohorts born in 1935–45 to ~1% in
the most recent ones.*

![Period effect on unemployment](/images/apc_fig_desocu_tau.png)
*Period effect (τ). Unemployment is strongly countercyclical. The 2008–09 and 2020 shocks are the
most visible episodes, with similar magnitudes across gender groups.*

---

## APC Decomposition — Formal Wage Employment

![Age effect on formal employment](/images/apc_fig_formal_alpha.png)
*Age effect (α) — reference cohort: 1956. Formal employment probability is high and stable from
age 20 to 55, then drops sharply as workers transition to self-employment or inactivity. The
education gap is wide: men in the 1956 cohort show rates of ~60% (higher education) vs. ~20%
(basic education) across the entire life cycle.*

![Cohort effect on formal employment](/images/apc_fig_formal_kappa.png)
*Cohort effect (κ) — reference age: 42. Higher-education cohorts show consistently greater
formality across all generations. No clear generational trend is apparent for basic and
intermediate education groups.*

![Period effect on formal employment](/images/apc_fig_formal_tau.png)
*Period effect (τ). Period effects are moderate for intermediate and higher education groups,
fluctuating near zero throughout. The basic-education group shows considerably greater variability,
with a notable drop during 2008–10 (down to −0.15 log-odds for men) and a sharp spike for women
around 2020.*

---

## APC Decomposition — Informal Wage Employment

![Age effect on informal employment](/images/apc_fig_informal_alpha.png)
*Age effect (α) — reference cohort: 1956. Informal wage employment is more common among the young
and declines with age, partly reflecting transitions toward self-employment or formality as
experience accumulates.*

![Cohort effect on informal employment](/images/apc_fig_informal_kappa.png)
*Cohort effect (κ) — reference age: 42. Basic-education cohorts show the highest informality in
every generation. No significant generational improvement is observed, suggesting that structural
barriers to formality persist regardless of cohort.*

![Period effect on informal employment](/images/apc_fig_informal_tau.png)
*Period effect (τ). The cyclical component shows a spike in informality during 2008–09, consistent
with the informal sector acting as a buffer when formal employment contracts. In 2020, the pattern
is neutral or negative — many informal workers exited the labor force entirely rather than
switching to formal employment.*

---

## APC Decomposition — Self-Employment

![Age effect on self-employment](/images/apc_fig_autoempleo_alpha.png)
*Age effect (α) — reference cohort: 1956. Self-employment rises monotonically with age, especially
for men. This reflects the accumulation of sector-specific capital, business networks, and assets,
as well as progressive exit from salaried employment at older ages.*

![Cohort effect on self-employment](/images/apc_fig_autoempleo_kappa.png)
*Cohort effect (κ) — reference age: 42. Higher-education cohorts show consistently lower
self-employment in every generation. The basic-education group shows a clear generational decline:
men fall from ~48% in cohorts born in 1935 to ~30–35% in the most recent ones; a similar, albeit
slightly lower, pattern holds for women.*

![Period effect on self-employment](/images/apc_fig_autoempleo_tau.png)
*Period effect (τ). The cyclical component of self-employment is more volatile than that of other
outcomes, consistent with displaced workers entering self-employment during periods of economic
contraction.*

---

## APC Decomposition — Overemployment *(extension)*

> **Note:** Overemployment is not analyzed in Duval-Hernández & Orraca Romano (2009). This is an
> original extension. The variable measures the share of salaried workers who work more than
> 40 hours per week.

![Age effect on overemployment](/images/apc_fig_sobreocupado_alpha.png)
*Age effect (α) — reference cohort: 1956. Overemployment rates are highest among the young and
decline with age in all groups. The education gradient is inverted relative to formal employment:
basic-education workers show the highest rates, higher-education workers the lowest. Women's rates
are notably lower than men's across all education groups.*

![Cohort effect on overemployment](/images/apc_fig_sobreocupado_kappa.png)
*Cohort effect (κ) — reference age: 42. Among men, rates are relatively stable across cohorts.
Among women, a marked upward shift is observed in younger cohorts: generations born after 1965
show clearly higher overemployment rates than their predecessors, though still below male levels.*

![Period effect on overemployment](/images/apc_fig_sobreocupado_tau.png)
*Period effect (τ). The cyclical component of overemployment shows the greatest variability of all
estimated outcomes. No clear cyclical pattern associated with the 2008–09 or 2020 crises is
discernible; the series fluctuates around zero without a sustained direction in any group.*

---

## Key Findings

- **Participation:** Strong secular upward cohort trend for women; men show no generational shift. COVID-19 shock visible as the sharpest cyclical contraction in the sample.
- **Unemployment:** Younger cohorts face lower structural unemployment across all groups. Period effects confirm strong countercyclicality (2008–09 and 2020).
- **Formal employment:** Peaks in mid-career (20–55), then drops sharply. Education is the dominant predictor; no significant generational improvement for basic/intermediate groups.
- **Informal employment:** Functions as a cyclical buffer in recessions (2008–09) but not during COVID-19, when many informal workers exited the labor force entirely.
- **Self-employment:** Rises monotonically with age; lower education correlates with higher self-employment at every age and cohort. A generational decline in self-employment is visible for basic-education workers.
- **Overemployment *(extension)*:** Highest among young, low-education workers. Younger female cohorts show a generational increase in overemployment, a pattern absent in men.

---

**Data:** ENOE, INEGI (2005Q1–2025Q4) | **Method:** APC decomposition, Deaton (1997) | **Tool:** R
