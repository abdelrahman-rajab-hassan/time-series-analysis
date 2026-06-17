# 🌦️ Weather Time Series Analysis
 
A time series analysis of London weather data, focusing on precipitation and temperature trends.
 
## 📊 Data
 
The dataset (`london_weather_MODIFIED.csv`) contains daily London weather records, filtered to the year 2000 onward. Key features used:
 
- 🌧️ **precipitation** – daily rainfall (inches)
- 🌡️ **mean_temp** – average daily temperature
- ❄️ **min_temp** – minimum daily temperature
- 🔥 **max_temp** – maximum daily temperature
- ⛄ **snow_depth** – daily snow depth
## 🧠 What This Notebook Does
 
1. **Data Preparation**
   - Loads the data and converts the date column to a datetime index
   - Filters to 2000 onward and keeps only the relevant weather columns
   - Imputes missing values — mean for roughly symmetric features (`mean_temp`, `min_temp`, `max_temp`), median for heavily right-skewed features (`precipitation`, `snow_depth`), based on skewness scores and visual checks (box plots, histograms)
2. **Analysis & Visualizations**
   - **Q1:** 🌧️ Which month had the most precipitation between 2000–2010? Resamples precipitation to monthly totals, finds the peak month, and plots it with a labeled vertical line.
   - **Q2:** 🥶 Which year between 2000–2020 had the coolest average temperature? Resamples mean temperature to yearly averages and visualizes the trend.
## 🛠️ Tools Used
 
Python, pandas, matplotlib (including custom tick locators/formatters for date axes)
 
## 📁 Repo Structure
 
```
weather-trend-analysis/
├── 📄 README.md
├── 📓 weather-time-series-analysis.ipynb
└── 📊 london_weather_MODIFIED.csv
```
 
