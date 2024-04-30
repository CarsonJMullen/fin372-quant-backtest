# Backtesting a Crypto Timing Strategy

This repo was built as a Final Project in FIN 372 Quant Investment Management at the University of Texas at Austin, where we instructed to create a trading strategy and backtest the historical results of employing that strategy.

## Basics of Our Strategy

### Intuition/Abstract

When banks issue secondary equity offerings, we predict that this will cause panic to sell the bank’s stock due to liquidity and bank run concerns, and a coinciding rush to alternative currencies, namely Bitcoin, over the next two weeks. Our backtest takes short positions on all US bank stocks, classified by Bloomberg, on the announcement of additional equity offerings, and buys Bitcoin for the same dollar amount for a 2-week holding period. Overall, the best backtest of a 14-day holding period shows positive results, with annualized arithmetic returns of 4.792%, an annualized Sharpe ratio of 1.046, and an annualized alpha of 2.823% that is statistically significant.

### Data Sources

* Bloomberg: Pulled dates of all US bank secondary equity issuance announcements
* Python Yahoo Finance package: Pulled price and return data

### Universe

* US Equities that
    1. are in the banking industry as determined by Bloomberg
    2. are listed on Yahoo Finance
    3. announced a secondary equity offering
* Bitcoin

### Signals
Announcement of Secondary Issuances of a US Bank derived from Bloomberg. This will be instantaneous and require no time lag, so we will trade on the date announced at the adjusted close price.

### Trading Rule
Buy 6.25% of NAV in BitCoin and short 6.25% of NAV in the underlying banking stock that had the secondary issuance. Close both trades in 14 days from opening. 

We chose 6.25% because the maximum number of open trades at a time for our largest holding period was 32 (16 open and 16 close). 6.25% is the maximum percentage that would ensure that we don’t exceed $1 long, $1 short, and $1 held at any given time. 

In summary, on the announcement date of the secondary equity issuance, we will buy 6.25% of NAV in BitCoin and short 6.25% in the bank stock at the adjusted closing price, and hold each for 14 days.

### Holding Period
14 days (Also tested 7, 30, and 60 days)

### Time Period
**September 17th, 2014 - February 29th, 2024**

September 17th, 2014 was the first day that Bitcoin appeared on Yahoo Finance. This is the first day that we assume our strategy becomes viable because Bitcoin becomes well known enough to be listed on a major financial platform. Before September 17th, it is unlikely that the general public knew about decentralized financial products such as Bitcoin. Since it is impossible that a person could switch from a bank to a decentralized asset, if they didn’t know it existed we decided to start when it was first listed on Yahoo Finance.

February 29th, 2024 was the last day that we had information on Fama-French returns on the market and returns of the risk-free asset, so we decided this would be our end point. 

## File Directory

### 1. Final Report.pdf
*  Final write up fully explaining our work

### 2. pull_data.ipynb

* Pulls price and return data from yf and renames tickers in Equity Issuances file to correctly merge

### 3. constants.py

* Holds constant information used in multiple files

### 4. sbf_data_processor.ipynb
* Loads and merges price and signal data
* Provides universe of securities and signals for each date

### 5. portfolio_db.ipynb
* Tracks current portfolio and account balance sheet
* Keeps records of all trades/transactions
* Keeps history of NAV and margin requirements

### 6. sbf_trading_rule.ipynb
* Decides which trades to make given a universe of securities, signals, and current portfolio

### 7. backtest_executor.ipynb
* "Submits" order either hypothetically using historical data or live to a brokerage
* Calculates or retrieves transaction prices accounting for any liquidity costs

### 8. backtest_statistician.ipynb
* Looks at results of backtest or live trading and computes statistics ($\alpha$ etc) as well as informative plots (e.g. NAV and margin over time)

### 9. Output (Folder)
* Shows account history, backtest stats (multi-factor regression), plot of returns, and the specific trades made for each holding period

### 10. regression-comp.xslx
* Directly compares backtest_stats.csv of all four holding periods and includes t-stat values
