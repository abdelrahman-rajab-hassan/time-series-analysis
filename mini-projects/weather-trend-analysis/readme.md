`<span class="token-keyword">#</span><span class="token-text"></span><span class="token-keyword">Weather Time Series Analysis</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-text">A time series analysis of London weather data, focusing on precipitation and temperature trends.</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-keyword">##</span><span class="token-text"></span><span class="token-keyword">Data</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-text">The dataset (`london_weather_MODIFIED.csv `) contains daily London weather records, filtered to the year 2000 onward. Key features used:</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-punctuation">- </span><span class="token-text">**precipitation** – daily rainfall (inches)</span>`

`<span class="token-punctuation">- </span><span class="token-text">**mean_temp** – average daily temperature</span>`

`<span class="token-punctuation">- </span><span class="token-text">**min_temp** – minimum daily temperature</span>`

`<span class="token-punctuation">- </span><span class="token-text">**max_temp** – maximum daily temperature</span>`

`<span class="token-punctuation">- </span><span class="token-text">**snow_depth** – daily snow depth</span>`

`<span class="token-keyword">##</span><span class="token-text"></span><span class="token-keyword">What This Notebook Does</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-punctuation">1. </span><span class="token-text">**Data Preparation**</span>`

`<span class="token-comment"></span><span class="token-punctuation">- </span><span class="token-text">Loads the data and converts the date column to a datetime index</span>`

`<span class="token-comment"></span><span class="token-punctuation">- </span><span class="token-text">Filters to 2000 onward and keeps only the relevant weather columns</span>`

`<span class="token-comment"></span><span class="token-punctuation">- </span><span class="token-text">Imputes missing values — mean for roughly symmetric features (`mean_temp `, `min_temp `, `max_temp `), median for heavily right-skewed features (`precipitation `, `snow_depth `), based on skewness scores and visual checks (box plots, histograms)</span>`

`<span class="token-punctuation">2. </span><span class="token-text">**Analysis & Visualizations**</span>`

`<span class="token-comment"></span><span class="token-punctuation">- </span><span class="token-text">**Q1:** Which month had the most precipitation between 2000–2010? Resamples precipitation to monthly totals, finds the peak month, and plots it with a labeled vertical line.</span>`

`<span class="token-comment"></span><span class="token-punctuation">- </span><span class="token-text">**Q2:** Which year between 2000–2020 had the coolest average temperature? Resamples mean temperature to yearly averages and visualizes the trend.</span>`

`<span class="token-keyword">##</span><span class="token-text"></span><span class="token-keyword">Tools Used</span>`

`<span data-prose-review-ignore=""> </span>`

`<span class="token-text">Python, pandas, matplotlib (including custom tick locators/formatters for date axes)</span>`
