# 📈 Macroeconomic Unemployment Rate Prediction with XGBoost

An empirical machine learning and econometric panel data study evaluating non-linear relationships between macroeconomic aggregates (CPI, Industrial Production, Discount Rate) and national unemployment rates across 8 structurally diverse economies (2000–2024).

---

## 📌 Research Overview & Core Findings
> **Core Hypothesis:** Is national unemployment driven primarily by universal macroeconomic rules or by country-specific structural institutions?

* **Exceptional Predictive Accuracy:** A hyperparameter-optimized XGBoost regression pipeline captured non-linear structural shocks across economies, achieving an **$R^2$ of 0.99**, an **MAE of 0.17**, and an **RMSE of 0.28** on test splits.
* **Empirical Feature Attribution:** Country dummy variables (Poland, South Korea, Turkey) dominated feature importance rankings, proving that localized structural dynamics and labor institutional flexibility outweigh universal aggregates like CPI and Industrial Production in explaining employment variance.

---

## 📊 Benchmark & Evaluation Results

| Metric | Score | Description |
| :--- | :---: | :--- |
| **Coefficient of Determination ($R^2$)** | **0.99** | Explains 99% of total variance across multi-country panel observations |
| **Mean Absolute Error (MAE)** | **0.17** | Average absolute deviation of predicted unemployment rate |
| **Root Mean Squared Error (RMSE)** | **0.28** | Penalized error metric for large idiosyncratic forecasting outliers |

### Hyperparameter Configuration
* `learning_rate`: 0.05
* `n_estimators`: 1,000
* `max_depth`: 6
* `subsample`: 0.80
* `colsample_bytree`: 0.80
* `early_stopping_rounds`: 50

---

## 📉 Visualizations & Results

### 1. Actual vs. Predicted Unemployment (Across 8 Countries)
Ground truth historical rates vs. model predictions across divergent economic trajectories:
![Actual vs Predicted](assets/actual_vs_predicted.png)

### 2. Feature Importance (Information Gain)
Dominance of country-specific fixed effects over universal macroeconomic aggregates:
![Feature Importance](assets/feature_importance.png)

### 3. Macroeconomic Correlation Matrix
Correlation heatmap between unemployment, discount rates, industrial output, and inflation:
![Correlation Matrix](assets/correlation_matrix.png)

---

## 📁 Dataset Details
* **Source:** Federal Reserve Bank of St. Louis (FRED)
* **Time Span:** Monthly panel data from 2000 to 2024
* **Countries (8):** USA, Germany, Brazil, South Korea, Japan, Mexico, Poland, Turkey
* **Key Indicators:**
  * **Target:** `ISSIZLIK` (Unemployment Rate %)
  * **Predictors:** 
    * `TUFE`: Consumer Price Index (CPI)
    * `SURETIM`: Industrial Production Index
    * `ISFAIZ`: Discount Rate (Investment Cost Proxy)
    * Country-specific dummy encodings (One-Hot Encoded)

---

## 📂 Repository Layout
```text
macroeconomic-unemployment-xgboost/
├── assets/
│   ├── actual_vs_predicted.png       # 8-country comparative time series plots
│   ├── feature_importance.png        # XGBoost information gain rankings
│   └── correlation_matrix.png        # Cross-indicator correlation heatmap
├── data/
│   ├── processed/
│   │   └── hepsi_bir_arada_ulkeler_verisi.csv # Cleaned & merged panel data
│   └── raw/                          # Country-level raw monthly CSVs from FRED
├── notebooks/
│   └── macroeconomic_analysis.ipynb  # End-to-end data processing, EDA & XGBoost modeling
├── reports/
│   └── Aleyna_Sahan_VeriAnalizi.pdf  # Full academic thesis documentation
├── requirements.txt                  # Python dependencies
└── README.md
