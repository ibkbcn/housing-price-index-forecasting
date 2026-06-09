# Housing Price Index Forecasting

A comparison of forecasting models on the Housing Price Index (HPI) for new-build homes in Catalonia. The goal: take a real time series and see which model predicts its evolution best, from classic methods to machine learning.

## About the data

The data is the HPI published by the Spanish General Council of Notaries, based on actual public deeds. I keep only new-build homes in Catalonia, at a quarterly frequency and with 2007 as the reference year. That's 72 observations in total, split 80/20 between training (58) and test (14).

The series shows two clear cycles: the 2008 crisis drop and the recovery that followed. There's no strong seasonality, and the Dickey-Fuller test confirms the series is non-stationary (p-value > 0.05).

## The models

- **Deterministic:** linear trend and Holt's exponential smoothing
- **Stochastic:** ARIMA (via `auto.arima`) and ETS
- **Machine learning:** XGBoost, building a lag matrix (n=4) to give it the temporal context it lacks on its own

## Results

| Model    | RMSE  | MAE   | MSE     |
|----------|-------|-------|---------|
| Holt     | 14.69 | 12.19 | 215.72  |
| ARIMA    | 12.24 | 10.03 | 149.72  |
| ETS      | 14.69 | 12.19 | 215.72  |
| XGBoost  | 44.41 | 41.34 | 1972.46 |

ARIMA(0,2,1) came out the most accurate. Holt and ETS landed very close together, and XGBoost fell clearly behind: with so little data, it had no room to learn.

## Takeaway

The interesting part is that the simplest model won. In a real-world setting I'd go with ARIMA, not just because it's more accurate but because it's far cheaper to train and maintain than XGBoost. 

## Stack

R · ARIMA · ETS · XGBoost 

*Forecasting course project. MSc in Data Science, La Salle - URL (2025). With Marc Fort.*
