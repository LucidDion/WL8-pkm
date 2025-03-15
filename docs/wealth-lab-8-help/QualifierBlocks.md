# Qualifier Building Blocks
Each [Condition Building Block](ConditionBlocks) can optionally accept one **Qualifier Building Block**. The Qualifier Blocks alters how the logic of the Condition Block is evaluated.

---
## For N Consecutive Bars
In order for the Condition Block to evaluate to true, its condition must occur for a certain number of consecutive data points (bars). In this example, the entry occurs if the RSI indicator spends 3 consecutive trading days in oversold territory.  
 
![Consecutive Bars Qualifier Block](https://www.wealth-lab.com/Images/WLHelp/NConsecBars.png)

---
## N Bars Ago
Causes the condition to be evaluated a certain number of data points (bars) ago, instead of on the current bar being processed.

---
## N Times Within N Bars
In order for the Condition Block to evaluate to true, its condition must occur a certain number of times within the specified lookback period.

---
## Within the Past N Bars
The Condition Block evaluates to true if its condition occurred at least one time within the specified lookback period.

---
## Indicator Symbol
This Qualifier Block causes indicator calculations on its Condition Block to be performed on a different symbol than the one currently being processed. This lets you easily implement Strategies that use external data to make trading decisions. In the example below, the Strategy goes long when the RSI indicator of the current symbol being tested is oversold, but *also requires* the RSI of the overall market (using SPY as a benchmark) be oversold.  
 
![Indicator Symbol Qualifier Block](https://www.wealth-lab.com/Images/WLHelp/IndicatorSymbol.png)


This example video shows how to use external symbol's data:

[![External Symbol Indicator Strategy](http://img.youtube.com/vi/gVRQ1i2HtqY/0.jpg)](https://www.youtube.com/watch?v=gVRQ1i2HtqY "External Symbol Indicator Strategy")

## Logical Inverter
When applied to a Condition Block, causes the Block to evaluate to true if its conditional logic evaluates to false.