# DataSets
- [take me there now](action:DataSets)

A **DataSet** is simply a collection of symbols. When you backtest a trading [Strategy](Strategies), you select what **DataSet** of data to test, in addition to the data scale, test period, and various other settings.

## DataSets and Providers
Wealth-Lab loads historical data using the historical data providers you configured in the [Historical Providers](HistoricalProvidersTab) list. You can have a single **Data Provider** configured, for example WealthData, and all of your **DataSets** will load their data from WealthData. Whenever it loads a new symbol, Wealth-Lab checks your configured **Providers** one by one until it finds one that can provide data for the symbol.

## Linking a DataSet to a Data Provider
Although by default, **DataSets** and **Providers** are not linked, you can associate a **Data Provider** with a **DataSet** at the time you create the **DataSet**. If you select this option, Wealth-Lab will attempt to load data for the **DataSet's** symbols from the specified **Data Provider** before trying the other **Providers**.

## Auto-Created DataSets
When you create a multiple-instance [Data Provider](HistoricalProvidersTab), such as [**ASCII**](ASCII) or **Metastock** format, Wealth-Lab will automatically create a **DataSet** that contains all of the symbols available in the **Data Provider**.

## DataSet Providers
Some **DataSets** are created by Wealth-Lab itself, or [Extensions](Extensions) via a mechanism called **DataSet Providers**. These **DataSets** appear in their own nodes in the DataSet tree.  

### Hide DataSets
You can hide the preinstalled DataSets created by various data providers (except Wealth-Data's). This will also 
make them disappear from the "Select Backtest DataSet" dropdown in Strategy Settings. To do it, right click on 
the DataSet Provider you want to hide.  To restore a hidden DataSet provider, click on the eye icon nearby "New DataSet" button.

## Wealth-Data DataSets
A prime example of a **DataSet Provider** is **Wealth-Data**. The DataSets supplied by **Wealth-Data** contain the symbols in various well-known indices such as the Dow 30, S&P 100, NASDAQ 100, German MDAX and many more. 

## Dynamic DataSets

The WealthData DataSets mentioned above are ***dynamic***. When you backtest using a **dynamic** DataSet, you will only see trades for symbols that actually were in the index on the signal date. These dynamic DataSets also contain history for the delisted stocks. This eliminates the danger of **survivorship bias** from tainting your backtest results.

You can create your own dynamic DataSets in the New Dataset Wizard. One of the Wizard configuration pages allows you to make your DataSet dynamic, and provides an interface for you to enter a list of start and end dates for symbols that require dynamic date filtering during backtesting.

[![Create your own Dynamic DataSets](http://img.youtube.com/vi/5KlRRpMyVE8/0.jpg)](https://www.youtube.com/watch?v=5KlRRpMyVE8&t=223s "Create your own Dynamic DataSets")

## Clicking DataSet Symbols
You can expand a DataSet node in the tree to see all of the symbols it contains. When you have a [Chart](Chart) 
window open, clicking a symbol in the tree loads that symbol into the chart. When you have a [Strategy](Strategies) window open and it is set to single-symbol backtesting mode, clicking a symbol in the tree runs the Strategy on that symbol.
