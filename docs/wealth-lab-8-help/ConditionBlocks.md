# Condition Building Blocks
You can drop one or more **Condition Blocks** onto **Entry** and **Exit Blocks** to apply conditions to entries and exits. In order for the entry or exit to occur, *all of* the attached conditions must evaluate to true.

---
## Indicator Compare to Value
Compares an **Indicator value** to a specific **numeric value**. Whenever a Building Block lets you specify an Indicator, you can choose from any of the [Indicators](Indicators) contained in Wealth-Lab, including from extensions. Additionally, you can specify the core data series Open/High/Low/Close or Volume, as well as a number of calculated averaged series, like AverageOHCL which is the average of Open, High, Low and Close. The core data series appear at the top of the Indicator drop down list.

Here we create a condition that checks if the RSI indicator is oversold.  
 
![RSI less than 30](https://www.wealth-lab.com/Images/WLHelp/RSIOversold.png)

---
## Indicator Compare to Indicator
Similar to above, but compares an **Indicator value** to **another Indicator value**. You can also specify an optional lookback period for the second Indicator. This lets you accomplish something like below, where we see if the moving average (SMA) is higher than it was the day before.  
 
![Indicator Compare to Indicator](https://www.wealth-lab.com/Images/WLHelp/SmaGreaterThanDayBefore.png)

---
## Indicator %Above/Below Indicator
Evaluates to true when an Indicator is a **certain percentage above or below another Indicator**. In this example, the Strategy sells the next bar at market open if the price (High) penetrates 1% above the upper Bollinger Band.  

![Indicator %Above/Below Indicator](https://www.wealth-lab.com/Images/WLHelp/PercentAboveBBand.png)

--- 
## Indicator Crosses Value
Similar to Indicator Compare to Value, but evaluates to true when an Indicator **crosses over** or **crosses under** a numeric value. For example, if the RSI on this bar is 35, and the previous bar's RSI value was 29, the RSI is considered to have **crossed over** 30.

---
## Indicator Crosses Indicator
Resolves to true when one Indicator **crosses over** or **crosses under** another Indicator. A typical case is price (Close) **crossing over** or **crossing under** a moving average (SMA). Another common strategy involves two moving averages, one fast and one slow. The example below enters the market when the fast moving average **crosses over** the slow moving average.  
 
![Indicator Crosses Indicator](https://www.wealth-lab.com/Images/WLHelp/SmaCrossover.png)

---
## Indicator Crosses Signal Line
Triggers when an Indicator crosses over or crosses under a **signal line**. The **signal line** is a smoothed version of the source Indicator, created by applying another Indicator called a **smoother** to the source Indicator. Wealth-Lab comes with many smoothers, such as a **Simple Moving Average** (SMA), **Exponential Moving Average** (EMA), and **Median**. This Condition Block lets you select which smoother to use from a dropdown list. In this example, the Strategy goes long (enters a new long position) when the MACD indicator crosses over its signal line based on a 9 period SMA.

![Indicator Crosses Signal Line](https://www.wealth-lab.com/Images/WLHelp/IndicatorCrossesSignalLine.png)

---
## Indicator new High/Low
Evaluates to true when an Indicator makes a **new high** or **new low** value within a specific lookback period.

---
## Indicator Turns
Lets you check if an Indicator has **turned up** or **turned down**. An Indicator has **turned up** when its value is higher than its previous value, after a period where it has been declining. The following example uses two Condition Blocks to time an entry when the CMO oscillator **turns up** while below -40.  
 
![Indicator Compare to Value](https://www.wealth-lab.com/Images/WLHelp/CmoTurnsUp.png)

---
## Open Position Count
Let's you compare the number of open positions in the backtest to a specific value. This Condition Block has a parameter called Across Portfolio. When set to false, the Block counts of the number of open positions for the current symbol being processed. When set to true, it counts the total number of open positions across all symbols.

The Strategy below maintains two open positions. It enters when the RSI Indicator goes below 40, and then again when it goes below 30. It uses the **Open Position Count Condition Block** to ensure that only two positions are maintained for each symbol.  
 
![Open Position Count Block](https://www.wealth-lab.com/Images/WLHelp/RsiDoubleEntry.png)

---
## Symbol Filter
Accepts a set of symbols separated by commas and spaces and resolves to true if the symbol currently being processed is contain in this list. This Condition Block is useful in pairs trading situations where you want to apply one set of trading logic to one symbol, and different logic for another symbol.

---
## Symbol Ranking by Indicator
Intended to be used when backtesting on a DataSet, not an individual symbol. Ranks the symbols by a specified Indicator and resolves to true of the current symbol is within the Top or Bottom of a specified number of symbols. The default parameters resolve to true if the symbol is one of the 5 that has the lowest RSI(20) in the DataSet on the current bar of data.

---
## Transaction Weight (a.k.a. Priority)
This Condition Block technically is not a condition. It is a way for you to set the **weight**, a priority, of an entry signal in a Building Block Strategy. Transaction Weight comes into play in the ```Backtester``` when there are more trade signals generated than available simulated capital. The ```Backtester``` fills signals with a higher weight first, giving them priority to use available buying power.

If you do not assign Transaction Weight, Wealth-Lab assigns it randomly, which can lead to varying results for the same backtest. For a demonstration, see the video: [Same Strategy and Data, Why Different Results?](https://youtu.be/ECCF5zdnC7U)

In the Transaction Weight block you specify an **Indicator** on which to base the priority and whether trades should be prioritized by **Lowest** or **Highest** weight values. For example, all else being equal if you think that a stock with a lower RSI value will perform better than one with a higher value, configure an RSI indicator and choose **Lowest Values**. 

**Transaction Weight** should only be used with **at Market** entries. In practice, when you have too many trade candidates (with respect to buying power), you can sort the Alerts by some indicator value and choose the signals having the highest or lowest values to place as trades for the market open.  This is what the Transaction Weight block simulates.

**Stop and Limit** orders are different.  You should place *all* stop and limit orders signaled by a strategy in the market since there's no way to know which will be filled or the order in which fills occur.  The only valid priority value for **at Limit** and **at Stop** entry signals for an accurate backtest is the *time of day* at which the price exceeds the signal trigger price.  An *earlier* time of day is given *greater weight*. You can apply **Time-of-day priority** in end-of-day backtests with **Use Granular Limit/Stop Processing** in [Advanced Strategy Settings](AdvancedStrategySettings).

---
## Trend Line Break
Resolves to true if prices break above or below a trend line. 
![Open Position Count Block](https://www.wealth-lab.com/Images/WLHelp/TrendlineBreak.png)

Define the trendline by specifying the following parameters:  
 
**Trendline Points**  
Number of peak/trough points used to compose trendline.  Trendlines with more than 2 points are fit using the **least squares method** (linear regression prior to Build 12).
  
**Reversal Percent**   
 The percentage required to qualify a peak/trough.
 
**Maximum Deviation**  
The maximum deviation of the trendline from the peaks/troughs used to define it. A deviation of 1% or lower indicates a trend line that is very close to its source points.
 
**Trendline Direction**  
 Whether the trend line is rising or falling.
 
**Breaks**  
Whether price breaks above or below the trendline.  Since by definition price will be *below peaks* and *above troughs*, you would choose a break **Above/Below** for trendlines based on **Peaks/Troughs**, respectively. 

**Base Trendline on**  
Choose if the trendline should use **Peaks** or **Troughs**.  The most recent peaks or troughs with respect to the current bar are used. 

**Chart Type**  
Choose if the trendline should be observed on a **Linear** (default) or **Log** chart. 

---
## Trend Line Break Advanced
Just as with **Trend Line Break** resolves to true if prices break above or below a trend line.  The difference is that this rule does not require consecutive peaks/troughs to create the trend.  This allows longer term trends to be revealed even when using small reversal percentages. 

Trend Line Break Advanced will discover many simultaneous trendline possibilities and returns one of them based on the following logic: 

- **2-Point Lines** - Returns the trendline with the least (most negative) slope for rising or falling Peaks.  Likewise, the rule returns the trendline with the greatest (most positive) slope for rising or falling Troughs. 
- **Multi-point Lines** - Since several active trends may be found, returns the trendline with the least percentage deviation from the composing peaks/troughs. 

![Open Position Count Block](https://www.wealth-lab.com/Images/WLHelp/TrendlineBreakAdvanced.png)

The same options apply as the previous Trend Line Break condition with the following omission and additions:

**Breaks**   (Not Required!)  
For trendlines based on Peaks, a break occurs when price crosses Above the trendline.  Likewise it's understood that for a trendline created by Troughs, a break occurs when price crosses Below.
 
**Incursion % Allowed**  
Allows for peaks or troughs that are not part of the trendline to be crossed by a specified percentage.  If a peak/trough incursion exceeds this value, the trendline is not created. 

**Calendar Days Lookback**  
Discards peaks/troughs that are "too old" as of the current bar.  This is an optimization feature that can help speed up a trendline search especially for intraday simulations that use Trend Line Break Advanced. 
