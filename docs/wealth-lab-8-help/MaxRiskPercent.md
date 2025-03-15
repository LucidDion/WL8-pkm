# Max Risk Percent
This position sizing method you specify the **maximum percentage loss** you're willing to take on a trade, and a **stop loss level**. The position is sized such that, if the stop loss level is hit, the trade results in a loss that is as close as possible to the maximum risk. Market factors such as price gaps can result in trades that have losses greater than the specified maximum.

## The Stop Loss Level
For this position sizing method to work, your Strategy needs to establish an initial stop loss level at the time it places the trade. Furthermore, the Strategy must subsequently issue exit orders at the stop loss level, otherwise the Max Risk Percent method won't work as intended. WL8 provides defaults to help get Max Risk Percent position sizing functioning easily.
## Max Risk Indicator
An initial Stop Loss Level is automatically calculated based on the Max Risk Indicator that is set up in [Trading Preferences](TradingPreferences). The default Max Risk Indicator is **MathIndOpValue(Low,Multiply,0.9)** which resolves to a value that is 10% below the low of the signal bar. You can replace the Max Risk Indicator in Trading Preferences, but you should take care to pick an indicator that will consistently return values that are well below the current price range for long trades or above the current price for shorts. If the strategy trades both long and short, then you must customize the stop loss in a C# Strategy as described next.
## Customizing the Stop Loss Level
In a [C# Coded Strategy](CSharpCodeBased) you can override the method **GetMaxRiskStopLevel** to return a customized Stop Loss level. The method provides you the BarHistory, PositionType, and index being processed so you can use whatever means required to calculate and return an appropriate Stop Loss for the trade. The value you return here will be used instead of the Max Risk Indicator.

```csharp
public override double GetMaxRiskStopLevel(BarHistory bars, PositionType pt, int idx)
{
	double atr = ATR.Series(bars, 14)[idx] * 1.5;
	double stop = (pt == PositionType.Long) ? bars.Low[idx] - atr : bars.High[idx] + atr;
	return stop;
}
```
		
## Placing Exit Orders
A Strategy needs to place exit orders at the Stop Loss Level in order for the trade to close, limiting the risk to the specified Max Risk amount. You can issue these exits as you normally would in your C# Coded Strategies. A Position's established Stop Loss Level is stored in the Position instance's **RiskStopLevel** property.

☑ Automatically issue a Stop Loss Order
WL8 provides an automated way to generate these exit orders. In Trading Preferences, enable the **Automatically Issue a Stop Loss order** check box to turn on this behavior. This feature is handy to enable in [Building Block Strategies](BuildingBlock), where you cannot access the Stop Loss Level of a Position.

☑ Adjust Stop Loss Level bar-by-bar (Trailing)
The second option, **Adjust Stop Loss Level bar-by-bar**, causes the Position Stop Loss Level to be recalculated each bar, based on its Max Risk Indicator. For long positions, if the new result is greater than the previous value, it adjusts upward, resulting in the Stop Loss Level ratcheting up in a trailing stop manner. The opposite occurs for short trades.

For a demonstration of features, see this Youtube video:
[![WealthLab 8 Build 11 - Max Percent Risk Position Sizing Returns](http://img.youtube.com/vi/xkzJZuYei_o/0.jpg)](https://www.youtube.com/watch?v=xkzJZuYei_o "Max Percent Risk Position Sizing Returns")


%{color:blue}**Max Risk Sizing Example**%  
Assume current equity is $50K and you set 3% for the Max Risk % Sizer. The strategy buys at $150 LIMIT and your stop price is 10% below the entry, or $135. The number of shares, then, is:

$ Risk = $50000 * 3% = $1500  
Share size = $1500 / (150 - 135) = 100 shares

Summarizing, your trading strategy will buy 100 shares at 150 and should control the risk by selling at a stop loss if price hits 135. If price drops to that level, 100 shares will lose about $1500. Note that if price gaps lower than 142, the trade will lose even more.

