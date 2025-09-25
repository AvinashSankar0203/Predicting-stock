# 📉 Tesla (TSLA) Stock Price Prediction: Linear Regression Analysis

This project explores the feasibility of using a simple **Linear Regression** model to predict the daily closing price of Tesla (TSLA) stock, focusing on the highly volatile period of January 2024.

The core finding of this analysis is the **critical inadequacy of the linear model** for time-series financial data, providing valuable insights into the necessary complexity for accurate market prediction.

## 🎯 Project Goal

To build and evaluate a Linear Regression model using 2023 historical data and predict the stock's performance for January 2024.

## 📊 Data & Features

The model was trained on daily stock data from January 2023 to December 2023.

### Features Used (Input Variables)

The model relied exclusively on intraday movements and volume changes, intentionally excluding lagged price data (i.e., yesterday's close) to test the strength of volatility-based features:

1.  **Open-Close Difference:** Measures daily momentum.
2.  **High-Low Range:** Measures daily volatility.
3.  **Volume Change Percentage:** Measures changes in trading activity.
4.  **Squared High-Low Range:** A polynomial feature introduced to capture the non-linear effect of extreme volatility.

## 🔍 Model Evaluation Results

The model was evaluated on a test set (20% of 2023 data). The metrics confirm the model's complete failure.

| Metric | Value | Interpretation |
| :--- | :--- | :--- |
| **R-squared ($R^2$)** | **-1.86** | The model performs **worse than guessing the historical average price** every day. This violates the core assumption of linear regression for this data. |
| **Mean Squared Error (MSE)** | **1067.74** | A very high error value. |
| **Root Mean Squared Error (RMSE)** | **~$32.68** | The average prediction was off by approximately **$32.68** per share, rendering the predictions useless for trading. |

## 💡 Critical Analysis: Why the Model Failed

The failure of the Linear Regression model is primarily due to two factors: **ignoring time-dependency** and **improper feature selection**.

### 1. Financial Flaw (Time Series Dependency)
* **Stock price is sequential:** The price of a stock today is overwhelmingly determined by its price yesterday (momentum and trend). By only using intraday features, the model lacked any historical context, resulting in highly erratic and directionally incorrect predictions (see plots below).

### 2. Machine Learning Flaw (Linearity)
* **Market is Non-Linear:** The relationship between volatility, volume, and future price is complex and non-linear, driven by human sentiment and global events. A linear model cannot capture these dynamics. The model merely reacted to daily noise (High/Low swings) without learning the sustained trend.

## 📈 Prediction Visualization

The charts illustrate the model’s struggle to capture market reality.

### 1. Predicted vs. Actual (Test Set)
The model's predictions (red dashed line) show random noise, failing to mimic the actual price trend (blue solid line).



### 2. Final Prediction (January 2024)
The prediction for the unseen data shows that the linear model essentially produced a **flat line with minimal, random deviations**, proving the features used were insufficient to determine market direction.



## 🚀 Next Steps and Improvements

The project's key takeaway is the need to move to specialized time series methods.

1.  **Feature Correction (Immediate Fix):** Add the **previous day's closing price** (`Close.shift(1)`) as a primary feature to introduce time dependency.
2.  **Model Upgrade:** Transition from Linear Regression to **Recurrent Neural Networks (RNNs)**, specifically **Long Short-Term Memory (LSTM)** models, which are built to process and remember sequences of data.
3.  **Feature Engineering:** Incorporate complex **Technical Indicators** (e.g., Simple Moving Averages, RSI) to provide the model with explicit trend and momentum signals.

---

### **Project Structure**

* `stock_prediction.py`: Main Python script for data fetching, cleaning, feature engineering, model training, and prediction.
* `README.md`: This file.
* `/images/`: Directory containing all generated charts.
