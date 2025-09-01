# Stock Volatility Forecasting 

## Overview  
This project was developed as part of **Discipline Assessment 2** in the *DATA3888 Data Science Capstone* (University of Sydney).  
It was an **individual project** designed as a client presentation task.  

The client, *Louis (a quantitative trader)*, requested an **interpretable model** to forecast realized volatility from high-frequency stock data (`stock_1.csv`).  
The work required both rigorous technical modeling and clear communication to a client with introductory data science knowledge.  

**Code + Output:**  
- [Full HTML Report](./Discipline%20Assessment%202%20-%20Stock-1.html)  

---

## Objectives  
- **Forecast realized stock volatility** using high-frequency features.  
- **Compare candidate models**:  
  - Linear Regression (baseline, interpretable).  
  - HAR-RV (Heterogeneous AutoRegressive Realized Volatility model, with WLS adjustment).  
  - XGBoost (nonlinear, tree-based model for richer feature interactions).  
- **Explain results clearly to a non-technical audience** through a 3-minute presentation.  
- **Justify final model choice** with evaluation metrics, interpretability trade-offs, and limitations.  

---

## Data & Features  
- Source: `stock_1.csv` (workshop dataset).  
- Target: **Realized Volatility** = √(Σ log_return²), computed in 20-second buckets  
- Features engineered:  
  - Weighted Average Price (WAP).  
  - Bid-Ask Spread.  
  - Log Returns (mean & standard deviation).  
  - Aggregated microstructure features per `time_id`.  
- Train/validation split: **80/20**, preserving chronological order

---

## Candidate Models  
- **Linear Regression**  
  - Predictors: WAP, Order Size, Bid-Ask Spread.  
  - Local patterns captured per `time_id`.  
  - Adjusted R² ≈ 0.50:contentReference[oaicite:2]{index=2}.  

- **HAR-RV (with WLS)**  
  - Predictors: past volatility (volₜ₋₁, mean_vol over last 5 buckets).  
  - WLS adjustment accounts for heteroskedasticity.  
  - Adjusted R² ≈ 0.40:contentReference[oaicite:3]{index=3}.  

- **XGBoost (Tree-Based Regression)**  
  - Captures nonlinearities, interactions, and outliers.  
  - No stationarity or normality assumptions.  
  - R² ≈ 0.95, QLIKE ≈ 0.0083 (best performing):contentReference[oaicite:4]{index=4}.  
  - Top feature: `log_return_sd`.  

---

## Results & Model Selection  
- **Final model:** **XGBoost**  
  - Outperformed Linear Regression and HAR-RV on all error metrics.  
  - Robust to noise and nonlinear effects.  
  - Trade-off: less interpretable than linear models.  

- **Communication focus:** Results were distilled into client-friendly language, with visualizations and simplified explanations to bridge technical concepts with business decisions.  

---

## Tech Stack  
- **Language:** Python  
- **Libraries:** pandas, scikit-learn, xgboost, matplotlib  
- **Methods:** HAR-RV, WLS, XGBoost, error analysis (MAE, RMSE, R², QLIKE)  

---

## Deliverables  
- **Notebook:** Data prep, model training, evaluation.  
- **Presentation:** 3-minute client pitch with results and limitations.  
