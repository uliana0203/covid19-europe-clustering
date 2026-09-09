# Data sources

The two files in this folder are the exact, unmodified snapshots of publicly
available open datasets that were used to produce the figures and tables in the
article. The WHO and World Bank portals are refreshed continuously (report
revisions, back-filled data, re-based population estimates), so a later download
would not reproduce the same results. The snapshots are therefore committed
here on purpose. Both datasets are distributed by their providers under the
**Creative Commons Attribution 4.0 International licence (CC BY 4.0)**, which
permits this redistribution with attribution.

---

## `WHO-COVID-19-global-daily-data.csv`

- **Provider:** World Health Organization (WHO)
- **Dataset:** WHO COVID-19 dashboard — reported COVID-19 cases and deaths
  (daily, by country)
- **Portal:** https://data.who.int/dashboards/covid19/data
- **Download page:** https://data.who.int/dashboards/covid19/data ("Download the
  full data set")
- **Snapshot:** downloaded 2026-02-20; the file contains reports through
  2026-01-18. Only records up to 2025-12-31 are used in the analysis.
- **Licence:** CC BY 4.0 with additional WHO terms of use
  (https://data.who.int/about/data/terms-and-conditions)
- **Suggested attribution:** "COVID-19 cases and deaths data. Geneva: World
  Health Organization. Available from https://data.who.int/dashboards/covid19
  (accessed 20 February 2026), licensed under CC BY 4.0."
- **Note:** WHO does not endorse this analysis or any results derived from the
  data.

## `API_SP.POP.TOTL_DS2_en_csv_v2_40826.csv`

- **Provider:** The World Bank
- **Dataset:** World Development Indicators — "Population, total"
- **Indicator code:** `SP.POP.TOTL`
- **Portal:** https://data.worldbank.org/indicator/SP.POP.TOTL
- **Snapshot:** downloaded 2026-02-20; World Bank "Last Updated Date" 2026-01-28
  (annual values through 2024). The 2025 value is not provided by the World Bank
  and is obtained in the notebook by per-country linear-trend extrapolation from
  2020–2024.
- **Licence:** CC BY 4.0 (World Bank Open Data,
  https://datacatalog.worldbank.org/public-licenses)
- **Suggested attribution:** "Population, total (SP.POP.TOTL). World Development
  Indicators, The World Bank. https://data.worldbank.org/indicator/SP.POP.TOTL
  (accessed 20 February 2026), licensed under CC BY 4.0."

---

Newer data can be obtained from the portals above, but replacing these files
will change the outputs and they will no longer match the article.
