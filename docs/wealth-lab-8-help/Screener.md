# Screener

 - [take me there now](action:Screener)

## Screener Basics
The Screener tool lets you use your existing Strategies to screen the market for opportunities using daily data. It runs your Strategy on the last bar of data only, allowing it to generate entry signals without processing an entire backtest. The Screener can operate in two modes, **Remote** or **Local**.
## Remote Screens
The Remote Screener submits your Strategy to a back-end service operated by WealthLab. You can use one of the pre-selected Universes of data, including the entire US Stock Market. Remote Screens can execute very quickly because our service keeps a year of data in-memory for the entire US stock market. However, the service does not support most extension libraries, or any third-party libraries you might be using in your Strategy. You have to stick to WealthLab.Indicators, WealthLab.TASC, or WealthLab.AdvancedSmoothers in a Remote Screen.

## Local Screens
Select a Local Screen to run the Screen on one of your local WL8 DataSets. Local Screens can employ all of the extensions and third-party libraries you use in your WL8 backtesting and development. 

[![Local Screener](http://img.youtube.com/vi/VRSNuGDoHXY/0.jpg)](https://www.youtube.com/watch?v=VRSNuGDoHXY&t=150s "Local Screener")

## Working with the Resulting Signals
The Screener results are presented in the standard Signals list. From there, you can **Stage** or **Place** Signals to the [Order Manager](OrderManager), or **Send** Signals to the [Quotes](Quotes) tool like always. You can also use the toolbar buttons to **Copy** long/short symbols to the clipboard or **Create** a [DataSet](DataSets) from the symbols. These options create a *unique* list of symbols, so the resulting number of symbols might be less than the number of Signals.

The **Position Size** control lets you quickly change the quantities of the Screener signals, based on the position size that you establish.

## No Signals
If a Screen returns no signals when you expect signals, it could be that the data has not yet updated. Certain data providers update daily data a few hours after market close, so try the Screen later.

## Demo Video

See this introductory video for a demonstration of the Screener in action:

[![New Screener Tool in WL8](http://img.youtube.com/vi/0kReX5qZkVU/0.jpg)](https://www.youtube.com/watch?v=0kReX5qZkVU&t=366s "New Screener Tool in WL8")
