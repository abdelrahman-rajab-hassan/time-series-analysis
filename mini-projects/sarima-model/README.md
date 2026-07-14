# SARIMA Home Value Forecasting

Forecasts New York City's typical home value 6 months into the future using SARIMA models fit on Zillow Home Value Index (ZHVI) data.

## Key Results

| Metric | Manual SARIMA(1,1,0)(1,0,0,12) | auto_arima SARIMA(1,1,1)(0,0,0,12) |
|---|---|---|
| MAE | $12,737 | **$12,012** |
| RMSE | $14,203 | **$13,396** |
| MAPE | 1.56% | **1.48%** |

- `auto_arima` beat the manually-specified model on all three test-set metrics, but the notebook's final refit cell uses the manual model's orders `(1,1,0)(1,0,0,12)` — see [Limitations](#limitations--next-steps).
- **6-month-ahead forecast (final refit, entire history through May 2026):** typical NYC home value holds essentially flat at **~$817.8K**, moving from $817,751 (Jun 2026) to $817,764 (Nov 2026) — a net change of **+$13 (+0.002%)**.
- So what: over this horizon the model finds no meaningful momentum in either direction — useful as a "no big swing expected" signal, not as a precise dollar forecast (see caveats below).

## Problem Statement

Given ~26 years of monthly home value data for the largest US metro (New York City), can we forecast typical home values 6 months ahead with reasonable accuracy? This is a standard real-estate/market-timing question: buyers, sellers, lenders, and city planners want a short-horizon view of where prices are headed. The exercise compares a manually-specified SARIMA model (built from ACF/PACF/ADF diagnostics) against an automatically tuned one (`pmdarima.auto_arima`) to see whether automated order search adds value over manual time-series diagnostics.

## Data

- **Source:** Zillow Home Value Index (ZHVI), `zillow-home-analysis.csv` (~93 MB, not tracked in this repo folder listing beyond the raw CSV).
- **Raw shape:** one row per U.S. city/region, one column per month from `2000-01-31` to `2026-05-31` (325 columns), plus metadata (`RegionID`, `SizeRank`, `RegionName`, `RegionType`, `StateName`, `State`, `Metro`, `CountyName`).
- **Filtered subset used for modeling:** the 4 largest cities by `SizeRank` (New York, Los Angeles, Houston, Chicago), melted to long form and resampled to monthly (`MS`) frequency, then further filtered to **New York only, from 2018-01-01 onward** (95 monthly observations feeding the train/test split).
- **Caveats:**
  - ZHVI is itself a smoothed, model-based estimate from Zillow (not raw transaction prices), so it already embeds Zillow's own imputation/smoothing assumptions.
  - Data through 2026 in this CSV extends past the "current date" of many analyses — treat any date beyond the actual data pull date as Zillow's own nowcast/estimate, not observed sales.
  - No explicit missing values in the modeled New York series (`isna().sum()` == 0), but the wider raw file may contain gaps for smaller regions not used here.
  - Single-city model: no exogenous macro features (rates, inventory, income) are included, so the forecast is a pure univariate extrapolation of past price behavior.

## Methodology

1. **Load & filter:** read the full ZHVI CSV, filter to the 4 largest cities via `SizeRank`.
2. **Reshape:** `melt()` wide date columns into long form (`Date`, `HomeValue`), parse `Date` to `datetime`, set as index.
3. **Resample:** `groupby('RegionName').resample('MS').mean()` to enforce monthly-start frequency per city.
4. **Exploratory analysis:** plot all 4 cities' home values; answer point questions (highest/lowest value at end of 2008, Nov→Dec 2008 change via `.diff()`).
5. **Series prep (New York):** filter to 2018-01-01 onward, confirm no nulls.
6. **Seasonality check:** `seasonal_decompose(model='additive', period=12)` → confirmed a regular seasonal component.
7. **Stationarity & orders:**
   - Augmented Dickey-Fuller test on the raw series (non-stationary, p=0.616).
   - `pmdarima.ndiffs` → 1 order of differencing needed.
   - ACF/PACF plots on the once-differenced series to select AR/MA orders manually.
8. **Train/test split:** last 6 months held out as test (to match the 6-month forecast horizon); remainder is training data.
9. **Manual model:** `SARIMAX(order=(1,1,0), seasonal_order=(1,0,0,12))` fit on training data.
10. **Automated model:** `pmdarima.auto_arima` (stepwise search minimizing AIC, `d=1, D=0, m=12`) → best order `(1,1,1)(0,0,0,12)`, refit as `SARIMAX` on training data for consistent metric comparison.
11. **Evaluation:** MAE, RMSE, MAPE for both models on the 6-month test set.
12. **Final forecast:** refit the selected order on the **full** series (train+test) and forecast 6 months beyond the end of the dataset; compute raw and percent net change between the first and last forecast months.

## Results & Evaluation

- Both models track the test period closely (MAPE < 2%), with `auto_arima` edging out the manual model on every metric (MAE, RMSE, MAPE all lower).
- Both models' 6-month forecasts are nearly flat lines near the last observed value — consistent with a series that, after differencing, still shows limited short-term signal beyond its recent level and mild seasonal AR term.
- Diagnostics on both fitted models show significant Ljung-Box statistics (p < 0.05), indicating residual autocorrelation remains — i.e., the models likely haven't captured all the structure in the series (see limitations).
- No baseline (e.g., naive "last value" or seasonal-naive) comparison was computed in the notebook — see next steps.

## Reproducibility

**Environment:** Python 3.12, with:
```
numpy
pandas
matplotlib
statsmodels
pmdarima
scikit-learn
```
No `requirements.txt` is currently checked into this folder — create one with `pip freeze > requirements.txt` in your working environment, or install the packages above via pip/conda.

**Seed:** SARIMAX/auto_arima fits here are deterministic (maximum-likelihood optimization, no random seed dependency), so results should reproduce exactly given the same input data and package versions.

**How to run end-to-end:**
1. Place `zillow-home-analysis.csv` in this folder (same directory as the notebook).
2. `pip install numpy pandas matplotlib statsmodels pmdarima scikit-learn`
3. Open `sarima-model.ipynb` and run all cells top to bottom (Part 1 → Part 2 → Time Series Models section).
4. Note: the final-refit cell (`final_order`, `final_seasonal_order`) currently hardcodes `(1,1,0)` / `(1,0,0,12)` — update these to match whichever model you select as "final" before trusting the future forecast (see Limitations).

## Project Structure

```
sarima-model/
├── sarima-model.ipynb       # Full analysis: load → reshape → EDA → stationarity → manual SARIMA → auto_arima → final forecast
├── zillow-home-analysis.csv # Raw ZHVI data, all US regions, monthly columns 2000-01 through 2026-05
└── README.md                # This file
```

## Limitations & Next Steps

- **Inconsistency in the notebook:** the metrics comparison identifies `auto_arima`'s `(1,1,1)(0,0,0,12)` as the lower-error model, but the final full-history refit cell still uses the manual model's orders `(1,1,0)(1,0,0,12)`. The "Final Model" markdown conclusion is also left with unfilled placeholders. This should be reconciled before treating the reported future forecast as the intended "best" one — refit with `(1,1,1)` and no seasonal AR term to see if the future forecast changes materially.
- **No baseline model:** add a naive/seasonal-naive forecast (e.g., repeat last value, or last year's same month) to confirm the SARIMA models actually add value over a trivial baseline.
- **Residual autocorrelation:** significant Ljung-Box results on both models suggest unmodeled structure remains; a broader `auto_arima` search (larger `max_P`/`max_Q`, allow `D>0`) or a different seasonal treatment could improve fit.
- **Single city, univariate:** extending to Los Angeles, Houston, and Chicago (already loaded) would test whether the same order generalizes, or whether each city needs its own tuned model.
- **No exogenous regressors:** mortgage rates, housing inventory, or regional employment data (SARIMAX supports exogenous variables) could improve accuracy, especially over longer horizons.
- **Confidence intervals:** the 95% CI bands are plotted but not summarized numerically — reporting interval width alongside the point forecast would better convey forecast uncertainty (the near-zero point change is well within typical CI width).
- **Longer/rolling backtests:** a single 6-month holdout is a small test set; walk-forward cross-validation across multiple 6-month windows would give a more robust accuracy estimate.

## License & Contact

Educational/practice project (mini-project exercise). No license specified — treat as personal practice work, not licensed for redistribution.

Questions: abdelrahman.r.hassan@gmail.com
