# USD-JPY-Trend-Prediction-Using-Technical-Indicators-and-Classical-Machine-Learning
USD/JPY Daily Trend Forecasting Framework

## Overview

The foreign exchange (Forex) market is the world's largest financial market, where exchange rates are influenced by economic conditions, monetary policy, and market sentiment. Due to the non-stationary and dynamic nature of financial markets, accurately predicting price movements remains a challenging task. This project develops a machine learning framework to forecast the next-day direction (Bullish or Bearish) of the USD/JPY currency pair using historical daily exchange rate data obtained from Yahoo Finance. The workflow combines Exploratory Data Analysis (EDA), technical indicator feature engineering, and classical machine learning to build an interpretable and reproducible forecasting model.

## Business Problem

Many Forex traders rely on subjective interpretation of technical indicators, which can lead to inconsistent trading decisions. This project investigates whether technical indicators combined with machine learning can improve the prediction of next-day USD/JPY market direction and support more objective, data-driven decision making.

## Objectives

- Collect historical daily USD/JPY (JPY=X) data from Yahoo Finance.
- Perform data cleaning and Exploratory Data Analysis (EDA).
- Generate technical indicators through feature engineering.
- Build a binary classification model to predict Bullish or Bearish market trends.
- Evaluate model performance using time-series validation.
- Identify the most influential technical indicators for trend prediction.

## Dataset and Feature Engineering

The dataset consists of daily Open, High, Low, Close, and Volume (OHLCV) data for the USD/JPY currency pair downloaded from Yahoo Finance.

Technical indicators were engineered to capture different market characteristics:

- **Trend:** Moving Averages (MA50, MA100, MA200)
- **Momentum:** Relative Strength Index (RSI)
- **Volatility:** Average True Range (ATR)

A binary target variable was created to classify whether the following trading day's closing price is higher (Bullish) or lower (Bearish) than the current day's closing price.

## Methodology

The project follows the workflow below:

**Data Collection → Data Cleaning → Exploratory Data Analysis → Feature Engineering → Target Creation → Time-Series Train/Test Split → Feature Scaling → Baseline Model (K-Nearest Neighbors) → Model Evaluation**

The baseline model is **K-Nearest Neighbors (KNN)**, providing a benchmark for evaluating predictive performance before exploring more advanced machine learning algorithms.

## Time-Series Validation

Since financial data is sequential and non-stationary, random train-test splitting and standard K-Fold cross-validation are not appropriate because they introduce look-ahead bias by allowing future observations to influence model training. This project preserves chronological order by using a time-series train-test split, ensuring that the model is evaluated only on future observations, thereby providing a more realistic assessment of its predictive performance.

## Evaluation Metrics

Model performance is assessed using:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

## Technologies

Python • Pandas • NumPy • Scikit-learn • Matplotlib • yfinance • pandas-ta • Jupyter Notebook
