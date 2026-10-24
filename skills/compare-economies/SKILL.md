---
name: compare-economies
description: Use when the user wants to compare countries on an economic or social indicator, or rank countries, for example which country in a group has the highest debt, inflation or unemployment.
---

# Compare countries on one indicator

A table of two or more countries on the same indicator from EconDash, with the period, unit and source of every value.

## Steps

1. **Indicator.** Call `search_indicators` with the topic in short English keywords, for example "life expectancy" or "debt to gdp". Pick the result that fits the question:
   - a ratio (% of GDP, per capita, per 1,000 people) compares countries of different size; an absolute amount (current USD, persons) compares size;
   - the `countries` count in the result: a series that covers one country, such as many FRED, BLS and Eurostat series, cannot be compared across countries;
   - a vague topic, such as "debt" (government, household or external), needs a choice: ask the user, or pick one and name it in the answer.
2. **Country codes.** The tools take ISO 3166-1 alpha-3 codes. For a group such as "G7" or "the Nordics", list the member codes and say in the answer which countries were included. `list_countries` lists all codes, including aggregates such as `EUU` (European Union) and `WLD` (world).
3. **One point in time.** Call `compare_countries` with `indicator`, `countries` (up to 20 per call) and `year`. Without `year`, it returns the latest observed value of each country.
4. **Change over time.** For a trend, call `get_indicator_series` for each country with `start_year` and `end_year`, or call `compare_countries` once per year for two or three years.

## The answer

- A table: country, value, period, unit. Sort it when the user asks for a ranking.
- A ranking covers only the countries in the table. Say so when the user asks about "the world" and only some countries were compared.
- State the caveats the tool returns:
  - each value has its own `period`; without `year`, latest years can differ between countries;
  - codes in `no_data` have no value for this indicator; list them rather than filling them in;
  - values labelled as projections are forecasts, not observations.
- Source and licence as the tool returns them, and the `chart_url` of each country for the full history on econdash.org.
- Format the answer as a table with a short summary.
