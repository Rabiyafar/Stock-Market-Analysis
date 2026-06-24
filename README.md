# Stock Price Direction Prediction (BBCA.JK)
A complete 10‑year machine learning pipeline using Random Forest, XGBoost, technical indicators, and threshold tuning.
# Project Summary
This project predicts next‑day stock movement (Up/Down) for BBCA.JK using:
10 years of OHLCV data
Technical indicators (RSI, MACD, Bollinger Bands, Volatility)
Momentum features (lagged returns)
Volume‑based features
Random Forest & XGBoost models
Threshold tuning to maximize recall for Up days
Feature importance analysis
F1‑score optimization
The project includes three versions of the model, showing a clear progression from a baseline model to a fully engineered XGBoost pipeline.


# Complete Workflow
This README documents the entire process, including all three code versions.
1. Data Loading & Cleaning
Load 10‑year dataset
Parse dates, set index
Remove suspicious rows where Volume = 0 and OHLC are identical
Code
df = df[df['Volume'] != 0]
2. Version 1 — Baseline Random Forest
File: 01_baseline_random_forest.ipynb
Goal
Build a simple baseline model using minimal features.
Features
MA5
MA10
Return_1
Return_2
Rolling_Std (20‑day volatility)
Target
Code
Target = 1 if next day's return > 0 else 0
Results
Accuracy ≈ 0.54
Recall for Up ≈ 0.05
Model predicts “Down” too often
Why this version matters
It establishes a baseline and shows that simple features are not enough.
3. Version 2 — Advanced Feature Engineering + Threshold Tuning
File: 02_feature_engineering_and_threshold_tuning.ipynb
Added Features
Momentum
Return_1
Return_2
Return_3
Volatility
Volatility_5
Volatility_10
Trend Indicators
RSI (14)
MACD
MACD Signal
Bollinger Bands
BB_Mid
BB_Upper
BB_Lower
Volume Features
Volume_Change
Volume_MA5
Volume_MA10
Results
Accuracy ≈ 0.52
Recall for Up improves
Feature importance shows momentum + volume dominate
Threshold Tuning (Version 2)
Default threshold = 0.5
But financial models often need high recall for Up.
We sweep thresholds from 0.1 to 0.9:
Code
thresholds = np.arange(0.1, 0.9, 0.01)
Best threshold ≈ 0.21
Results
Recall for Up ≈ 1.00
Precision drops (expected)
Good for trading strategies that prioritize catching Up days
4. Version 3 — Random Forest + XGBoost Pipeline
File: 03_random_forest_vs_xgboost.ipynb
This is the cleanest and most complete version.
Includes
Zero‑volume row removal
Full technical indicators
Proper NaN/inf cleaning
Random Forest + XGBoost
Threshold tuning for both
F1 vs threshold plot
XGBoost Model
Parameters
Code
params = {
    'objective': 'binary:logistic',
    'eval_metric': 'logloss',
    'eta': 0.05,
    'max_depth': 4,
    'subsample': 0.8,
    'colsample_bytree': 0.8,
    'seed': 42
}
Results
Default threshold accuracy ≈ 0.52
Best threshold ≈ 0.19
Recall for Up ≈ 1.00
XGBoost slightly outperforms Random Forest
# Feature Importance (RF + XGB)
Top features across models:
RSI
Return_1
Volume_Change
Volatility_10
MACD
Return_3
Momentum + volume + volatility dominate.
# F1 vs Threshold Plot
Blue = Random Forest
Red = XGBoost
Vertical lines = best thresholds
Shows how lowering threshold increases recall.
# Key Insights
Removing zero‑volume rows improves indicator quality
Feature engineering significantly improves signal
Threshold tuning is essential for financial ML
XGBoost performs slightly better than Random Forest
High recall for Up days is achievable
Accuracy is NOT the right metric for trading models
# Next Steps
Add LSTM/GRU deep learning models
Add macroeconomic features
Try walk‑forward validation
Build a backtesting engine
Optimize thresholds using profit instead of F1

# Author
Rabiya Farheen MSc Data Science, Technical University of Braunschweig, Germany
