# 🏠 U.S. Housing Price Analysis

**Exploring how inflation, interest rates, GDP, unemployment, and the stock market drive U.S. housing prices (2000–2025)**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange.svg)](https://jupyter.org/)

A DSA 210 data science project by **Bardiya Shavandi**, investigating whether macroeconomic forces — inflation, interest rates, mortgage debt, GDP, unemployment, and the stock market — can explain and predict movements in the U.S. House Price Index (USSTHPI) between 2000 and 2025.

📄 **[Read the full project report →](Report.md)**

---

## 📌 Overview

Housing prices touch nearly everyone — homeowners, renters, investors, and policymakers alike. This project asks a simple question with a complex answer: **which economic forces actually move the U.S. housing market, and by how much?**

Using two decades of public economic data, the project combines exploratory data analysis, statistical hypothesis testing, and machine learning to quantify the relationship between six economic indicators and the national House Price Index.

### Research Questions

1. How do inflation rates (CPI) influence real estate prices in the U.S.?
2. What is the impact of interest rate changes on the housing market?
3. Does the stock market have a significant correlation with housing market performance?
4. How do Mortgage Debt Service Payments (MDSP) influence housing prices?
5. How do GDP and unemployment relate to housing price trends?

Each question was tested as a formal null/alternative hypothesis pair using Pearson correlation, then explored further with predictive modeling.

---

## 📊 Data Sources

| Indicator | Series | Source |
|---|---|---|
| House Price Index (target) | `USSTHPI` | [FRED](https://fred.stlouisfed.org/series/USSTHPI) |
| Inflation (CPI) | `CPIAUCSL` | [FRED](https://fred.stlouisfed.org/series/CPIAUCSL) |
| Interest Rates | `FEDFUNDS` | [FRED](https://fred.stlouisfed.org/series/FEDFUNDS) |
| Mortgage Debt Service Payments | `MDSP` | [FRED](https://fred.stlouisfed.org/series/MDSP) |
| GDP | `GDP` | [FRED](https://fred.stlouisfed.org/series/GDP) |
| Unemployment Rate | `UNRATE` | [FRED](https://fred.stlouisfed.org/series/UNRATE) |
| Stock Market Closing Prices | `Close` | [Kaggle](https://www.kaggle.com/datasets/ahmadrafiee/stock-market) |

All series are filtered to a consistent **2000–2025** observation window and merged on date. Raw CSVs are available in [`Data_raw/`](Data_raw).

---

## 🧪 Methodology

1. **Data collection & cleaning** — handled missing values (forward/backward fill), standardized date formats, and aligned all series to a shared time index.
2. **Outlier detection** — used box plots, Z-scores, and IQR to flag and review extreme values.
3. **Feature engineering** — built lagged variables and rolling averages (e.g., 3-month CPI/Fed Funds averages) to capture momentum and seasonality.
4. **Exploratory analysis** — histograms, scatter plots, time series plots, and a Pearson correlation heatmap.
5. **Hypothesis testing** — Pearson correlation with p-value < 0.05 as the significance threshold for each economic factor.
6. **Predictive modeling** — Linear Regression, Random Forest Regressor, and K-Nearest Neighbors to predict `USSTHPI`.
7. **Unsupervised learning** — K-Means clustering (k=3, selected via the Elbow Method) with PCA for visualization, to uncover hidden economic regimes.

---

## 🔍 Key Findings

| Indicator | Correlation with Housing Prices | Strength |
|---|---|---|
| GDP | ≈ +0.89 | Very strong, positive |
| Inflation (CPI) | ≈ +0.84–0.86 | Very strong, positive |
| Stock Market | ≈ +0.37 | Moderate, positive |
| Unemployment | ≈ −0.29 | Moderate, negative |
| Interest Rates (FEDFUNDS) | ≈ −0.10 | Weak, negative |
| Mortgage Debt (MDSP) | ≈ +0.006 (not significant) | None |

**Model performance** (predicting `USSTHPI`):

- **Random Forest Regressor**: R² ≈ 0.999 — best overall fit; CPI's 3-month rolling average emerged as the single most important predictor.
- **Linear Regression (with lag features)**: R² ≈ 0.999
- **Linear Regression (without lag features)**: R² ≈ 0.956 — confirms raw economic indicators alone carry strong predictive signal.
- **K-Means Clustering**: identified 3 distinct economic regimes (e.g., volatile vs. stable periods) without using housing prices as an input.

**Bottom line:** inflation and GDP are the dominant drivers of long-run housing price trends in this dataset, while interest rates and mortgage debt show comparatively weak standalone effects. Lag and rolling-average features meaningfully improve predictive accuracy, suggesting housing prices carry strong momentum.

For the full breakdown — including every visualization, hypothesis test, and model evaluation — see **[Report.md](Report.md)**.

---

## 🛠️ Tech Stack

- **Language:** Python 3
- **Data handling:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Statistics:** `scipy.stats`
- **Machine learning:** `scikit-learn` (`LinearRegression`, `RandomForestRegressor`, `KNeighborsRegressor`, `KMeans`, `PCA`, `StandardScaler`)
- **Environment:** Jupyter Notebook (Google Colab)

---

## 📁 Repository Structure

```
US-Housing-Price-Analysis/
├── Data_raw/                   # Raw CSV datasets (CPI, Fed Funds, GDP, MDSP, Stock Market, UNRATE, HPI)
├── Project.ipynb               # Full analysis notebook: cleaning, EDA, hypothesis testing, ML models
├── Report.md                   # Detailed write-up of methodology, findings, and conclusions
├── README.md                   # Project overview (this file)
└── LICENSE                     # MIT License
```

---

## 🚀 Getting Started

```bash
git clone https://github.com/Bardiyashavandi/US-Housing-Price-Analysis.git
cd US-Housing-Price-Analysis
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
jupyter notebook Project.ipynb
```

The notebook runs end-to-end: load raw CSVs from `Data_raw/`, clean and merge them, then reproduce every chart, hypothesis test, and model in the report.

---

## ⚠️ Limitations & Future Work

- Results rely on the quality and completeness of historical public data.
- National-level data may obscure regional housing market differences.
- No advanced time-series models (e.g., ARIMA, LSTM) were used — a natural next step for improving forecasts.
- Future iterations could incorporate state- or city-level data, additional variables (income, population growth, housing supply), or an interactive forecasting dashboard.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

## 👤 Author

**Bardiya Shavandi** — DSA 210, Sabancı University
