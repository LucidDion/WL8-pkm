# MetaStrategies

 - [take me there now](action:MetaStrategy)

**MetaStrategies** are **Strategies** that are composed of other **Strategies**. You can backtest a group of **Strategies**, preferably non-correlated, together. After the backtest, you see the aggregate result in the various [Strategy Result Viewers](StrategyResultViewers). **MetaStrategies** provide an additional Strategy Result Viewer, **Profit Curves**, which shows graphs of the individual component Strategy profit curves.

To compose your **MetaStrategy**, drag one or more **Strategies** from the [Strategies](Strategies) list onto the MetaStrategy design surface. There you can set the following parameters of each Strategy:

 - [DataSet](DataSets) of data to use in backtest
 - **Scale** of data
 - **Position sizing**

### Important!
> 1. MetaStrategies run with [Retain NSF Positions](AdvancedStrategySettings) enabled and is not optional.  
> 2. MetaStrategies are incompatible with the [Trading Preference](TradingPreferences) **Use Broker Account Value for Position Sizing**.

---
## Portfolio Weighting
Each Strategy gets a certain percentage of the overall backtest equity, controlled by the 
**Portfolio Weighting** that you establish. For example, with a starting capital of $100,000, and 4 Component Strategies added, by default each Component Strategy would get $25,000 allocated for its backtest run.

---
## Rebalancing
Select the desired **Rebalance Frequency** from the MetaStrategy toolbar. This controls how often the equity and cash of the component Strategies are reallocated to get back in line with your established **Portfolio Weighting**. 

Rebalancing doesn't liquidate Positions. It reallocates available cash between Strategies to 
move closer to the Portfolio Weight allocations that you specify.

## Common Capital Pool
Check this option in the MetaStrategy designer toolbar to turn on Common Capital Pooling. In this mode, all of the Component Strategies share the same source equity pool as defined in the parent MetaStrategy starting capital. The Component Strategies also the combined equity to determine their % of equity Position Sizing.

Enabling this option has the following effects:

 - Portfolio Weight becomes irrelevant, and the associated controls no longer appear in the designer.
 - Rebalancing becomes irrelevant, and the associated control is disabled in the designer.
 - All Component Strategies adopt a margin factor to match the margin factor of the parent MetaStrategy.

## Inter-Strategy Signal Pruning
When this option is enabled, the MetaStrategy will maintain only one position per symbol, even if the component Strategies could have multiple positions in the symbol. The feature works by performing the following steps:
- Eliminates buy signals if there is already an open position for the symbol.
- Eliminates a sell signal if there is more than one open position for the symbol in all of the component Strategies.
- Eliminates all addition entry signals for a symbol of there is a market entry signal.
