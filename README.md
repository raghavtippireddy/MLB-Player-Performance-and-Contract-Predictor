# MLB-Player-Performance-and-Contract-Predictor
A predictive analytics tool that forecasts future MLB player performance and evaluates whether players are overvalued or undervalued relative to their contracts. Built with Python and machine learning regression models, this project helps surface cost-efficient talent and flag inflated contracts in Major League Baseball.

# Overview
Front offices and fans alike often ask the same question: Is this player actually worth what they're being paid? This project answers that by combining historical performance data with salary information, then training regression models to predict key performance metrics. The output is a clear comparison between expected value and actual contract cost.

# Key Features
Data Pipeline: Automated collection and cleaning of MLB player statistics and salary data from public sources (MLB Stats API, Spotrac).
Performance Prediction: Regression models (Linear Regression and Random Forest) trained to forecast metrics such as Player Efficiency Rating and Win Shares.
Contract Value Analysis: Side-by-side comparison of predicted player value vs. actual salary to identify market inefficiencies.
Visualizations: Charts and plots built with Matplotlib and Seaborn that highlight overpaid stars and hidden bargains across the league.

# Tech Stack
Language: Python 3.x
Data Handling: Pandas, NumPy, Requests
Machine Learning: scikit-learn (Linear Regression, Random Forest Regressor)
Visualization: Matplotlib, Seaborn
Data Sources: MLB Stats API, Spotrac

# Methodology
Data Collection — Pulled player stats and contract data from public APIs using the requests library.
Data Cleaning — Standardized formats, handled missing values, and merged stats and salary datasets on player identifiers using Pandas.
Feature Engineering — Selected and transformed input features (batting average, OPS, WAR, age, position, etc.) most predictive of future performance.
Model Training — Trained and compared Linear Regression and Random Forest models, evaluating performance with metrics like R² and RMSE.
Value Analysis — Translated predicted performance into expected dollar value and compared it against actual salary to flag overvalued and undervalued players.
Visualization — Built plots to surface trends, outliers, and the most cost-efficient contracts in the league.
