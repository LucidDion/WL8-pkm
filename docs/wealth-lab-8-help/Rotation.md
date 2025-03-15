# Rotation
**Rotation Strategies** use one specific [Indicator](Indicators) to assign a **weight value** to all of the symbols in the backtest [DataSet](DataSets) and rotate into the symbols that have the highest (or lowest) weight value on a periodic basis. This **Strategy** always stays fully invested in the market, swapping into the top or bottom few symbols after sorting them by **weight factor**.

---
## Source Indicator
Any **Indicator** that Wealth-Lab contains can be selected as the source of the **weight factor**. You can select manually from the drop-down list or drag and drop an **Indicator** from the [Indicators](Indicators) list.

---
## Rotation Settings
The other important settings of the **Rotation Strategy** are:

 - **Number of Symbols to Hold** - Controls how many symbols are held at any given time. Changing this value automatically set the **position sizing** in **Strategy Settings** to an appropriate **Percent of Equity**.
 - **Sort Direction** - Let you **buy symbols with** either the **lowest** or **highest** weight.
 - **Rebalance Frequency** - controls how often the **Strategy** performs a **rebalance**, checking the weight values and buying/selling accordingly. Supported rebalance intervals are *only* Daily, Weekly, and Monthly.
 - **Position Type** - allows you to create either a **Long** or a **Short** Rotation Strategy.

## Additional Conditions
Here you can drag and drop Condition [Building Blocks](BuildingBlocks) to impose additional restrictions on which symbols are considered for inclusion. During the Rotation Strategy Rebalance, only symbols that meet all of the Conditions are considered as candiates to hold for that period.

[![Rotation Strategies with added Conditions](http://img.youtube.com/vi/RxikkJgQk8Y/0.jpg)](http://www.youtube.com/watch?v=RxikkJgQk8Y&t=400s "Rotation Strategies with added Conditions")
