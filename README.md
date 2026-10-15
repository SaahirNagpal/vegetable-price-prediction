# Vegetable Price Prediction using Linear Regression

## What it does

- Predicts tomorrow's modal price (Rs/quintal) for 5 vegetables across 5 markets (25 price series)
- Vegetables: Tomato, Onion, Potato, Brinjal, Cauliflower
- Markets: Pune, Azadpur (Delhi), Bangalore, Lucknow, Kolkata
- Data: 35,075 rows, Jan 2022 to Dec 2025

## How it works

1. Clean the data
2. Build features from past days only (lag prices, rolling averages, arrivals, time of year) to avoid data leakage
3. Split by date: first 80% to train, last 20% to test (no shuffling)
4. Train Linear Regression and Ridge Regression, and compare with a naive baseline (tomorrow = today)

## Results

| Model | MAE (Rs) | RMSE (Rs) | MAPE (%) | R² |
|---|---|---|---|---|
| Naive (yesterday's price) | 26.019 | 34.465 | 1.035 | 0.998 |
| **Linear Regression** | **25.172** | **33.429** | **1.001** | 0.998 |
| Ridge (alpha 10) | 25.634 | 34.144 | 1.019 | 0.998 |

Linear Regression has an average error of about 1% of the price. It is only about 3% better than the naive baseline, because one-day-ahead prices change very slowly. The high R² (0.998) is also not very meaningful for the same reason.

## Files

| File | Description |
|---|---|
| `vegetable_price_prediction.ipynb` | Main notebook (runs on Google Colab) |
| `mandi_prices_dataset.csv` | Synthetic dataset |
| `veg_price_linreg.joblib` | Saved trained model |
| `Vegetable_Price_Prediction_Report.docx` | Full project report |

## How to run

1. Open the notebook in Google Colab
2. Upload `mandi_prices_dataset.csv` (set `DATA_SOURCE` to the upload option)
3. Run all cells

To try real data, use an Agmarknet or data.gov.in CSV instead. The cleaning code matches column names loosely, so it should work with few changes.

## Tools

Python, pandas, NumPy, scikit-learn, matplotlib, seaborn, joblib

## Limitations and future work

- Synthetic data, one-day-ahead prediction only, single train-test split
- Next steps: use real data, add weather and festival features, try Random Forest / XGBoost, and predict a week ahead
