### Backtesting a Crypto Timing Strategy

This repo was built as a Final Project in FIN 372 Quant Investment Management at the University of Texas at Austin, where we instructed to create a trading strategy and backtest the historical results of employing that strategy.

### Basics of Our Strategy

## Data Sources

* Bloomberg: Pulled dates of all US bank secondary equity issuance announcements
* Python Yahoo Finance package: Pulled price and return data

## Universe

* US Equities that
    1. are in the banking industry as determined by Bloomberg
    2. are listed on Yahoo Finance
    3. announced a secondary equity offering
* Bitcoin

## Signals
Announcement of Secondary Issuances of a US Bank derived from Bloomberg. This will be instantaneous and require no time lag, so we will trade on the date announced at the adjusted close price.

## Trading Rule
Buy 6.25% of NAV in BitCoin and short 6.25% of NAV in the underlying banking stock that had the secondary issuance. Close both trades in 14 days from opening. 

We chose 6.25% because the maximum number of open trades at a time for our largest holding period was 32 (16 open and 16 close). 6.25% is the maximum percentage that would ensure that we don’t exceed $1 long, $1 short, and $1 held at any given time. 

In summary, on the announcement date of the secondary equity issuance, we will buy 6.25% of NAV in BitCoin and short 6.25% in the bank stock at the adjusted closing price, and hold each for 14 days.

## Holding Period
14 days (Also tested 7, 30, and 60 days)

## Time Period
September 17th, 2014 - February 29th, 2024

September 17th, 2014 was the first day that Bitcoin appeared on Yahoo Finance. This is the first day that we assume our strategy becomes viable because Bitcoin becomes well known enough to be listed on a major financial platform. Before September 17th, it is unlikely that the general public knew about decentralized financial products such as Bitcoin. Since it is impossible that a person could switch from a bank to a decentralized asset, if they didn’t know it existed we decided to start when it was first listed on Yahoo Finance.

February 29th, 2024 was the last day that we had information on Fama-French returns on the market and returns of the risk-free asset, so we decided this would be our end point. 

### File Directory

