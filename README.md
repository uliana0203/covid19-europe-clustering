# Temporal Evolution of Pandemic Clusters Across Europe (2020–2025)

Reproducible code and data for the study of the temporal evolution and stability
of country-level COVID-19 surveillance profiles across 45 European countries
between 2020 and 2025.

Monthly reported cases and deaths are normalised per 100,000 inhabitants,
standardised within each year, reduced with principal component analysis (PCA),
and clustered with five algorithms (Ward hierarchical clustering, k-means,
Gaussian mixture models, spectral clustering, OPTICS). Solutions are evaluated
with internal validation indices (Silhouette, Davies–Bouldin, Calinski–Harabasz)
and with year-to-year partition stability (Adjusted Rand Index, Normalized Mutual
Information).

## Publication status

The associated article has been **submitted for publication**. This repository
is provided so that the analysis can be inspected and reproduced; the citation
will be added once the article is published.

**Authors:** Uliana Zbezhkhovska, Dmytro Chumachenko

## Repository structure

```
covid19_europe_clustering/
├── clustering_covid_europe.ipynb   # single notebook: preprocessing + all figures/tables
├── requirements.txt
├── LICENSE                         # MIT (code only)
├── README.md
├── .gitignore
├── data/
│   ├── WHO-COVID-19-global-daily-data.csv          # WHO COVID-19 dashboard snapshot
│   ├── API_SP.POP.TOTL_DS2_en_csv_v2_40826.csv     # World Bank population (SP.POP.TOTL) snapshot
│   └── DATA_SOURCES.md                             # provenance, snapshot dates, attribution
└── figures/
    └── Figure_1.png … Figure_9.png                 # regenerated when the notebook runs
```

## Data sources

| Dataset | Source | Notes |
|---------|--------|-------|
| Daily reported COVID-19 cases and deaths by country | World Health Organization COVID-19 dashboard | Snapshot downloaded 20 February 2026 (reports through 18 January 2026); monthly aggregation January 2020 – December 2025 |
| Annual total population by country | World Bank Open Data, indicator `SP.POP.TOTL` | Snapshot downloaded 20 February 2026 (World Bank release 28 January 2026); values for 2020–2024 used directly, 2025 obtained by per-country linear-trend extrapolation from 2020–2024 |

The WHO and World Bank portals are updated continuously (revisions, back-filled
reports, re-based population estimates), so re-downloading later would change the
inputs and therefore the figures. The two files in `data/` are the **exact,
unmodified snapshots used for the article** and are committed deliberately so the
results stay reproducible. Both providers release these data under the
**Creative Commons Attribution 4.0 International licence (CC BY 4.0)**, which
permits this redistribution with attribution; see
[`data/DATA_SOURCES.md`](data/DATA_SOURCES.md) for source URLs, indicator codes,
snapshot dates and attribution. The data files remain the copyright of WHO and
the World Bank and are not covered by the code licence (see below).

## How to run

```bash
python -m venv .venv
# Windows:  .venv\Scripts\activate
# Linux/macOS:  source .venv/bin/activate
pip install -r requirements.txt

jupyter lab clustering_covid_europe.ipynb
```

Run the notebook top to bottom (Python 3.11). It rebuilds every figure into
`figures/` and prints both result tables. All random seeds are fixed to 42, so
the numbers match those reported in the article.

Expected run time: a few minutes on a typical laptop (the silhouette-surface and
optimal-`k` searches dominate).

## What the notebook produces

| Notebook output | Article item |
|-----------------|--------------|
| `Figure_1.png` | Fig. 1 — Annual heatmaps of infection and mortality rates per 100,000 |
| `Figure_2.png` | Fig. 2 — Correlation between incidence and mortality rates over time |
| `Figure_3.png` | Fig. 3 — Temporal trajectories for selected countries |
| `results_df` table | Table 1 — Performance comparison of clustering algorithms, 2020–2025 |
| `best_configs` table | Table 2 — Best-performing configuration by year and metric |
| `Figure_4_Ward_vs_KMeans_optimal_k_annotated.png` | Fig. 4 — PCA projections under silhouette-optimised `k` |
| `Figure_5_KMeans_Ward_Outliers.png` | Fig. 5 — Ward and k-means clustering with identified outliers |
| `Figure_6_KMeans_Ward_Outlier_Overlap.png` | Fig. 6 — Overlap of outlier countries between algorithms |
| `Figure_7_Clustering_Stability.png` | Fig. 7 — Temporal stability of cluster assignments (ARI, NMI) |
| `Figure_8_Silhouette_Analysis_Ward_KMeans.png` | Fig. 8 — Silhouette analysis for Ward and k-means |
| `Figure_9.png` | Fig. 9 — Temporal evolution of country cluster memberships |

## Reproducibility notes

- **Study panel (45 countries).** The 20 February 2026 WHO snapshot labels the
  Netherlands as *"Netherlands (Kingdom of the)"*, so it is not matched by the
  country list used here; combined with the requirement of complete monthly
  records for all 72 months, this yields the balanced 45-country panel described
  in the article.
- **2025 population** is extrapolated (linear trend, 2020–2024) because World Bank
  estimates for 2025 were not yet available at the time of analysis; 2025
  per-capita rates are therefore approximate.
- **OPTICS** returns a variable number of clusters and labels noise as `-1`; its
  internal indices are reported as descriptive diagnostics and are not directly
  comparable with the fixed-`k = 6` methods.
- Clustering and all validation metrics are computed in year-specific PCA score
  spaces (components explaining ≥ 90 % of variance); the PC1–PC2 projection is
  used for visualisation only.

## License

- **Code** (the notebook and any supporting scripts): MIT License — see
  [`LICENSE`](LICENSE).
- **Data** (`data/*.csv`): © World Health Organization and © The World Bank,
  reused under CC BY 4.0. These files are not relicensed here; the MIT License
  does not apply to them. Attribution and terms are in
  [`data/DATA_SOURCES.md`](data/DATA_SOURCES.md).
- **Figures** in `figures/` are generated by the code from the data and are
  released under the same MIT License as the code.

## Acknowledgements

This research was funded by the National Research Foundation of Ukraine under
research project No. 2025.07/0270, "A Multidisciplinary Methodology for Modelling
the Syndemic of War: Infectious Diseases, Information Manipulation, and Challenges
of Incomplete Medical Data During Conflicts."
