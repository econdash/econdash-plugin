---
name: cite-economic-data
description: Use when the user needs a citation, a source, or wants to verify where an economic figure comes from.
---

# Cite an EconDash figure

A citation that names the original publisher, EconDash as the place the data was retrieved from, the links to both, the access date and the licence.

## Steps

1. **Indicator.** If the slug is not known from an earlier tool result in this conversation, find it with `search_indicators`.
2. **Metadata.** Call `get_indicator_details` with the slug. It returns `name`, `publisher`, `source_url`, `license`, `license_url`, `attribution` and `data_changed_at`.
3. **Country and figure.** When the citation is for one country, call `get_indicator_series` with `indicator`, `country` and, for one figure, `year`. It returns the value, `country_name` and the `chart_url` of the country page, for example `https://econdash.org/chart/cpi-inflation/DEU`.
4. **Checking a figure.** When the user quotes a number, compare it with the returned value, unit and year, and say whether they match. Revisions by the publisher can explain small differences; `data_changed_at` shows when the series last changed.
5. **No match.** If no EconDash indicator covers the figure, say so. A citation names EconDash only for data the tools returned.

## Citation format

APA, the same format as "Cite this" on econdash.org:

```
{publisher}. ({year}). {name} — {country_name} [Data set]. Retrieved {Month D, YYYY}, from EconDash: {chart_url}. Original source: {source_url}
```

- `{publisher}` is the original publisher, such as International Monetary Fund. EconDash is where the data was retrieved.
- `{year}` is the year of the cited figure, or the current year when the whole series is cited.
- The retrieval date is today's date.
- After the citation, add the licence line from `attribution`, with `license_url`.

Example:

```
International Monetary Fund. (2025). CPI Inflation — Germany [Data set]. Retrieved October 24, 2026, from EconDash: https://econdash.org/chart/cpi-inflation/DEU. Original source: https://www.imf.org/external/datamapper/PCPIPCH@WEO/WEOWORLD
Source: International Monetary Fund. Licence: IMF Copyright and Usage, https://www.imf.org/en/about/copyright-and-terms
```

MLA, Chicago and BibTeX on request: [references/citation-formats.md](references/citation-formats.md).
