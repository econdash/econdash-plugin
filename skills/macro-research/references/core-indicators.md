# Core indicators for a country snapshot

Slugs checked against the EconDash catalogue. Coverage is the number of countries and regions with data.

| Topic | Slug | Unit | Source, coverage | Alternative |
| --- | --- | --- | --- | --- |
| Real GDP growth | `gdp-growth-annual-percent` | % | World Bank, 1961 onward, 258 | `real-gdp-growth` (IMF, with projections, 52) |
| GDP per capita | `gdp-per-capita` | current USD | World Bank, 1960 onward, 258 | `gdp-per-capita-imf` (IMF, with projections, 52) |
| Inflation | `cpi-inflation-rate-percent` | % | World Bank, 1960 onward, 237 | `cpi-inflation` (IMF, with projections, 52) |
| Unemployment | `unemployment-ilo-estimates` | % of labour force | ILO, 1991 onward, 186 | `unemployment-rate` (IMF, with projections, 50) |
| Government debt | `government-debt-percent-gdp` | % of GDP | World Bank, 1970 onward, 120 | `gross-government-debt` (IMF, with projections, 52) |
| Current account | `current-account-balance-2` | % of GDP | IMF, 1980 onward, 52 | `current-account-balance` (World Bank, current USD, 201) |
| Trade openness | `trade-volume-percent-gdp` | exports plus imports, % of GDP | World Bank, 1960 onward, 253 | |
| Population | `total-population` | persons | World Bank, 1960 onward, 261 | |

The World Bank series cover more countries. The IMF series cover fewer countries but include projections, and for the largest economies they often have a more recent year.

Two definitions differ between the main and the alternative slug, so name the source next to the figure:

- Government debt: the World Bank series is central government debt; the IMF series is general government gross debt and is usually higher.
- Unemployment: the ILO series is a modelled estimate for comparison between countries; the IMF series follows national definitions.
