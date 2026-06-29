# 📈 Walmart Stock Forecasting with ARIMA

A time series project that forecasts Walmart (WMT) **Adjusted Close** prices for the next quarter using an ARIMA model. 🛒

---

## 🎯 Goal
Use Walmart stock data from **2010 to 2020** to predict the Adjusted Close values for the next quarter (13 weeks × 5 business days = 65 trading days).

---

## 🧰 Tools & Libraries
- 🐍 Python
- 🐼 pandas / numpy
- 📊 matplotlib / seaborn
- 📐 statsmodels (ARIMA, ADF, ACF/PACF)
- 🔮 pmdarima (ndiffs)
- 📏 scikit-learn (MAPE, RMSE)

---

## 🔁 Workflow
1. 📥 **Load & inspect** the dataset (nulls, duplicates, data types)
2. 🗓️ **Datetime index** with business-day frequency (`'B'`)
3. 🧹 **Handle missing values** with forward fill (closed-market days)
4. ✂️ **Slice** the data to 2010–2020
5. 🧪 **Stationarity check** with the ADF test + `ndiffs` → found **d = 1**
6. 📉 **ACF / PACF** plots to estimate `p` and `q`
7. 🔀 **Train/test split** (last 65 business days as test)
8. 🤖 **Fit ARIMA**, forecast, plot, and evaluate
9. 🔍 **Compare orders** in a loop to pick the best

---

## 🏆 Final Model: ARIMA(0,1,0)
- ✅ Lowest **MAPE: 2.46%** and the simplest model (a random walk)
- 📊 Adding AR/MA terms did **not** improve results → no extra structure to exploit
- 👀 Visually the forecast is a **flat line** near the last training price: it captures the price *level*, not the daily *direction* — expected behavior for stock data

---

## 📂 Project Structure
```
.
├── 📄 WMT.csv            # Walmart stock data (Date, Adj Close)
├── 📓 arima-model.ipynb  # Notebook: full ARIMA workflow & analysis
└── 📝 README.md          # Project overview (this file)
```
