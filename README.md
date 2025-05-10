# Backtrader Multi-Factor Strategy with SVR

This repository implements a cross-sectional multi-factor stock selection strategy using Support Vector Regression (SVR) and Backtrader.

##  Strategy Overview

- **Rebalancing Frequency**: Every 5 trading days
- **Prediction Method**: Rolling prediction using SVR
- **Target**: Long stocks with high predicted return, short those with low predicted return
- **Input Features**: `bp`, `beta`, `market_cap`, `roe`, `turnover`
- **Target Variable**: Future momentum (next-period return)

##  Pipline
- Data source: yfinance
- Data clean: As Backtrader requires all data feed of stocks have data in each day to trigger  next(), in data cleaning process all the stock data are aligned to unified dates.
- Set commission and stamp duty rate
- Create strategy: Employ a rolling prediction approach, set the rebalancing interval 5 days, the factor data from the previous period is used as the training sample, and the resulting model is applied to the current period's factor data to generate return predictions. Based on the predicted return rankings and their signs, long and short positions are established accordingly.
- Train SVR model to predict momentum(y)
- Apply the trained model on the current period's factor data (`X`) to forecast future returns
- Rank predictions: Long top-N and short bottom-N stocks
- Execute trades at next day's open price (`open[1]`)




