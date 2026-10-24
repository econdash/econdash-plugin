# Other citation formats

The same fields as the APA format in the skill, in the layouts used by "Cite this" on econdash.org.

## MLA

```
{publisher}. "{name} — {country_name}." EconDash, {year}, {chart_url}. Accessed {D Mon. YYYY}. Original source: {source_url}.
```

Months are abbreviated: Jan., Feb., Mar., Apr., May, June, July, Aug., Sept., Oct., Nov., Dec.

## Chicago

```
{publisher}. {year}. "{name} — {country_name}." EconDash. Accessed {Month D, YYYY}. {chart_url}. Original source: {source_url}.
```

## BibTeX

Placeholders are in angle brackets here, because the braces belong to BibTeX.

```
@misc{econdash_<slug>_<iso3>,
  author = {{<publisher>}},
  title = {{<name> --- <country_name>}},
  howpublished = {EconDash},
  year = {<year>},
  url = {<chart_url>},
  note = {Accessed: <YYYY-MM-DD>. Original source: <source_url>}
}
```

The key uses the slug and the ISO3 code in lowercase, with every character other than a letter or digit replaced by `_`. In `author`, `title` and the original source URL, escape `&`, `%`, `_`, `#` and `$` with a backslash.
