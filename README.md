# Stock-Price-Forecasting-for-High-Frequency-Trading


This repository hosts our market microstructure modeling project for the **Optiver Trading at the Close** Kaggle competition, developed as part of the **MSBA 6421 - Predictive Analytics** course at the Carlson School of Management.

📌 [Competition Overview](https://www.kaggle.com/competitions/optiver-trading-at-the-close/overview)

---

## 📈 Problem Context

The **closing auction** on NASDAQ is crucial for determining official end-of-day prices. It is typically characterized by:

- Surges in trading volume
- Abrupt shifts in buy/sell imbalance
- Elevated spreads and price volatility

Our goal was to develop a predictive pipeline that models **imbalance size in real time**, empowering traders to anticipate pressure points during the last 540 seconds of the trading day.

---

## 🎯 Project Objectives

- Segment the final 540 seconds into **three strategic windows**
- Engineer microstructure features that capture evolving intraday signals
- Build and fine-tune predictive models for each window
- Blend predictions to produce consolidated stock-level forecasts
- Optimize for **fast inference**, **low MAE**, and **robustness to feature drift**

---

## 🔍 Window-Based Modeling Framework

| Window | Time Interval (s) | 
|--------|-------------------|
| 0–290  | Early phase with tight spreads and low volatility |
| 300–470 | Imbalance build-up as auction book dynamics intensify |
| 480–540 | Volatility peaks under final match pressure |

Each window was independently modeled with tailored features, model types, and hyperparameters.

---

## 🛠️ Feature Engineering Highlights

We engineered over **220 features** per observation, grouped into:

1. **Calculated Microstructure Signals**  
   E.g., `spread`, `wap_diff`, `order_flow_imbalance`

2. **Same-Day Intraday History**  
   Rolling statistics such as `sd_mean`, `delta_sd`, `initial_0s`

3. **Intra-Window Momentum**  
   Trends within the same window (`delta_within_window`, `sw_mean`)

4. **Cross-Window Interactions**  
   Lagged signals and starting window comparisons

5. **Cross-Day Context**  
   Multi-day rolling stats (`rolling_mean_10_`, etc.)

---

## 🤖 Model Performance Summary

| Window | Models Tested          | Best MAE |
|--------|-------------------------|---------|
| 0–290  | CatBoost, GRU           | **6.11 (CatBoost)** |
| 300–470| CatBoost, GRU           | **5.22 (CatBoost)** |
| 480–540| CatBoost, GRU, LightGBM | **4.98 (CatBoost)** |

✅ **Blended Final MAE:** `5.4404`  
(Note: Due to Kaggle API issues, final evaluation used `revealed_targets.csv` locally.)

---

## 🚀 Deployment-Ready Stack

- ⚡ **Low-latency Inference:** Tree-based CatBoost models
- 📦 **Serialized Models:** Pickled for easy production deployment
- 🧩 **Modular Pipeline:** Supports per-window predictions
- 🗜️ **Optimized Features:** Balancing performance and memory efficiency

---


## 🗂 Project Directory

```

optiver-trading-at-the-close-predictive-modeling/
├── data/        # Raw and processed datasets
├── notebooks/   # EDA and modeling experiments
├── models/      # Trained model artifacts (.pkl files)
├── outputs/     # Submission files, logs, MAE reports
├── utils/       # Custom feature engineering scripts
└── README.md    # Project documentation

```


