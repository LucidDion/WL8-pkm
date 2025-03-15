# Strategy Preferred Values
**Preferred Values** are [Strategy](Strategy) Parameter values that you've saved as the result of an [Optimization](Optimization). Each Preferred Value consists of a Symbol and a set of name/value pairs that represent the best Parameter values that the Optimization obtained for that Symbol.

For example, assume you ran a [Symbol by Symbol Optimization](SymbolBySymbolOptimization) on a Strategy with two Parameters named **Bars Ago** and **Consec Down**. You then select **Highest APR** as the [Performance Metric](MetricPreferences) to view, and the Optimization yields the following result:

![Symbol by Symbol Optimization](https://www.wealth-lab.com/images/WLHelp/SymBySym.png)

You can at this point right click and save each of the individual Symbol's Parameter values listed here as its Preferred Values. 

[![Preferred Values Walkthrough](http://img.youtube.com/vi/xuCCof5KcQY/0.jpg)](https://www.youtube.com/watch?v=xuCCof5KcQY&t=10s "Preferred Values Walkthrough")

---
## Preferred Values Tab
If a Strategy has Preferred Values, you'll see a new **Preferred Values** tab appear in the Strategy window. Here you can browse, or delete some or all of the Strategy's saved Preferred Values.

Preferred values are saved with a Strategy, so if you make any changes to them via an Optimization right click or in the Preferred Values tab, be sure to *save the Strategy* to persist the changes.

---
## Using Preferred Values in Backtesting
In the [Strategy Settings](StrategySettings) tab, **Strategy Parameters** section, if the Strategy has Preferred Values, you'll see a check box enabling you to use them in backtesting. When this option is enabled, the backtest will apply each Symbol's Preferred Values to its Parameters while executing. In the example above, AMZN would get a **Bars Ago** value of 2, while TCOM would get 6, and AAPL 3.

%{color:blue}**Note!**% 
>Using Preferred Values can easily lead to curve fitting. You can avoid this by determing 
Preferred Values in one data range, and then applying them in a different data range.

---
## Preferred Values in all Wealth-Lab Tools
PVs are saved with the Strategy, and the Strategy Setting to **Use Preferred Values** controls whether or not PVs are applied wherever the Strategy is run - in the [Strategy Monitor](StrategyMonitor), [Strategy Rankings](StrategyRankings), [MetaStrategy](MetaStrategy), or the [Signals Publisher](SignalsPublisher). If you need different versions of the Strategy for different tools, Clone the Strategy and save it with the desired settings. 