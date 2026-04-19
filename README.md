# The Spatial Expansion of Chinese Higher Education

An interactive data visualization of 849 Chinese universities retrieved from Wikidata, tracing how the country's university system grew from 1879 to today.

**Course:** Information Visualization, University of Bologna (2025)
**Author:** Zizhe

## Research Questions

1. **When did China build its universities?** — Historical expansion across 150 years
2. **Which provinces dominate, and which are left behind?** — Regional imbalance
3. **When did the imbalance start?** — Provincial founding patterns over time
4. **Did China's educational center of gravity shift?** — Geographic drift across decades

## Data Sources

- **Primary:** [Wikidata](https://www.wikidata.org) — universities (`Q3918`) located in China (`Q148`), retrieved via SPARQL. License: **CC0**.
- **Secondary:** Manually compiled province → macro-region classification table, based on the National Bureau of Statistics of China. License: **CC0**.

The dataset of 849 unique universities is smaller than official Ministry of Education counts (~1300 HEIs) because Wikidata skews toward well-known institutions and the query excludes vocational colleges. See the notebook and website for a full discussion of limitations.

## Repository Structure

```
.
├── index.html                  # The visualization website (GitHub Pages entry point)
├── data_cleaning.ipynb         # Full pipeline: SPARQL → clean → EDA → export
├── README.md
├── LICENSE
├── data/
│   ├── universities_raw.csv         # SPARQL output (cached)
│   ├── universities_clean.csv       # Main cleaned dataset
│   ├── region_classification.csv    # Secondary data source
│   ├── province_summary.csv         # Aggregates for RQ2
│   ├── region_summary.csv           # Aggregates for RQ2
│   ├── decade_province.csv          # Aggregates for RQ3
│   └── mean_center.csv              # Aggregates for RQ4
└── assets/
    └── eda_overview.png             # EDA summary chart
```

## How to Run

**View the website:** open `index.html` in a browser, or visit the live site above.

**Reproduce the data pipeline:**
```bash
pip install pandas numpy matplotlib SPARQLWrapper requests jupyter
jupyter notebook data_cleaning.ipynb
```
The notebook will auto-install any missing dependencies and cache SPARQL results locally. To force a fresh fetch from Wikidata, delete `data/universities_raw.csv`.

## Credits

- **Data:** Wikidata contributors (CC0)
- **Visualization libraries:** [Plotly.js](https://plotly.com/javascript/) (MIT), [Leaflet.js](https://leafletjs.com/) (BSD-2-Clause)
- **Map tiles:** [CARTO](https://carto.com/) Light basemap (CC BY 3.0), [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors (ODbL)
- **Fonts:** [Lora](https://fonts.google.com/specimen/Lora) and [Space Mono](https://fonts.google.com/specimen/Space+Mono) via Google Fonts (SIL Open Font License)

## License

This project (code, notebook, and written content) is released under the MIT License — see [`LICENSE`](LICENSE). Underlying Wikidata is CC0.

## Contact

Zizhe · University of Bologna · Information Visualization 2025
