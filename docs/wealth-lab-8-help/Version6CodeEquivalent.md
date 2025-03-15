
# Version 6 Code Equivalents

We re-wrote Wealth-Lab from the ground up and made some major changes in Versions 7 and 8!  The backtest now executes strategies for each symbol in synch on a bar-by-bar basis instead of running each symbol and compiling the results after the fact. This makes it much more powerful and flexible, but the cost is a new class model for creating Strategies. It's the same C# language, so it's usually quick work to migrate your strategies from Version 6 once you get the hang of it. 

For those familiar with Wealth-Lab 6 WealthScript, the reference of code equivalents below for some of the most-used functions may be helpful.  

For a more extensive treatment, download and install a Version 6.9 QuickRef containing Version 7 equivalent references from [this forum post](https://wl6.wealth-lab.com/Forum/Posts/Download-Version-6-9-QuickRef-with-Version-7-Equivalents-40609) or from the [Wealth-Lab Wiki](https://www2.wealth-lab.com/WL5Wiki/QuickRef7.ashx). 

If you can't find what you're looking for, ask us about it in the [Wealth-Lab Discussions](https://www.wealth-lab.com/Discussions). 

## Common Classes/Objects

| Wealth-Lab 6.9 | Wealth-Lab 7, 8| 
|----|----|
| DataSeries  | TimeSeries\nIndicatorBase (derives from TimeSeries) |
| Bars | BarHistory  |

## Functions

| Wealth-Lab 6.9 | Wealth-Lab 7, 8| 
|----|----|
| BuyAtMarket(bar + 1,"SignalName"); | PlaceTrade(bars, TransactionType.Buy, OrderType.Market, 0, "SignalName"); | 
| SetShareSize(100); | Transaction t = PlaceTrade(...);\nt.Quantity = 100;  |
| IsLastPositionActive() | HasOpenPosition(bars, PositionType.Long) | 
| ActivePositions() | OpenPositionsAllSymbols()\nGetPositions() |   
| CrossOver(bar, Close, sma) | bars.Close.CrossesOver(sma, idx) | 

## Indicators

| Wealth-Lab 6.9 | Wealth-Lab 7, 8| 
|----|----|
| DataSeries sma = SMA.Series(Close, 20); | IndicatorBase sma = SMA.Series(bars.Close, 20); |  
| DataSeries zeroSeries = new DataSeries(Bars, "My New Series"); | TimeSeries zeroSeries = new TimeSeries(bars.DateTimes, 0);\nzeroSeries.Description = "My New Series"; |  
| CreatePane | Not required.\nUse a *paneTag* parameter string in the Plot functions, e.g. ,"Price" for price pane, "Volume" for VolumePane.  |  
| PlotSeries | PlotIndicator\nPlotTimeSeries\nPlotBarHistory |  
| DataSeries sum = Sum.Series(Close, 10);\nDataSeries sumSma = Sum.Series(sma, 10);\nDataSeries.Abs(Close) | TimeSeries sum = bars.Close.Sum(10);\nTimeSeries sum = sma.Sum(10);\nTimeSeries abs = bars.Close.Abs(); |


