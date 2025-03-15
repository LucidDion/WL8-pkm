# Transformer Indicators

**Transformer Indicators** apply *transformations* to other Indicators. For example, you can create an indicator by adding or subtracting two other indicators. Transformers are especially useful in Building Block Strategies and can also be dropped onto the chart to form combinations of indicators that would otherwise require coding. If Transformers weren't available, you'd need to create custom indicators any time you needed a transformer-like operation for Building Blocks and Charting!

## Nesting Note
Most often, standard indicators are used as *Indicator* parameters in Transformers. But it's possible to add more levels of complexity by *nesting* Transformers:

Nesting means that you can use a Transformer Indicator as one of the *Indicator* parameters in another Transformer Indicator. For example, if one of the indicators to be transformed is a combination of two indicators, e.g., an SMA-smoothed RSI, use the *IndOnInd* or *SmoothedInd* Tranformer to create that indicator.

## Transformers in C# Coded Strategies
C# Coders are unlikely to program strategies using Transformer indicators since "transformations" can be coded more directly in WealthScript. However, if you drag & drop a Tranformer and "push" it into a C# Coded Strategy, you can continue to work with it with the following constraint (which is imposed by the Transformer Settings dialog): 

> A Transformer *Indicator* parameter can process indicators that use standard *PriceComponent* TimeSeries (OHLC/V), e.g., SMA.Series(bars.Close), or another Transformer indicator only. Applying an *indicator of an indicator* will not produce the expected result. For example, passing an indicator like `SMA.Series(RSI.Series(bars.Close, 14), 5)` in a Transformer indicator parameter will be interpreted *incorrectly and without error*.

---
### CrossoverIndValue
The *Crossover of Value Indicator* creates a binary wave (+/- 1) of Indicator's crossings above and below specified thresholds. **CrossoverIndValue** will return +1 when the Indicator (usually an oscillator type) *last crossed over* the "Above" threshold and -1 when the Indicator *last crossed under* the "Below" threshold.

%{color:blue}**Example**% 
Apply CrossoverIndValue to an RSI indicator with the above/below threshold levels set to 60/40. When the RSI crosses above 60, **CrossoverIndValue** will return +1 until the RSI crosses below 40 at which time the value would change to and remain -1 until the next time the RSI crosses above 60. 

### IndOnInd
*Indicator on Indicator* applies one Indicator to another Indicator. For example, you can create a smoothed RSI using any moving average as *Indicator* and the RSI as the *applied to* parameter.

![IndOnInd Settings](https://www.wealth-lab.com/Images/WLHelp/IndOnInd.png)  

### MathIndOpInd
**MathIndOpInd** returns an indicator that is the result of a mathematical operation on two other Indicators. 

### MathIndOpValue
**MathIndOpValue** returns an indicator that is the result of a mathematical operation on another Indicator and a fixed value. For example, you could create a 5% band above the close by multiplying the Close by 1.05. 

### OffsetInd
*Offset Indicator* applies an offset to another Indicator. A positive value for *Offset Bars* offsets the Indicator to the right (delay). A negative value offsets to the left (advance). Offsetting an Indicator to the left results in peeking into the future, so this indicator is flagged as possibly peeking.";

### RisingFalling
*Rising/Falling* returns a series that indicates if the indicator is rising(+1), falling(-1), or equal(0) for a specified scale. For example, this indicator can easily determine if the Weekly or Monthly RSI is rising or falling, which can be used as a filter for your Daily strategy. 

### ScaleInd
*Scale Indicator* compresses an Indicator to a higher scale frequency. For example, to a weekly scale from a daily base scale. ScaleInd works only to scale indicators that operate on the source BarHistory or one of its PriceComponents (OHLC/V).

### SmoothedInd
*Smoothed Indicator* Uses another Indicator (a Smoother) to return a Smoothed version of the selected indicator. 

### SymbolInd
*Symbol Indicator* returns the specified Indicator for an external symbol, i.e., a symbol other than the primary symbol being charted.

![SymbolInd Settings](https://www.wealth-lab.com/Images/WLHelp/SymbolInd.png)  

