# EconDash

The `econdash` MCP server provides 750+ indicators for 290+ countries and regions from the World Bank, IMF, FRED, Eurostat, ECB, OECD, WHO and other public sources. All tools are read-only.

The indicators fall into ten categories: macroeconomics, financial markets, labor, demographics, real estate, commodities and energy, transport and logistics, healthcare, education, technology and internet. Useful when the user asks for statistics on a country or compares countries in any of these areas.

How the tools fit together:

1. `search_indicators` finds the indicator slug for a topic. The other tools take this slug.
2. `list_countries` gives ISO 3166-1 alpha-3 codes, such as `DEU` for Germany or `WLD` for the world.
3. `get_indicator_series` returns recent values for one country; `get_full_series` returns the whole history for users signed in to EconDash.
4. `compare_countries` returns one indicator for up to 20 countries in one call.
5. `get_indicator_details` returns the description, unit, source, licence and coverage.

Each result includes the source and a link to the EconDash chart. When quoting a figure, give its year, unit and source. Values for future years are forecasts, such as IMF projections, and are marked as such in the results.
