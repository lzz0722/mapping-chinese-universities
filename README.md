# The Spatial Expansion of Chinese Higher Education

An interactive data visualization of 849 Chinese universities retrieved from Wikidata, tracing how the country's university system grew from 1879 to today — and how the resulting distribution looks very different depending on whether you count institutions or institutions per capita.

**Course:** Information Visualization, University of Bologna (2025)
**Author:** Zizhe
**Live site:** https://<your-github-username>.github.io/<your-repo-name>/

## Research Questions

1. **When did China build its universities?** — Historical expansion across 150 years
2. **Counting universities — or counting per capita?** — Regional imbalance from two angles
3. **When did the imbalance start?** — Provincial founding patterns over time
4. **Did China's educational center of gravity shift?** — Geographic drift across decades

## Data Sources

Three data sources are integrated in the pipeline:

- **Primary — Wikidata (CC0):** universities (`Q3918`) located in China (`Q148`), retrieved via SPARQL from the public endpoint at [query.wikidata.org/sparql](https://query.wikidata.org/sparql). Fields retrieved: English + Chinese labels, inception year (`P571`), coordinates (`P625`), and administrative location (`P131` traversed twice to reach the province level).
- **Secondary — Wikidata (CC0):** province-level population figures (`P1082`) with point-in-time qualifiers (`P585`), retrieved via a second SPARQL query. Coverage of all 34 province-level units is achieved by combining China's `P150` (*contains administrative territorial entity*) statement with an explicit `VALUES` clause for direct-administered municipalities and Special Administrative Regions. For each province the most recent population figure (2020 census for the mainland; 2021 for Hong Kong) is used to compute per-capita density in RQ2.
- **Tertiary — Manually compiled (CC0):** province → macro-region classification table, based on the National Bureau of Statistics of China's standard 7-region grouping.

The dataset of 849 unique universities is smaller than official Ministry of Education counts (~2,820 HEIs) because Wikidata skews toward well-known institutions and the query excludes vocational colleges. See the notebook and website for a full discussion of limitations.

## Scope

This project focuses on **mainland China and Hong Kong**. Two regions are excluded from the analysis:

- **Taiwan** — out of scope because its higher education system followed a historical trajectory independent from the mainland after 1949, and including it would distort the narrative around events like the 1952 departmental restructuring and the 1977 reinstatement of the Gaokao.
- **Macau** — excluded because Wikidata returns no universities for Macau within our query, so any per-capita figure would be undefined or misleading.

## Repository Structure

```
.
├── index.html                         # The visualization website (GitHub Pages entry point)
├── data_cleaning.ipynb                # Full pipeline: SPARQL → clean → integrate → EDA → export
├── README.md
├── LICENSE
├── data/
│   ├── universities_raw.csv           # SPARQL output for universities (cached)
│   ├── universities_clean.csv         # Main cleaned dataset
│   ├── province_population_raw.csv    # SPARQL output for populations (cached)
│   ├── province_population.csv        # Cleaned: one row per province, latest year
│   ├── region_classification.csv      # Manually compiled province → macro-region map
│   ├── province_summary.csv           # Merged aggregates for RQ2 (count + population + density)
│   ├── region_summary.csv             # Aggregates for RQ2
│   ├── decade_province.csv            # Aggregates for RQ3
│   └── mean_center.csv                # Aggregates for RQ4
└── assets/
    └── eda_overview.png               # EDA summary chart
```

## Website Interactions

- **RQ1** — hover any bar for the exact university count and decade.
- **RQ2** — toggle the ranked bar chart between **absolute count** and **universities per million inhabitants**; the ranking re-orders with an animated transition, revealing how per-capita normalisation reshuffles the provincial hierarchy. The bubble map on the left always shows absolute counts for spatial reference.
- **RQ3** — hover the heatmap for per-region, per-decade percentages.
- **RQ4** — pan and zoom the Leaflet map; click any waypoint on the mean-centre trajectory for the decade and university count.

## How to Run

**View the website:** open `index.html` in a browser, or visit the live site above.

**Reproduce the data pipeline:**
```bash
pip install pandas numpy matplotlib SPARQLWrapper requests jupyter
jupyter notebook data_cleaning.ipynb
```
The notebook will auto-install any missing dependencies and cache both SPARQL results locally. To force a fresh fetch from Wikidata, delete the corresponding raw file(s) in `data/`: `universities_raw.csv` and/or `province_population_raw.csv`.

## Credits

- **Data:** Wikidata contributors (CC0)
- **Visualization libraries:** [Plotly.js](https://plotly.com/javascript/) (MIT), [Leaflet.js](https://leafletjs.com/) (BSD-2-Clause)
- **Map tiles:** [CARTO](https://carto.com/) Light basemap (CC BY 3.0), [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors (ODbL)
- **Fonts:** [Lora](https://fonts.google.com/specimen/Lora) and [Space Mono](https://fonts.google.com/specimen/Space+Mono) via Google Fonts (SIL Open Font License)

## License

This project (code, notebook, and written content) is released under the MIT License — see [`LICENSE`](LICENSE). Underlying Wikidata is CC0.

## Contact

Zizhe · University of Bologna · Information Visualization 2025
