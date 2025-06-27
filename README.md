
# Demand Forecasting for Inventory Management

Combined Holt‑Winters × Linear Regression model for monthly SKU demand  
**MAPE ↓ 42 % vs. baseline**, validated on 5‑year history (74 observations)

---

## 🚀 Project Overview

This repository contains the code, data and documentation for my IHK-certified capstone project in Data and Process Analysis.  
The goal was to build a lightweight yet accurate forecasting pipeline that could be integrated into the company's inventory system and used by supply‑chain stakeholders to manage safety stock and reorder points effectively.

- **Time‑series models:** Holt‑Winters triple exponential smoothing (additive), SARIMA  
- **Machine learning:** multivariate Linear Regression  
- **Ensemble:** weighted blend with grid search for optimal weights  
- **Domain:** single high‑volume SKU, monthly granularity, 5 years of history

---

## 📂 Repository Structure

```
.
├── data/
│   └── sample_demand.csv          # anonymized SKU-level demand + inventory data
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_modeling_holt_winters.ipynb
│   ├── 03_modeling_linear_reg.ipynb
│   ├── 04_modeling_sarima.ipynb
│   └── 05_blending_evaluation.ipynb
├── src/
│   ├── dataset.py                 # data loading & preprocessing
│   ├── models.py                  # training & evaluation
│   └── predict.py                 # CLI entry-point
├── figures/                       # key plots
│   ├── hw_vs_actual.png
│   ├── sarima_vs_actual.png
│   └── ensemble_vs_actual.png
├── results/
│   └── metrics.csv
├── requirements.txt
└── LICENSE
```

---

## 🧑‍💻 Quick‑start

```bash
# 1. clone repo
$ git clone https://github.com/<your‑user>/inventory‑forecasting.git && cd inventory‑forecasting

# 2. create env & install
$ python -m venv .venv && source .venv/bin/activate
$ pip install -r requirements.txt

# 3. run quick forecast (outputs metrics to console)
$ python src/predict.py --train data/sample_demand.csv --horizon 6
```

Notebooks are sequential and cache intermediate results under `results/`.

---

## 🔢 Key Results

| Model                          | MAE   | MSE    | RMSE  | MAPE % |
|-------------------------------|-------|--------|-------|--------|
| Holt‑Winters (additive)       | 32.49 | 1 367  | 36.97 | 2.64   |
| Linear Regression             | 21.06 | 638    | 25.26 | 1.62   |
| Combined (optimized weights)  | 19.29 | 489    | 22.10 | 1.52   |
| SARIMA                        | 53.42 | 4 868  | 69.77 | 4.39   |

The combined model reduced MAPE by **42% vs. Holt-Winters**, balancing bias and variance on a 20% hold-out test set.

---

## 📊 Example Visualisations

*(To be added in `/figures`)*

---

## 🧠 Lessons Learned / Next Steps

- Why a simple linear blend outperformed more complex SARIMA
- Extend to multi-SKU and hierarchical forecasting
- Add experiment tracking (MLflow), containerize inference (Docker)

---

## 🗃 Data

The original dataset was sourced from the company’s internal system and contains real sales data for a single anonymized product (SKU).  
Only date, demand, and inventory were used; 74 monthly observations were retained.  
Due to confidentiality, only anonymized and reduced data is provided in the repository.

---

## 🙋‍♀️ Author

**Irina Merzdorf**  
Fachinformatikerin für Daten- und Prozessanalyse (IHK), 2025  
Capstone project graded *"gut"* (91/100) by the IHK Lübeck examination board

---

## 📜 License

MIT License. Anonymized sample data is included and may be reused freely.
