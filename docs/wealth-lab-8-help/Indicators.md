# Indicators

 - [take me there now](action:Indicators)

**Indicators** are time series data that can be plotted in [Charts](Chart) and used in trading [Strategies](Strategies). The data points that make up **Indicators** can come from these sources:

 - Calculated based on the historical price/volume data of the symbol currently being charted or processed in a backtest. Examples include **Simple Moving Average** (**SMA**) and **Relative Strength Index** (**RSI**).
 - Sourced from fundamental data based on the current symbol. Examples include **Fundamental** and **FundamentalRatio**.
 - Calculated based on historical price/volume data from a symbol *other than* the one currently being charted or processed. Examples include **SymbolData**.
 - Sourced from an external provider, such as a supplier of economic indicators or market breadth data. Examples include **USTYield** (sourced from a government web site that publishes historic US Treasury yield rates).

---
## Using Indicators
In Wealth-Lab, **Indicators** can be used in a variety of places:

 - Drag and dropped onto [Charts](Chart).  
 - In [Building Block Strategies](BuildingBlock), as a [Building Block](BuildingBlocks) parameter.
 - In [C#-Coded Strategies](CSharpCodeBased), you can create instances of indicators by calling their constructors.
 - As the weight factor in [Rotation Strategies](Rotation).

### Drag and Dropped Indicators 
#### Apply Indicator to Another

 1. Drag an indicator from the indicator pane and drop it into a chart. Configure as required.
 2. Drag another indicator and before releasing the mouse, hover over the first indicator's plot. 
 3. When the plotted indicator becomes highlighted, drop the second indicator and configure. 

#### Edit (or Delete) 
To edit or delete an indicator that you've dropped into a chart, left click on the indicator's label at the top of the pane to produce the **Edit...** and **Delete** options.

---
## Creating Indicators
See the [Custom Indicators](CustomIndicators) topic for information on how to create your own Indicators.

---
## [Unstable Indicators](StabilityOfIndicators)
Some indicators known as unstable can produce different results in the short term if the data loading range is insufficient. For reproducible results from a trading strategy, you must use indicators when they're stable.