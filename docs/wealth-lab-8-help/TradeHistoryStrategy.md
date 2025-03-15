# TradeHistory Strategies

 - [take me there now](action:TradeHistoryStrategy)

You can use **TradeHistory Strategies**, the simplest of all strategy types, to analyze trading 
histories exported from your broker or any other list of trades. Wealth-Lab will recreate the trades so that you can analyze them like any other backtest. 


![Trade History Strategy tool](https://www.wealth-lab.com/Images/WLHelp/TradeHistoryStrategy2.png)


[![Strategy Type - Imported Trade History](http://img.youtube.com/vi/90SDtgaGrAI/0.jpg)](https://https://www.youtube.com/watch?v=90SDtgaGrAI&t=10s"Strategy Type - Imported Trade History")


### Data
Wealth-Lab obtains data in the order of Provider precedence defined in the Data Manager > 
[Historical Providers](HistoricalProvidersTab). TradeHistory strategies will automatically adjust historical trades for splits, but you must ensure that an [Event Provider](EventProvidersTab) with Split data is enabled. 

It's *expected* that somes trades can and will fill *outside* of a bar's range for one of a number of reasons, some of which are:
 - Trade executed after hours outside the daily session range.
 - Odd lot trade (under 100 shares) outside the bar's range.  Charts include only full lot trades.
 - Position bought or sold due to option exercise.

### Configure and Backtest

 1. Launch a **TradeHistory** Strategy
 2. In the **Designer** tab, choose the File location that contains the trade history.
 3. Select the trade file Parser. Parsers are available for known data formats for some brokerages. Follow instructions shown in these parsers to download the trade file.  You can also supply your own ASCII format specification for a trade file. 
 3. If required, use *Offset Intraday Hours* to adjust the file's trade time to match the time zone for the data from the Historical Data Provider, which is usually the market's time zone.
 4. On the [Strategy Settings](StrategySettings) tab set an appropriate Data Range to cover the trades to analyze.
 5. Set the **Starting Capital** and Position Size.  If the trade file contains trade quantities, Position Sizing settings are ignored.
 6. **Run Backtest**

%{color:blue}**Note!**% 
> TradeHistory strategies run with [Retain NSF Positions](AdvancedStrategySettings) enabled and is not optional.
