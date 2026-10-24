---
name: macro-research
description: Use when the user asks for an overview of a country's economy, recent economic performance, or a macro snapshot (growth, inflation, unemployment, debt, trade).
---

# Country macro snapshot

A short overview of one country's economy built from the EconDash tools: growth, income, inflation, jobs, public debt and the external balance, each figure with its year and source.

## Steps

1. **Country code.** The tools take ISO 3166-1 alpha-3 codes: `DEU` Germany, `JPN` Japan, `BRA` Brazil, `EUU` European Union, `WLD` world. If the code is unclear, call `list_countries`. If the user names no country, ask which one.
2. **Indicators.** Use these slugs; coverage and definitions are in [references/core-indicators.md](references/core-indicators.md).

   | Topic | Slug | Alternative |
   | --- | --- | --- |
   | Real GDP growth | `gdp-growth-annual-percent` | `real-gdp-growth` (IMF, with projections) |
   | GDP per capita, current USD | `gdp-per-capita` | `gdp-per-capita-imf` |
   | Inflation | `cpi-inflation-rate-percent` | `cpi-inflation` |
   | Unemployment | `unemployment-ilo-estimates` | `unemployment-rate` |
   | Government debt, % of GDP | `government-debt-percent-gdp` | `gross-government-debt` |
   | Current account, % of GDP | `current-account-balance-2` | `current-account-balance` (current USD, World Bank) |
   | Trade, % of GDP | `trade-volume-percent-gdp` | |

   For a topic that is not in the table, find the slug with `search_indicators` using short English keywords, for example "youth unemployment" or "fdi". A guessed slug returns an error.
3. **Values.** For each indicator call `get_indicator_series` with `indicator`, `country` and `start_year` set ten years back. The calls do not depend on each other.
4. **Gaps.** If a series has no data for the country, try the alternative slug from the table. IMF alternatives cover about 50 economies and include projections. If that has none either, report the figure as not available rather than estimating it.

## The answer

- One line per indicator: the latest observed value with its year and unit, and the direction over the decade, for example "inflation 5.0% in 2025, down from 9.3% in 2022".
- Latest years differ between indicators, so state the year of each figure.
- `next_projection` and values labelled as projections are forecasts, such as IMF World Economic Outlook projections. Present them as "IMF projection for 2026", apart from observed values.
- A short paragraph on the overall picture, based only on the returned numbers.
- Sources: name the source of each figure as the tool returns it (World Bank, IMF, ILO) and give the `chart_url` links, where the user can see the full history on econdash.org.
- Format the answer as plain text or a table.
