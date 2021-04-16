# KNearest Neighbors SPY Price Direction Model
---
#### At a glance
- Machine Learning Project aimed to make a model that can predict the the direction of the SPY etf price on the next trading day


## Introduction

Stock market predictions using Machine Learning is daunting task due to the random behavior of the market. In this notebook, I am attempting to build a model that predicts the price direction of the SPY. The spy is an echange traded fund (etf) that tracks the S&P 500 index. The S&P 500 measures the perforamce of the 500 of the largest companies and is a solid evaluator for the whole stock market. I will be using this along with the E-MINI one month futures contracts and VIX volatlity index to predict the direction of the SPY etf. Futures and the VIX volatility index and their importanceare explained in more detail in the notebook

### Goal
To simplify my model, it will only predict percent change. A postive percent change will be assigned a buy signal and a negative percent change will be assigned a pass signal. (1 signals buy and 0 signals pass). Having said that I am going to judge the performance of the model on its precision and its ability to generate profit. Precision being percentage of times the stock went up given the model predicted the price going up. Since I am modeling around buy signals I'm more focused on limiting false postives. The recall rate does not need to be high but also not so low were I am not generating any buy signals. The AUC score of the precsion recall curve will also be used to evaluate the perfomrance of the model and its features. The precision of the model will be compared to the precision of predicting a buy signal very signal day.

## Data
- Daily price data (Open,Close,High,Low,Volume) for SPY, E-MINI, and VIX was collected finance.yahoo.com

## Feature Engineering 
- Relative Stength Index, simple moving averages(10, 50, 150 day moving average) 50 moving 2nd standard deviations were calculated using the price data.
- Calculated ratios and differences of some of the moving averages 
- This data set includes the current day features and uo to 3 days back. For example there is Close is the current day's closing price. Close_1 is yesterday's closing price This repeats for up until 3 days back and is applied to every feature that was engineered as well. 
- In total there are over 100 features 

## Results
#### Predicted SPY price vs Actual SPY price ofr next trading day
![Alt text](https://github.com/jacobh310/stock_prediction-models/blob/master/KNearest_Neighbor_regressor/images/predicted_vs_actual.JPG?raw=true "Sentiment")
- The results above came from a KKN alogrithim only being trained on the Open, Close, High, Low of the previous day
- From the line plot on the right it looks like the KNN algorithimg is closely undershooting the price

### Feature Selectiction 
- After testing tens of thousands of different feature combinations, the model precision was 64% vs the bench mark 57.2%

## Precision Recall
![Alt text](https://github.com/jacobh310/stock_prediction-models/blob/master/KNearest_Neighbor_regressor/images/precision_recall.JPG?raw=true "Sentiment")
- The Precison vs Recall curve shows that a threshold a slightly greater than a percent change of 0 would have a higher precision without sacrificing to to much recall when compared to the 0 percent change threshold.
- Thresholds being what my model considers a buy signal. Normally the thresh old is 0.0%. Anything above 0 indicates a postive percent change or a buy signal. Anything below 0.0% is a nagative percent change or a pass signal.

## Profit Loss/Evluation
- I built an algorithim to simulate real life trades with $10000. I will be testing out different thresholds and Risk Return ratios 
- I also implemeneted the maximum short capital gains tax in the algorithim
- The model will be comapared to investing $10000 into SPY over the same period of time
![Alt text](https://github.com/jacobh310/stock_prediction-models/blob/master/KNearest_Neighbor_regressor/images/profit_lossJPG.JPG?raw=true "Sentiment")
- Max Profit: $14400.62
- Best threshold:0.17%
- Model return: 44.01%

- SPY gain: 33.42% 
- SPY Investmet: $13341.61

The testing data shows that even with the high taxes the SPY trading strategy with the KNN model was more lucrative that investing $10000 into SPY

## Test (Holdout Validation)
- Model Precsion:56.97%
- Benchmark Precision: 57.72%

- Profit Before Taxes: $13489.78
- Profit post Max Taxes: $12079.90
- SPY Investment: $13871.05


## Conclusion
It does not make statistical finincial sense to deploy the final model with how poorly it performed on the test data. I will say that the test data included the stock market crash of March 2021. Given that market crashes do not happen very often it is impractical to think any machine learning algorithim has enough data to do well in those market conditions.

## Future work
I can develop a filter or bias where the model is only allowed to trade in certain market conditions. For example, only training the model on data that is above the 150 moving average. If there is a rapid drop in price below the 150 moving average the bot would not enter trades.
There are also a plethora of other indicators and metrics that can be combined.


## Resources
https://www.investopedia.com/terms/b/beta.asp
https://www.investopedia.com/terms/v/vix.asp
https://www.investopedia.com/ask/answers/042315/how-do-sp-500-futures-work.asp
https://towardsdatascience.com/machine-learning-techniques-applied-to-stock-price-prediction-6c1994da8001
https://github.com/NGYB/Stocks/tree/master/StockPricePrediction
This model also only used data from the current date and past 3 trading days. Tuning the number of past trading days can yield different results
