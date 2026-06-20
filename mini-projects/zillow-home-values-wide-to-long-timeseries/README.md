# Zillow home value time series analysis
 
A short time series project that takes Zillow's wide-form home value dataset, reshapes it into a proper time series, and analyzes how typical home values moved across the four largest U.S. cities.
 
## Overview
 
Zillow publishes its Home Value Index (ZHVI) in wide form — one row per city, one column per month. That layout is great for a spreadsheet, but unusable for time series analysis. This project melts the data into long form, builds a clean monthly time series, and answers two concrete questions about home value trends around the 2008 financial crisis.
 
## Dataset
 
- **Source:** Zillow Home Value Index (ZHVI) — typical home value, single-family residential and condo, smoothed and seasonally adjusted, monthly
- **Scope:** filtered down to the 4 largest U.S. cities by `SizeRank`
- **Original shape:** one row per city, ~300+ columns (one per month, 2000–2026)
## Project workflow
 
### Part 1 — preparing the dataset
 
1. Load the raw ZHVI CSV
2. Filter to the 4 largest cities using the `SizeRank` column (`SizeRank < 4`) — not row position, since row order isn't guaranteed
3. Melt the wide-form data into long form (`Date`, `HomeValue` columns)
4. Convert `Date` to a proper `datetime` type and set it as the index
5. Resample to monthly frequency, grouped by city
### Part 2 — visualization and analysis
 
1. Plot all 4 cities' home values on one chart (unstacked by city), with a titled, labeled axis and y-axis ticks formatted as `$XXXK`
2. Answer two questions directly from the resampled data:
   - Which city had the highest and lowest typical home value at the end of 2008?
   - How much did home values change (in dollars) from November to December 2008?
## Key techniques used
 
- `melt()` — reshaping wide-form data into long-form for time series
- `groupby().resample()` — aggregating irregular city-level data into a uniform monthly frequency
- `unstack()` — pivoting a city-level multiindex back into side-by-side columns for plotting and comparison
- `diff()` — computing month-over-month dollar changes
- `pd.IndexSlice` — slicing a multiindex by date without unstacking
- `FuncFormatter` (matplotlib) — custom y-axis tick formatting
## Tools
 
- Python
- pandas
- matplotlib
## Files
 
| File | Description |
|---|---|
| `zillow-home-analysis.ipynb` | Full notebook: data prep, reshaping, resampling, plotting, and analysis |
| `zillow-home-data.txt` | Raw Zillow ZHVI dataset (wide-form) |
| `README.md` | Project overview and documentation (this file) |
 
## Notes
 
This project focuses specifically on **getting from wide-form to a clean, analysis-ready time series** — the resampling and reshaping steps are the core skill being demonstrated, not advanced forecasting.
 
