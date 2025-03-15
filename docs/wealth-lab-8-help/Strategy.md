# Strategies

 - [take me there now](action:Strategies)

A **Strategy** is a set of rules that determine when to buy and sell a market based on its history. Wealth-Lab lets you develop Strategies in a number of ways:

 - [**Building Blocks**](BuildingBlock): drag and drop Entry & Exit rules, and Conditions
 - [**C#-Coded**](C#CodeBased): hand coded logic using the [C# programming language](https://en.wikipedia.org/wiki/C_Sharp_%28programming_language%29)
 - [**Rotation**](Rotation): uses an [Indicator](Indicators) as a weight factor to rotate into and out of the strongest symbols in a [DataSet](DataSets)
 - [**MetaStrategy**](MetaStrategy): backtests a *group of Strategies* together. 
 - [**Trade History**](TradeHistoryStrategy): creates a backtest using a history of trades, usually downloaded from your broker. 

## Backtesting
Backtesting means running your Strategy through a set of historical market data and evaluating its performance. Wealth-Lab provides numerous [Performance Visualizers](PerformanceVisualizers) that let you explore your Strategy's performance in many ways.

## Streaming and Strategies
The Building Block Design Surface and the C# Code Editor work with static data only.  For a Strategy to generate Signals with streaming data: 

1. launch a Chart window, 
2. drag and drop a Strategy onto it, and, 
3. click the Stream button to turn on Streaming. 

**Tip!**
Once you have several streaming Strategies set up, save your [Workspace](Workspaces) to quicky recall it.

![Strategy in Streaming Chart](https://www.wealth-lab.com/Images/WLHelp/ChartStreamStrategyKraken.png)

---
## Strategy Parameters
Parameters hold the values used for variables in a Strategy.  For example, 50 could be the value for the period parameter in a 50-day moving average. You can assign Parameters in a C# Strategy's constructor using **AddParameter()** or with a building block strategy by clicking the "Make Optimizable" button, when shown. 
Parameters have a name, type, default value, a min/max range, and a step value.  [Optimizations](Optimization) attempt to find the value for parameters that "optimize" an objective metric (e.g., APR% or Sharpe Ratio) within the range that you define. 

---
## Optimizing
You can define **Parameters** in your Strategies. Parameters are values that can assume a range of values, with a defined *start*, *stop*, and *increment*. You can use [Optimization](Optimization) to automatically backtest your Strategy using different combinations of Parameter values to find the most profitable ranges.

---
## Locking Strategies
From the Strategy window, you can lock a Strategy by clicking the **Lock** button on the toolbar. While a Strategy is locked, you can make changes to it, but cannot Save those changes. You also won't be warned about unsaved changes when you close the Strategy window.
