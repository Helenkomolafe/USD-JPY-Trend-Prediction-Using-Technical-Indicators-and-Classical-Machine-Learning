# USD/JPY Trend Prediction Using Technical Indicators and Classical Machine Learning (2000–2026)

## Project Overview

This project develops a classical machine learning model for predicting the **next-day direction of the USD/JPY exchange rate** using historical daily price data and technical indicators.

The objective is to determine whether USD/JPY will be **Bullish (1)** or **Bearish (0)** on the following trading day. A **Random Forest Classifier** was trained using technical indicators capturing momentum, volatility, and trend information.

The project also evaluates the model through a historical backtest to assess whether the generated signals could improve trading performance compared with a Buy & Hold strategy.

---

## Dataset

- **Currency Pair:** USD/JPY
- **Frequency:** Daily
- **Period:** 2000–2026
- **Total Observations:** 6,629
- **Training Observations:** 5,303
- **Testing Observations:** 1,326
- **Training Period:** 2000-10-13 to 2021-03-22
- **Testing Period:** 2021-03-23 to 2026-04-28

The target variable is based on whether the next day's average price is higher or lower than the current day's average price.

- **Bullish = 1**
- **Bearish = 0**

### Class Distribution

| Class | Proportion |
|---|---:|
| Bullish (1) | 51.70% |
| Bearish (0) | 48.30% |

---

## Features

The model uses eight technical features:

1. RSI
2. ATR
3. Dist_MA50
4. Dist_MA100
5. Dist_MA200
6. slopeMA50
7. slopeMA100
8. slopeMA200

These features represent momentum, volatility, price position relative to moving averages, and trend direction.

---

## Methodology

The project follows a chronological train-test approach to preserve the time-series structure of the financial data.

## Workflow

```text
Historical USD/JPY Data
          ↓
Data Cleaning
          ↓
Technical Indicator Calculation
          ↓
Feature Engineering
          ↓
Target Creation
          ↓
Chronological Train/Test Split
          ↓
Random Forest Classification
          ↓
Model Evaluation
          ↓
Trading Strategy Backtest

```

No random shuffling was used when splitting the data, helping to prevent future observations from being used to train the model.

------

## Model Performance

The Random Forest achieved:

| Metric                    |                      Result |
| ------------------------- | --------------------------: |
| Accuracy                  |                  **55.20%** |
| ROC-AUC                   |                  **52.74%** |
| Test Observations         |                   **1,326** |
| Majority-Class Baseline   |                  **56.41%** |
| Improvement over Baseline | **-1.21 percentage points** |

 
## Classification Report


| Class                | Precision | Recall | F1-Score |
| -------------------- | --------: | -----: | -------: |
| Bearish              |      0.48 |   0.32 |     0.38 |
| Bullish              |      0.58 |   0.73 |     0.65 |
| **Overall Accuracy** |           |        | **0.55** |

The model correctly identified approximately **73.3% of bullish observations,** but only **32.1% of bearish observations,** indicating a noticeable tendency toward predicting the bullish class.

## Confusion Matrix

The confusion matrix shows the number of correct and incorrect predictions made by the Random Forest model.

| Actual / Predicted | Bearish | Bullish |
|---|---:|---:|
| **Bearish** | 184 | 394 |
| **Bullish** | 200 | 548 |
               

## Benchmark Comparison

The majority-class baseline provides an important benchmark for evaluating the model.

| Model                   |   Accuracy |
| ----------------------- | ---------: |
| Majority-Class Baseline | **56.41%** |
| Random Forest           | **55.20%** |
| Difference              | **-1.21%** |

The Random Forest did not outperform the simple majority-class prediction.

Therefore, the model's classification performance should be interpreted cautiously.  

---
## Feature Importance

The Random Forest identified the following features as the most influential:

| Feature    | Importance |
| ---------- | ---------: |
| RSI        |     18.30% |
| Dist_MA50  |     15.93% |
| slopeMA200 |     12.53% |
| Dist_MA100 |     12.24% |
| slopeMA100 |     11.44% |
| ATR        |     10.42% |
| slopeMA50  |      9.97% |
| Dist_MA200 |      9.17% |

**RSI** was the most important feature, followed by the distance from the 50-day moving average and the slope of the 200-day moving average.

Feature importance indicates which variables the **Random Forest relied on most** when making predictions. However, a higher feature importance does **not mean that an individual indicator independently predicts future prices**.

--
## Backtesting Results

The model's trading signals were evaluated using historical backtesting.
| Metric                | Buy & Hold | Long-Only Strategy | Long-Short Strategy |
| --------------------- | ---------: | -----------------: | ------------------: |
| Total Return          |     46.60% |             58.27% |          **69.03%** |
| Annualized Return     |      7.54% |              9.12% |          **10.49%** |
| Annualized Volatility |      8.19% |          **6.81%** |               8.18% |
| Sharpe Ratio          |       0.92 |           **1.34** |                1.28 |
| Maximum Drawdown      |    -14.53% |         **-9.57%** |              -9.58% |
| Win Rate              |     56.42% |         **58.19%** |              55.21% |
The backtest produced stronger historical returns and lower maximum drawdown for the model-based strategies compared with Buy & Hold.

However, historical backtest performance does **not guarantee future profitability.**

----

## Final Prediction Example

Using information available up to **April 28, 2026,** the model predicted that USD/JPY would be:

**Bullish for April 29, 2026.**

The subsequent target observation was also *Bullish,** making this prediction correct.

This demonstrates how the trained model can generate a next-day directional signal when the required technical features are available.

## Key Findings

The project demonstrates that classical machine learning can be applied to USD/JPY trend classification using technical indicators.

However, the Random Forest achieved:

- **55.20% test accuracy**
- **52.74% ROC-AUC**
- **56.41% majority-class baseline**

The model therefore performed **1.21 percentage points below the baseline.**

Its ability to distinguish between bullish and bearish outcomes was limited, as indicated by the ROC-AUC of 52.74%.

The model also showed a clear tendency toward bullish predictions, correctly identifying approximately **73.3% of bullish observations but only 32.1% of bearish observations.**

## Final Findings and Conclusion

The results indicate that the selected technical indicators provided **limited predictive information for next-day USD/JPY direction** during the test period.

**RSI** was the most important feature at approximately **18.3%,** followed by **Dist_MA50 at 15.9%** and **slopeMA200 at 12.5%. ATR** also contributed meaningfully at approximately **10.42%.**

However, feature importance should not be interpreted as proof that these indicators independently predict future prices.

Overall, the Random Forest **did not outperform the majority-class baseline,** suggesting that the current technical-indicator configuration is insufficient for reliable next-day directional prediction.

-----
The project nevertheless demonstrates a complete machine learning workflow for a financial forecasting problem, including:

- Data preparation
- Technical indicator calculation
- Feature engineering
- Target creation
- Chronological train-test splitting
- Random Forest classification
- Model evaluation
- Feature importance analysis
- Trading strategy backtesting

--------
## Deployment

The trained Random Forest model could be deployed for real-time USD/JPY trend prediction by connecting it to a live forex data source.

A potential deployment pipeline would be:

Live USD/JPY Data
        ↓
Data Processing
        ↓
Technical Indicators
        ↓
Feature Engineering
        ↓
Trained Random Forest
        ↓
Bullish / Bearish Prediction
        ↓
Prediction Monitoring

New market data would be processed using the **same technical indicators and feature-engineering steps used during training.** The model would then generate either:

- **Bullish (1)**

- **Bearish (0)**

However, based on the final test results of **55.20% accuracy versus a 56.41% baseline,** deployment as a production trading system is not recommended at this stage.

Further model improvement and validation are required before real-world use.

------
## Limitations

Several limitations should be considered:

- Technical indicators alone may not contain sufficient information for reliable next-day FX prediction.
- The model shows a noticeable bias toward bullish predictions.
- Test accuracy did not outperform the majority-class baseline.
- The ROC-AUC indicates limited class-separation ability.
- Historical backtesting does not guarantee future performance.
- Transaction costs and spreads may reduce actual trading returns.
- Slippage and market liquidity were not fully represented.
- Forex markets are influenced by macroeconomic events, interest rates, monetary policy, geopolitical developments, and market      sentiment.
- These external factors were not included in the current feature set.

---------
## Future Improvements

Potential improvements include:

1. Adding macroeconomic and fundamental variables.
2. Incorporating additional volatility and momentum indicators.
3. Testing Gradient Boosting and XGBoost models.
4. Experimenting with alternative ensemble methods.
5. Optimizing classification thresholds.
6. Addressing the model's bullish prediction bias.
7. Adding market-regime features.
8. Testing alternative target definitions.
9. Conducting additional out-of-sample validation.
10. Incorporating transaction costs and slippage into the backtest.
11. Comparing machine learning models with simpler statistical benchmarks.
12. Exploring additional market information such as interest-rate differentials and economic indicators.

## Technologies Used
- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Scikit-learn**
- **pandas-ta**
- **Jupyter Notebook**
- **Yahoo Finance historical market data**

## Project Structure

```text
USDJPY-Trend-Prediction/
│
├── data/
│   └── USDJPY historical data
│
├── notebooks/
│   └── USDJPY_Trend_Prediction.ipynb
│
├── README.md
│
└── requirements.txt
```

---

## Conclusion

This project demonstrates the practical application of **classical machine learning, technical analysis, time-series modelling, and backtesting** to the USD/JPY foreign exchange market.

Although the Random Forest generated some useful trading signals and the backtest produced encouraging historical results, its **55.20% test accuracy and 52.74% ROC-AUC indicate limited predictive power for next-day USD/JPY direction.**

Importantly, the model did not outperform the **56.41% majority-class baseline.**

The findings highlight an important lesson in financial machine learning: a model should be evaluated against a meaningful baseline and tested on unseen chronological data rather than relying solely on accuracy or historical trading returns.

Future work will focus on improving feature engineering, incorporating additional market information, testing alternative models, and conducting more rigorous validation before any real-world deployment.





