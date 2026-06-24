Stock Price Movement Prediction (BBCA.JK)
10‑Year Analysis • Feature Engineering • Technical Indicators • Random Forest Classification

Project Summary
This project analyzes 10 years of daily stock data for BBCA.JK (Bank Central Asia) and builds a machine‑learning model to predict whether the next day’s return will be Up (1) or Down (0).
The workflow includes:
Data cleaning & anomaly detection
Return calculations
Technical indicator engineering
Visualization of price trends & volatility
Machine learning modeling (Random Forest)
Threshold tuning for trading‑oriented recall
Insights on model behavior & financial interpretation
The goal is direction prediction, not price prediction — a more realistic task for trading strategies.

Dataset
File: Bank_Stock_Price_10Y.csv
Period: 2014 → 2024
Rows: 2483
Columns: Open, High, Low, Close, Adj Close, Volume
Data Cleaning
No missing values
71 rows had Volume = 0 with identical OHLC values → removed
Final dataset: 2412 rows

Exploratory Data Analysis

Adjusted Close Price (2014–2024)
Shows long‑term upward trend with periodic corrections.

Distribution of Daily Returns
Near‑normal distribution
Most returns fall between –2% and +2%

20‑Day Rolling Volatility
Volatility spikes during:
2015–2016
2019
COVID‑19 (2020)
These align with global macroeconomic stress.

Feature Engineering
✔ Price‑Based Features
MA5, MA10
Return_1, Return_2, Return_3
Volatility_5, Volatility_10
✔ Technical Indicators
RSI (14‑day)
MACD & MACD Signal
Bollinger Bands (Upper, Lower, Mid)
✔ Volume Features
Volume Change (%)
Volume_MA5
Volume_MA10
✔ Target Variable
Code
Target = 1 if next day's return > 0 else 0

Visualizations
🔹 Moving Averages
MA5 and MA10 smooth short‑term noise and highlight trend direction.
🔹 Bollinger Bands
Show volatility expansion/contraction and price extremes.
 
Machine Learning Model
Model
RandomForestClassifier
Baseline
With class weights
With expanded feature set
Train/Test Split
Time‑series aware:
80% → Train
20% → Test

Baseline Performance
Metric	Value
Accuracy	~0.54
Recall (Up)	very low
Precision (Up)	moderate


The model predicts Down most of the time.

Improved Feature Set Performance
After adding RSI, MACD, Bollinger Bands, Volume features:
Accuracy: 0.52
Recall (Up): 0.22
Precision (Up): 0.44
Better than baseline, but still limited — daily stock direction is inherently noisy.

Threshold Tuning (Trading Perspective)
Lowering the probability threshold from 0.5 → 0.3:
Recall (Up): 0.97 → captures almost all Up days
Accuracy drops → expected
Model predicts Up most of the time
Why This Matters
For trading, catching Up days is often more important than accuracy.
False positives can be managed with stop‑loss.

Feature Importance
Top contributors:
Return_1
Return_2
MA5
MA10
Volatility indicators
Momentum and short‑term trend dominate predictive power.

Key Insights
Daily stock direction is extremely hard to predict
Feature engineering helps, but only slightly
Threshold tuning is powerful for trading strategies
Accuracy is misleading — focus on recall & profitability

Future Improvements
Add XGBoost / LightGBM - (attempt made and is added to git)
Add regime detection (bull/bear phases)
Add sentiment features (news, social media)
Use walk‑forward validation
Build a backtesting engine to evaluate actual returns

Conclusion
This project demonstrates a complete end‑to‑end workflow for stock movement prediction:
Clean data
Engineer features
Visualize trends
Train ML models
Tune thresholds
Interpret results
While accuracy remains modest, the model provides useful trading insights, especially when optimized for high recall of profitable Up days.

Author
Rabiya Farheen
MSc Data Science, Technical University of Braunschweig, Germany
