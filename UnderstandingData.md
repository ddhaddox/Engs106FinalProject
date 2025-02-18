## Dataset Description

This dataset contains historic data for the daily ten minute closing auction on the NASDAQ stock exchange.

The ML challenge is to predict the future price movements of stocks relative to the price future price movement of a synthetic index composed of NASDAQ-listed stocks.

Relevant notebook for understanding trading at the close of day and our df: https://www.kaggle.com/code/tomforbes/optiver-trading-at-the-close-introduction

### Data Columns

Here are the columns in the training CSV (df)

1. **stock_id**: 
    A unique identifier for the stock. Not all stock IDs exist in every time bucket.
2. **date_id**: A unique identifier for the date. Date IDs are sequential & consistent across all stocks.
3. **imbalance_size**: The amount unmatched at the current reference price (in USD).
4. **imbalance_buy_sell_flag**: An indicator reflecting the direction of auction imbalance.
buy-side imbalance; 1
sell-side imbalance; -1
no imbalance; 0
5. **reference_price**: The price at which paired shares are maximized, the imbalance is minimized and the distance from the bid-ask midpoint is minimized, in that order. Can also be thought of as being equal to the near price bounded between the best bid and ask price.
6. **matched_size**: The amount that can be matched at the current reference price (in USD).
7. **far_price**: The crossing price that will maximize the number of shares matched based on auction interest only. This calculation excludes continuous market orders.
8. **near_price**: The crossing price that will maximize the number of shares matched based auction and continuous market orders.
9. **[bid/ask]_price**: Price of the most competitive buy/sell level in the non-auction book.
10. **[bid/ask]_size**: The dollar notional amount on the most competitive buy/sell level in the non-auction book.
11. **wap**: The weighted average price in the non-auction book $\frac{BidPrice*AskSize + AskPrice*BidSize}{BidSize + AskSize}$
12. **seconds_in_bucket**: The number of seconds elapsed since the beginning of the day's closing auction, always starting from $0$.
13. **target**: The $60$ second future move in the wap of the stock, less the 60 second future move of the synthetic index. Only provided for the train set.
    
        i) The synthetic index is a custom weighted index of Nasdaq-listed stocks constructed by Optiver for this competition.

        ii) The unit of the target is basis points, which is a common unit of measurement in financial markets. A 1 basis point price move is equivalent to a 0.01% price move.

        iii) Where t is the time at the current observation, we can define the target

    $Target = \left( \frac{StockWap_{t+60}}{StockWap_{t}} - \frac{IndexWAP_{t+60}}{IndexWAP_{t}} \right) * 10000$



Goal of Machine Learning is to accurately predict "Target"

Other Submissions (if need inspiration):
- https://www.kaggle.com/competitions/optiver-trading-at-the-close/code
- https://www.kaggle.com/competitions/optiver-trading-at-the-close/discussion/487446 (Winner)
- https://www.kaggle.com/competitions/optiver-trading-at-the-close/discussion/486868 (9th place)