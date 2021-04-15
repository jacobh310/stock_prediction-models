# KNearest Neighbors SPY Price Direction Model
---
#### At a glance
- Machine Learning Project aimed to make a model that can predict the the direction of the SPY etf price on the next trading day

## Introduction

I am going to be predicting the direction of the SPY which is an echange traded fund (etf) that tracks the S&P 500 index. The S&P 500 measures the perforamce of the 500 of the largest companies and is a solid evaluator for the whole stock market. I will be using this along with the E-MINI one month futures contracts and VIX volatlity index to predict the direction of the SPY etf. Futures and the VIX volatility index and their importanceare explained in more detail in the notebook

### Goal
To simplify my model, it will only predict the percent change and assiging a buy if the percent change is positive and pass signal otherwise(1 signals buy and 0 signals pass). Having said that I am going to judge the performance of the model on its precision and its ability to generate profit. Precision being percentage of times the stock went up given the model predicted the price going up. Since I am modeling around buy signals I'm more focused on limiting false postives. The recall rate does not need to be high but also not so low were I am not generating any buy signals. The auc score of the precsion recall curve will also evaluate the perfomrance of the model and its features.

## Data
- Daily price data (Open,Close,High,Low,Volume) for SPY, E-MINI, and VIX was collected finance.yahoo.com

## Feature Engineering 
- Relative Stength Index, simple moving averages(10, 50, 150 day moving average) 50 moving standard deviations were calculated using the price data.
- Calculated ratios and differences of some of the moving averages 

## Results
![Alt text](https://github.com/jacobh310/film_revenue_model/blob/master/images/feat_importance.JPG?raw=true "Sentiment")
