# MLB Player Performance and Contract Predictor

A Moneyball-style analysis that predicts MLB player salaries from on-field performance to identify undervalued and overpaid players, then finds cheaper, statistically similar replacements.

## Overview

Front offices and fans often ask the same question: is this player worth what he's being paid? This project answers it in three stages:

1. Explore which team-level batting metrics are most closely tied to winning.
2. Train regression models to predict a hitter's next-season salary from his current-season stats, then compare predicted and actual salary to flag undervalued and overpaid players.
3. Use nearest-neighbor search on batting, fielding, and pitching stats to recommend similar players who could replace an expensive or aging one.

## Data

All data comes from the [Lahman Baseball Database](https://sabr.org/lahman-database/):

- **Teams:** season-level team statistics, 1973 to 2022, excluding the strike- and pandemic-shortened 1981, 1994, 1995, and 2020 seasons
- **Batting, Fielding, Pitching:** player-season statistics
- **Salaries:** player salaries, 1985 to 2016

## Project Structure

| Notebook | Focus |
|---|---|
| `MoneyballPart1.ipynb` | Team-level exploratory analysis: derived batting average, on-base percentage, and slugging percentage; interactive team performance trends; correlation heatmap against winning |
| `MoneyballPart2.ipynb` | Salary prediction and undervalued-player ranking |
| `MoneyballPart3.ipynb` | Player similarity search with K-Nearest Neighbors and PCA visualization |

## Methodology

**Data preparation**
- Combined multiple stints (a player traded mid-season) into one row per player-season.
- Filtered out player-seasons with fewer than 130 at-bats to reduce noise from small samples.
- Engineered features including batting average, on-base percentage, slugging percentage, seasons played, and arbitration and free-agent eligibility.

**Salary prediction**
- Paired each season's batting stats with the player's salary from the following year, so the model predicts future pay from past performance rather than describing current pay.
- Log-transformed salary to correct a heavy right skew, and scaled input features with MinMaxScaler.
- Trained and compared Linear Regression, Decision Tree, Random Forest, and a neural network (MLPRegressor) on an 80/20 train-test split.

**Undervalued-player analysis**
- Converted the gap between predicted and actual log salary into a predicted-to-actual salary ratio and ranked players by it to surface the most undervalued and overpaid contracts.

**Replacement search**
- Merged batting, fielding (with one-hot encoded positions), and pitching stats, normalized counting stats by games played, and kept each player's most recent season from 2019 onward.
- Standardized all features and used K-Nearest Neighbors to find the players most similar to a chosen player.
- Used PCA to project players into two dimensions (batting and fielding vs. pitching) to visualize how they group.

## Results

Salary prediction on the 20% held-out test set (target: log10 salary):

| Model | R² | MSE |
|---|---|---|
| Linear Regression | n/a | 0.130 |
| Decision Tree (max depth 3) | 0.544 | 0.146 |
| Random Forest (max depth 3) | 0.569 | 0.138 |
| Neural Network (MLPRegressor) | 0.646 | 0.113 |

The neural network performed best, explaining about 65% of the variance in next-season log salary.

## Limitations and Next Steps

- The train-test split is random rather than time-based; validating on later seasons only would better reflect real forecasting.
- The salary model uses batting statistics only; adding pitching, fielding, and advanced metrics would extend it to all players.
- Salary data ends in 2016, so contract comparisons do not reflect the current market.

## Tech Stack

- **Language:** Python 3
- **Data:** Pandas, NumPy
- **Machine Learning:** scikit-learn (Linear Regression, Decision Tree, Random Forest, MLPRegressor, K-Nearest Neighbors, PCA)
- **Visualization:** Matplotlib, Seaborn, ipywidgets, mplcursors

## Running the Notebooks

Open the notebooks in Jupyter or Google Colab and run them in order. Data loads directly from hosted CSV files. Install dependencies with:

pip install pandas numpy scikit-learn matplotlib seaborn ipywidgets mplcursors
