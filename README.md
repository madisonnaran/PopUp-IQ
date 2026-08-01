# PopUp IQ

PopUp IQ is a data-driven venue intelligence tool that scores NYC neighborhoods for pop-up bar placement using public datasets, Python for data processing and modelling, and Power BI for visualization and interactive reporting.

## What it does
- Aggregates and cleans public NYC datasets (foot traffic proxies, land use, zoning, liquor licenses, transit access, demographics, and commercial vacancy where available).
- Engineers features and computes a neighborhood suitability score for pop-up bars.
- Produces interactive Power BI dashboards to explore scores, drivers, and candidate locations.

## Tech stack
- Python (pandas, geopandas, scikit-learn)
- Power BI for dashboards and maps
- Public data sources: NYC Open Data, Census/ACS, MTA, Department of Health, Business licensing records

## Getting started
1. Collect relevant public datasets (NYC Open Data, ACS, MTA, liquor licenses).
2. Use Python scripts to clean, join, and geospatially aggregate data to neighborhood / census tract level.
3. Engineer features (accessibility, density, nightlife activity, competition, spending power) and compute a composite suitability score.
4. Export aggregated tables to CSV/Parquet and load into Power BI for visualization and final site selection.

## Notes
- Keep personal or proprietary data separate from public datasets.
- Adjust scoring weights to reflect business priorities (foot traffic vs. cost vs. licensing risk).

## License
MIT