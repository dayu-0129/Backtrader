# 1 Backtrader Multi-Factor Strategy with SVR

This repository contains two trading strategy implementations using Backtrader: a cross-sectional multi-factor stock selection strategy based on Support Vector Regression (SVR), and a technical indicator-based strategy using MACD crossover signals.


##  Strategy Overview

- **Rebalancing Frequency**: Every 5 trading days
- **Prediction Method**: Rolling prediction using SVR
- **Target**: Long stocks with high predicted return, short those with low predicted return
- **Input Features**: `bp`, `beta`, `market_cap`, `roe`, `turnover`
- **Target Variable**: Future momentum (next-period return)

##  Pipline
- Data source: yfinance(data can be downloaded from:https://drive.google.com/file/d/1-vrhIPlpXU-fY6Wt3UzhDOgun9UGlxfX/view?usp=drive_link)
- Data clean: As Backtrader requires all data feed of stocks have data in each day to trigger  next(), in data cleaning process all the stock data are aligned to unified dates.
- Set commission and stamp duty rate
- Create strategy: Employ a rolling prediction approach, set the rebalancing interval 5 days, the factor data from the previous period is used as the training sample, and the resulting model is applied to the current period's factor data to generate return predictions. Based on the predicted return rankings and their signs, long and short positions are established accordingly.
- Train SVR model to predict momentum(y)
- Apply the trained model on the current period's factor data (`X`) to forecast future returns
- Rank predictions: Long top-N and short bottom-N stocks
- Execute trades at next day's open price (`open[1]`)

## Results
![image](https://github.com/user-attachments/assets/c446f079-5237-42ab-9872-1eda417bad88)
![image](https://github.com/user-attachments/assets/c573b5d0-2c0b-4042-b4f0-0c81a38be701)


# 2 MACD-Based Trading Strategy (Backtrader)

 MACD crossover strategy implemented using Backtrader

##  Strategy Overview

- **Indicator Used**: MACD with Signal Line
- **Buy Signal**: MACD line crosses above the Signal line (bullish crossover)
- **Sell Signal**: Price moves ±10% from buy price
- **Capital**: 10,000
- **Position Sizing**: Fixed stake of 100 units

##  Indicators

- **MACD**: Difference between 12-period EMA and 26-period EMA
- **Signal**: 9-period EMA of MACD
- **MACD Histogram**: Visual representation of MACD - Signal

##  Logic

1. When not in position:
   - Check for MACD crossover: if MACD crosses above signal → **buy**
2. When holding a position:
   - If price rises or drops by more than 10% from entry → **sell**
## Results
![image](https://github.com/user-attachments/assets/4318274a-f059-4ae8-ac22-c8c582e8e090)





