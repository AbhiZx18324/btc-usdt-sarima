# BTC/USDT Market Predictive Model

This repository contains the implementation of a predictive model using **SARIMA (Seasonal AutoRegressive Integrated Moving Average)** for the BTC/USDT trading pair. The model forecasts future Bitcoin prices based on historical data, and a trading strategy is devised using the predictions.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Data Preprocessing](#data-preprocessing)
3. [Modeling Approach](#modeling-approach)
4. [Evaluation](#evaluation)
5. [Trading Strategy](#trading-strategy)
6. [Backtesting Results](#backtesting-results)

## Project Overview
This project focuses on using time series analysis to predict Bitcoin's future closing prices, leveraging the SARIMA model. The model has been trained and tested on BTC/USDT data from **January 1, 2018, to January 31, 2022** with a time interval of 6 hours.

The project also includes a simple trading strategy based on moving averages and evaluates its performance using backtesting.

## Data Preprocessing
- **Dataset**: The model uses the **OHLC** (Open, High, Low, Close) data for BTC/USDT.
- **Target Variable**: We focus on the **closing price** of Bitcoin as it's often used for predicting future price movements.
- **Stationarity Check**: The **Dickey-Fuller test** was used to ensure stationarity. After taking the first difference, stationarity was achieved.
- **Seasonality**: A seasonal differencing with a period of 24 (6 days in 6-hour intervals) was applied to handle seasonality.

### Key Preprocessing Steps:
1. **First differencing** to stabilize trends.
2. **Box-Cox transformation** to stabilize variance.
3. **Seasonal differencing** with `s = 24`.

## Modeling Approach
The SARIMA model used in this project is tuned using **ACF** and **PACF** plots. A grid search was applied to find the best parameters based on **AIC** (Akaike Information Criterion). The optimal parameters found are:

- **p=2, d=1, q=4**
- **P=0, D=1, Q=1, s=24**

The model was evaluated using **20-fold time-aware cross-validation**, with **Mean Absolute Percentage Error (MAPE)** as the evaluation metric.

## Evaluation
- **Cross-Validation Results**: The average MAPE across 20 folds is **22.38%**.
- **Forecasting**: The model predicts future Bitcoin prices based on the historical data provided.

## Trading Strategy
The trading strategy is based on a simple moving average crossover approach:
- **Buy** when the 78-hour moving average crosses above the 144-hour moving average.
- **Sell** when the 78-hour moving average crosses below the 144-hour moving average.

## Backtesting Results
Backtesting of the strategy on historical data showed the following performance metrics:
- **Sharpe Ratio**: 1.1299
- **Annualized Returns**: 10.16%
- **Maximum Drawdown**: 7.92%

Additionally, a risk management strategy was employed using a stop loss of 2% and a 2:1 reward-risk ratio.

