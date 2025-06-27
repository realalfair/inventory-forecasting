# 📦 Demand Forecasting for Inventory Management

Combined Holt‑Winters × Linear Regression model for monthly SKU demand  
**MAPE ↓ 42 %** vs. baseline, validated on 5‑year history (74 observations)

---

## 🚀 Project Overview

This repository contains the code and documentation for my IHK capstone project _"Forecasting Data for Inventory Management and Demand Planning."_ The goal was to build a robust, interpretable forecast pipeline for a high-demand SKU, deployable in the WEMALO customer system to support better stock control decisions.

- **Time series:** triple exponential smoothing (Holt-Winters)
- **Machine learning:** multivariate linear regression
- **Ensemble:** weighted combination with grid search
- **Validation:** 80/20 split, residual diagnostics, MAPE/RMSE/MAE
- **Data:** 5 years monthly data (74 points), from 4e digital GmbH internal system

---

## 📂 Repository Structure

```
.
├── data/                # synthetic example dataset
│   └── sample_demand.csv
├── notebooks/
│   ├── 01_data_analysis.ipynb
│   ├── 02_holt_winters_model.ipynb
│   ├── 03_linear_regression_model.ipynb
│   ├── 04_combined_model.ipynb
│   └── 05_sarima_comparison.ipynb
├── src/
│   ├── preprocess.py    # feature creation, train/test split
│   ├── models.py        # modeling and metrics
│   └── forecast.py      # CLI entrypoint
├── figures/
│   ├── holt_vs_actual.png
│   ├── lr_vs_actual.png
│   ├── combined_vs_actual.png
│   └── sarima_vs_actual.png
├── results/
│   └── evaluation.csv
├── requirements.txt
└── README.md
```

---

## 🧑‍💻 Quick‑start

```bash
# 1. clone repo
$ git clone https://github.com/<your-username>/inventory-forecasting.git && cd inventory-forecasting

# 2. set up environment
$ python -m venv .venv && source .venv/bin/activate
$ pip install -r requirements.txt

# 3. run sample forecast
$ python src/forecast.py --train data/sample_demand.csv --horizon 3
```

---

## 🔢 Key Results

| Model                 | MAE   | RMSE  | MAPE (%) |
|----------------------|-------|-------|----------|
| Holt-Winters         | 32.49 | 36.97 | 2.64     |
| Linear Regression     | 21.06 | 25.26 | 1.62     |
| Combined (opt-weight)| 19.29 | 22.10 | 1.52     |
| SARIMA               | 53.42 | 69.77 | 4.39     |

⚡ _Combined ensemble reduced MAPE by 42 % vs. Holt-Winters baseline._

---

## 📊 Visualizations

<img src="figures/combined_vs_actual.png" width="600"/>

---

## 📈 Business Use

The forecasts feed into a simple reorder calculator for determining safety stock and reorder points based on historical demand, variability, lead time, and service level. Output is intended to be used in the WEMALO system via JSON API.

---

## 🗃 Data

Original client data is confidential. A synthetic dataset is included in `data/`, preserving the structure (SKU, Date, Demand, Inventory).

---

## 📝 Lessons Learned

- Model ensembles are powerful even with simple methods
- Preprocessing (e.g., lag features, seasonality) has a huge impact
- SARIMA is strong in theory but needs careful tuning for real-world use
- Collaborative feedback improves both model and documentation quality

---

## 🙋‍♀️ Author

**Irina Merzdorf**  
Fachinformatikerin für Daten- und Prozessanalyse (IHK), 2025  
Capstone project rated *"sehr gut"* by IHK Lübeck

---

## 📜 License

MIT License. Sample data is synthetic and freely reusable.
