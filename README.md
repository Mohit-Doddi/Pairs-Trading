# Pairs-Trading
Pairs trading is a statistical arbitrage strategy.  The strategy is to simultaneously take a long position and a short position on a pair of stocks that are cointegrated in the past but have sufficient spread between them on the day of trading.This is based on the assumption that the spread between them is mean-reverting.  The weights for each leg of the pair (hedge ratio) is estimated using a statistical method.  

#Data Collection:
+ Scrapped data for futures using the Nsepy library in python 
+ Data collected for the time period :- 1/1/2014- 31/12/2019 
+ Took only those contracts which have near month expiration 
+ Sliced the data to keep only those contracts which had the futures of the underlying trading for the whole period. 

#Methodology:
1) Divided the data into two time periods :-
     P1 :- Time period used for checking which pairs of futures are cointegrated through their closing prices 
     P2:- Running backtest to see the returns obtained using our strategy 
2) Find cointegrated pairs by running cointegration test on all possible pairs
3) Take k ( a parameter ) number of pairs with the lowest p-value in the cointegration test  
4) For every pair X-Y of futures:-
     Regress returns of Y on X and model the residuals of this regression as an OU process
     Take coefficient of X as the hedge ratio ( number of contracts of X traded for every contract of Y) 
5) Select pairs which have a positive sharpe in in-sample backtesting
Establish trading rules such that you go long/short on Y and short/long on X whenever the residual of the above regression diverges sufficiently below/above its expected value.
