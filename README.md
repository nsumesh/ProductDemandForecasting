# Product Demand Forecasting and Stockout Predictor

# Overview
This project forecasts daily product demand and highlights potential stockout risks for a multi-store retail chain using historical sales data and exogenous features such as promotions, holidays, and macroeconomic indicators.

The goal is to assist supply chain planners and category managers in making informed decisions on inventory replenishment, demand spikes, and stockout risks during the last two weeks of August 2017 (August 16–31).

## Dataset Description
The dataset is based on the [Favorita Grocery Sales Forecasting](https://www.kaggle.com/competitions/favorita-grocery-sales-forecasting/data) Kaggle competition and includes:

- Historical daily sales per store_nbr, item_family, and date
- Store metadata: city, state, cluster, and store type
- Event calendar: holidays (local, regional, national), transferred holidays
- Oil price index as a proxy for economic activity
- Promotional flags
- Transactions (partial availability)

## Workflow 

Data Preprocessing
- Merged multiple sources (stores, oil, holidays, transactions)
- Filtered training data up to August 15, 2017

Feature Engineering (Key temporal, lag, and statistical features created):
- lag_1, lag_7: Previous day and previous week sales
- rolling_mean_7, rolling_std_7: Weekly sales patterns
- rolling_mean_30: Longer-term trends
- day, month, year, weekofyear, is_weekend, dayofweek

Model Building
- Used LightGBM Regressor with log-transformed sales
- Tuned hyperparameters manually for optimal validation RMSE
- Trained per-store-family combination and predicted demand from Aug 16–31

Forecast Inference
- Generated predictions on a filtered test set
- Re-transformed log_sales to get final predicted sales
- Created multiple granular outputs:
  - Daily forecasts per (store, family)
  - Aggregates per store
  - Aggregates per family
  - Aggregates per day

## Tableau Visualizations
- Daily Forecast Line Chart (Aug 16–31)
- Store-Level Demand Comparison
- Product Category Demand Patterns

Files used for this : 
- daily_forecast_by_store_family.csv : Daily breakdown of store sales per category
- agg_date.csv: Date-wise aggregate for time series trend
- agg_per_store.csv: Store-level forecasts
- agg_per_store_family.csv: Store & category granularity











