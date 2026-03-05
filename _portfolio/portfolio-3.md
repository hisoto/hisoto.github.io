---
title: "Automated Price Behavior Monitoring in Mexico"
excerpt: "Monthly automated pipeline that scrapes INPC and INPP series from INEGI, processes them in R, and renders a reproducible Quarto report on Mexican inflation dynamics.<br/><img src='/images/inpc_annual_2026m01.png'>"
collection: portfolio
---

This project is a monthly automated reporting system for tracking price behavior across Mexico. It is developed as part of the institutional work at CONASAMI (Comisión Nacional de los Salarios Mínimos) to monitor cost-of-living pressures relevant to minimum wage policy.

## Data Pipeline

Data are collected directly from INEGI's price index portal using a two-step web scraping process: first, ASP.NET session tokens (`__VIEWSTATE`, `__EVENTVALIDATION`) are retrieved via a GET request to the series structure page; then a POST request to the export endpoint returns the data as an HTML table, which is parsed with `rvest`. The pipeline downloads approximately 79 series in total, covering INPC components, biweekly indices, five basic food products, INPC for 46 cities, and the National Producer Price Index (INPP), storing all data in a single flat CSV file.

The processed data feed into a set of `ggplot2` visualizations and a Quarto report that is re-rendered each month with updated figures.

## Key Findings — January 2026

### General Inflation

Mexico's consumer price index (INPC) registered an **annual variation of 3.79%** in January 2026, with a monthly increase of 0.38%.

### Core vs. Non-Core Inflation

A notable divergence between core and non-core components characterizes the current inflationary environment:

| Component | Annual change | Monthly change |
|-----------|:-------------:|:--------------:|
| **Core (Subyacente)** | 4.52% | 0.60% |
| — Goods | 4.56% | 0.64% |
| — Services | 4.48% | 0.56% |
| **Non-core (No subyacente)** | 1.39% | −0.36% |
| — Agricultural | 1.52% | −0.27% |
| — Energy & regulated tariffs | 1.28% | −0.46% |

Core inflation is running at more than three times the rate of non-core, driven by persistently elevated prices in both goods and services.

### Minimum Consumption Basket

The minimum consumption basket (Canasta de Consumo Mínimo, CCM) rose **3.60% annually** and 0.38% monthly — slightly below headline INPC, suggesting that the goods most relevant to lower-income households faced marginally lower price pressures than the general basket.

### Basic Food Products

Strong divergence is observed among five staple products monitored by CONASAMI:

| Product | Annual change | Monthly change |
|---------|:-------------:|:--------------:|
| Beef (*carne de res*) | +16.45% | +0.53% |
| Milk (*leche*) | +10.08% | +0.87% |
| Tortilla | +1.80% | +0.29% |
| Beans (*frijol*) | −9.89% | −1.49% |
| Eggs (*huevo*) | −8.17% | −6.31% |

Beef and milk remain significantly above headline inflation, while beans and eggs are deflating sharply following supply-driven price corrections.

### Geographic Variation (46 Cities)

Annual inflation across the 46 cities tracked by INEGI ranged from **2.13% (Tijuana, B.C.) to 5.60% (Chetumal, Q.R.)**. The Northern Border Free Zone (ZLFN) cities averaged 3.07% — below the national figure — reflecting the effects of trade proximity and price arbitrage. Interior states, particularly in southern and central Mexico, showed the highest inflation rates.

### Producer Prices (INPP)

The National Producer Price Index (excluding oil) increased **2.12% annually** and 0.14% monthly, with divergence across sectors:

| Sector | Annual change | Monthly change |
|--------|:-------------:|:--------------:|
| Tertiary (services) | +4.02% | −0.64% |
| Secondary (manufacturing, excl. oil) | +1.61% | +0.74% |
| Primary (agriculture, mining) | −5.90% | −2.41% |

The contraction in primary sector producer prices is consistent with the deflation observed in agricultural consumer goods (beans, eggs).

## Tools

R (`httr2`, `rvest`, `xml2`, `data.table`, `ggplot2`, `tidyverse`), Quarto, INEGI open data portal.
