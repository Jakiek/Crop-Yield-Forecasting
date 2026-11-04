# Crop Yield Forecasting Under Climate Stress

Machine learning project for the Artificial Intelligence course at Universitas Gadjah Mada (2026), themed on SDG 13: Climate Action.

The model predicts annual rice production (in thousand tons) for 18 regencies in West Java from climate data and harvest area, using a **multiple linear regression with optional L2 (Ridge) regularization built from scratch** with gradient descent.

## Results (unseen 2024 test data)

| Metric | Value |
|---|---|
| R² | 0.98 |
| RMSE | 47.27 thousand tons |
| MAE | 37.48 thousand tons |

## Data

- **Climate:** daily mean temperature and total rainfall from the [Open-Meteo Archive API](https://archive-api.open-meteo.com/), aggregated into yearly features per regency (2013–2024).
- **Rice production and harvest area:** official statistics from Open Data Jabar and BPS Jawa Barat.

## Method

1. Fetch climate data from the API (with caching and retry handling) and merge it with official statistics by year and regency.
2. Split the data **chronologically** to avoid data leakage: train 2013–2021, validation 2022–2023, test 2024.
3. Standardize numeric features using training-set statistics only.
4. Train a custom `RidgeLinearRegression` class (NumPy, OOP) with gradient descent.
5. Tune the learning rate, epochs, and L2 strength with grid search on the validation set.
6. Evaluate with MSE, RMSE, MAE, and R², then analyze the loss curve, actual vs. predicted values, and residuals.
7. Test real-world climate scenarios to show how temperature and rainfall shifts affect production.

## Limitations

Harvest area explains most of the variation in production; the climate features have a smaller effect. A high R² therefore reflects the strength of harvest area as a predictor more than climate alone.

## How to run

Open the notebook in [Google Colab](https://colab.research.google.com/drive/1y3-AbfilvYfRFE81-qeacfc4X8uAyZoH) and run all cells. No API key is required.

Video presentation: https://youtu.be/Ot1BI5HGRxc

## Team

- Naufal Dzaky
- Diaz Amantajati Susilo

**Tech:** Python, NumPy, pandas, Matplotlib, Requests
