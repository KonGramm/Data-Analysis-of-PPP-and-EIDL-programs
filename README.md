# PPP & EIDL COVID-19 Loan Analysis

Analysis of two major U.S. federal COVID-19 relief programs — the **Paycheck Protection Program (PPP)** and the **Economic Injury Disaster Loan (EIDL)** program — examining how loan volume and loan amounts were distributed across U.S. states and industries (NAICS codes), normalized against U.S. Census Annual Business Survey data.

## Overview

This project combines and analyzes SBA loan-level data from PPP and EIDL to answer: **which states and industries were helped the most and least by COVID-19 relief lending?** The analysis also cross-references findings with consumer spending recovery data from [Opportunity Insights](https://tracktherecovery.org/) to explore whether relief loan distribution helps explain differences in economic recovery between states.

## What's in this repo

| File | Description |
|---|---|
| `PPP_EIDL_Analysis_Code.ipynb` | Full analysis notebook: data loading, cleaning, merging, aggregation, normalization, and heat map generation |
| `PPP_EIDL_Analysis_Report.pdf` | Written report summarizing findings, methodology, and commentary on state/industry impact |
| `PPP_EIDL_Analysis_Presentation.pptx` | Slide deck summarizing the analysis and key results |
| `Project_Description.pdf` | Original assignment/task description |

## Methodology

1. **PPP data** — Loaded loan-level PPP data into an indexed pandas DataFrame, keeping `Loan Amount`, `Borrower's State`, `Date Approved`, and `NAICS Code` (restricted to 2-digit NAICS sectors). Added a `LoanProgram` column tagged `"PPP"`.
2. **EIDL data** — Loaded EIDL loan data (`ACTIONDATE`, `PRIMPLACEOFPERFORMANCECD`, `FACEVALUEOFDIRECTLOANORLOANGUARANTEE`), tagged rows `"EIDL"`, and derived `State` from the place-of-performance code.
3. **Merge** — Combined PPP and EIDL datasets into a single unified DataFrame, aligned by `State`, `Date`, `Amount`, `LoanProgram`, and `NAICS` code.
4. **Aggregation & normalization** — Computed total number of loans and total loan amount per state and NAICS sector, then normalized these against U.S. Census Annual Business Survey figures (e.g. number of establishments/employer firms) to control for baseline business activity.
5. **Visualization** — Produced U.S. choropleth heat maps of normalized loan count and loan amount by state using `geopandas` and `matplotlib`/`seaborn`.
6. **Recovery comparison** — Compared normalized lending intensity in North Carolina vs. Michigan (with a focus on NAICS 71 — Arts, Entertainment & Recreation) against Opportunity Insights' consumer spending recovery tracker to assess whether relief funding patterns help explain the divergence in economic recovery between the two states.

## Tech stack

- Python
- `pandas` — data loading, cleaning, merging, aggregation
- `geopandas` — geospatial heat maps
- `matplotlib`, `seaborn` — visualization
- Jupyter Notebook

## Data sources

- [SBA PPP Loan Data](https://data.sba.gov/dataset/ppp-foia)
- [SBA EIDL Loan Data](https://data.sba.gov/dataset/covid-19-eidl)
- [U.S. Census Bureau — Annual Business Survey](https://www.census.gov/programs-surveys/abs.html)
- [Opportunity Insights — Economic Tracker](https://tracktherecovery.org/)

## Key findings

See the full [analysis report](Final_Assignment/PPP_EIDL_Analysis_Report.pdf) for detailed commentary on which states and industries received the most and least normalized relief funding, and how this relates to differences in consumer spending recovery between North Carolina and Michigan.

## How to run

```bash
git clone https://github.com/KonGramm/<repo-name>.git
cd <repo-name>
pip install pandas geopandas matplotlib seaborn jupyter
jupyter notebook PPP_EIDL_Analysis_Code.ipynb
```

> Note: raw PPP/EIDL/Census source files are not included in this repo due to file size — download them from the links above and place them in a `data/` folder before running the notebook.

## Author

Konstantinos Grammatikopoulos
