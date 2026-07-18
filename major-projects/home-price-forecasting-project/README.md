# 🏡 Oregon Home Value Forecast

## What is this project?

This project looks at historical housing price data and tries to answer a simple question:

> **"Based on how home prices have changed over the last 18 years, what will they look like a year from now?"**

We focus specifically on the **state of Oregon**, using real housing data from Zillow going back to the year 2000.

Think of it like looking at a chart of someone's savings account balance over many years, spotting the pattern in how it grows (or drops), and then using that pattern to make an educated guess about next year's balance.

---

## What did we actually do?

### Part 1 — Getting to know the data
- Loaded a large spreadsheet of home prices, one row per neighborhood, one column per month, going back to the year 2000.
- Reshaped it into a simpler format: one row per neighborhood *per month*, so it's easier to analyze over time.
- Saved a smaller, filtered version of the data (just five West Coast states, and just 2010–2020) that's ready to be plugged into Tableau, a data visualization tool.
- Plotted a chart comparing average home prices across states over time.

### Part 2 — Focusing on Oregon and predicting the future
- Filtered the data down to just Oregon, and calculated the average home price for each month from January 2000 to December 2018.
- Checked that there was no missing/incomplete data (there wasn't — nothing to clean up).
- Looked for repeating seasonal patterns (like "prices always go up every summer"). We found the seasonal effect was tiny and not worth worrying about — the real story was the long-term ups and downs (a boom, the 2008 housing crash, then a recovery).
- Used statistics to figure out how much "smoothing" the data needed before it could be reliably modeled.
- Tried two different approaches to build a forecasting model:
  1. A model we tuned by hand, using careful reasoning about the data.
  2. An automated tool that picks the best settings on its own.
- Compared both models by hiding the last 12 months of real data, having each model "guess" those months, and checking how close the guesses were. **Our hand-tuned model was about 18 times more accurate** than the automated one.
- Used our best model to make a genuine forecast — predicting Oregon home prices for the **12 months after the data ends** (i.e., real predictions about the future, not just a test).
- Summarized the forecast: what the predicted price will be in the final month, and how much prices are expected to change (in percent) over that year.

---

## Why does this matter?

This is the same basic approach used by real estate analysts, economists, and investors to answer questions like:
- Is now a good time to buy or sell?
- Are prices in this area expected to keep rising?
- How reliable is a given prediction, and when might it be wrong (e.g., during a crisis)?

---

## 📁 Folder structure

```
home-price-forecasting-project/                     
├── README.md                                    You are here
├── oregon-home-value-forecast.ipynb.ipynb The   main notebook — all the analysis and forecasting steps
├── zillow-home-values.csv                       The raw dataset from Zillow (all U.S. neighborhoods)
└── data-for-tableau.csv                         A filtered, cleaned-up version of the data for use in Tableau
```
