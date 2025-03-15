
# DataSets Tab

This view has an expanded interface of the Navigation view's [DataSets](DataSets) in the left sidebar.   The main pane to the right shows details for data in the local cache for each symbol in the selected DataSet. 

Use the DataSets view to: 
 - see details of each of the DataSet's symbols 
 - create new DataSets and configure existing ones. 
 - update all symbols in a selected DataSet for the selected Scale in one action by clicking the **Update DataSet** button
 - use **Data Tool** features in the lower tabs (see below)

### Update DataSet
Technically it's not required to manually update your data cache since Wealth-Lab automatically requests data when required.  However, in order to "seed" the cache for [scheduled updates](ScheduledUpdateTab), it's a good idea to Update a new DataSet to be sure symbology is correct and data are current and to make subsequent updates more efficient. 

%{color:blue}**Important!**% 
> After adding a DataSet, select the **Scales** of data you want to save locally and click **Update DataSet** after each scale selection to download data that you work with so that [Scheduled Updates](ScheduledUpdateTab) can update the cached data.

---
## Data Tool
The set of 4 tabs below the list of symbols is collectively known as the **Data Tool**. Use the Data Tool's features to perform operations on entire **DataSets** that would otherwise take considerable effort:

-   **Truncate last or first N bars**  (or  **N days**  of intraday  **data**)
-   Wipe the entire  DataSet data to **prepare for refresh**
-   Flag / Remove **inactive (dead) symbols**
-   Remove selected symbols
-   Remove **weekend and synthetic bars**
-   Fix OHLC **out of bounds**
-   Check  data for **validity**

### Symbols Tab
If allowed by the DataSet's Provider, use this view to **add or remove** symbols from the selected DataSet. (For example, pre-installed **WealthData** DAX, Dow 30, etc. cannot be modified.)  Removing a symbol does not delete its cached data.

### Data Truncation Tool
You may wish to **Truncate** data to prune an old history or to prepare to refresh data from a particular date. For example, if you find a gap in a symbol's data, truncate the data to the start of the gap in order to update the data from that point.

![Data Tool Data Truncation](https://www.wealth-lab.com/Images/WLHelp/DataToolTruncation.png)
 
Select the symbol(s) on which to operate and one of the truncate options.  Click **Select All Symbols** or use the Shift or Ctrl + click combinations for multi-select.  Choose one fo the Truncate options from theh dropdown.  **Delete N Days** is particularly useful to truncate recent intraday histories.

### Inactive Symbols Tool
Use this tool to **flag** (recommended) and then **remove** inactive symbols that have: 
- 0 bars of data, or, 
- no data after a specified date
 
![Data Tool Flag Inactive Symbols](https://www.wealth-lab.com/Images/WLHelp/DataToolInactiveSymbols.png)
 
%{color:blue}**Note!**% 
>Some DataSet Providers, like **WealthData**, may not allow you to remove inactive symbols, which are used for backtesting lists of historical index constituents. 

Inspect the flagged symbols and choose one of the removal options to remove the inactive symbols from the current or all DataSets.  

If you wish to preserve the data in the local cache, uncheck **Also Delete Local Files for Inactive Symbols**.  Leaving the data implies that the Historical Data Provider will continue to attempt to update these symbols during a [Scheduled Update](ScheduledUpdateTab). 

### Data Integrity Tool
The Data Integrity Tool quickly identifies where problems are (or might be) in symbol data, and where possible, can apply corrections.  To ignore alarms from older history that you may not be using, select a date from which to start testing. 

![Data Tool Data Integrity](https://www.wealth-lab.com/Images/WLHelp/DataToolDataIntegrity.png)

**Missing Dates**  
Attempts to identify days on which an instrument is *expected* to trade in its particular market but no data are present.  This test can generate many *false alarms* for instruments that have undergone trading halts or that were illiquid in their early history. 

Weath-Lab includes a list historical trading halts for listed Wealth-Data symbols and these will not be identified as missing dates. For other false alarms, please contact support with the **symbol, market, and date**.  We'll include them in the next update.

**Synthetic Bars**  
Some data vendors insert synthetic bars for days on which no trades took place (e.g. stock halt).  A synthetic bar is detected when: 
1. OHLC prices are the same and equal the prior bar's close, or,
2. OHLC precisely match OHLC from the prior bar. 

Synthetic bars can be removed by cleanup. 

**Weekend Bars**  
Trading on weekends is normal for currency, crypto, and some international markets.  If these instruments are properly identified in the [Markets and Symbols](MarketsAndSymbols) tool, they will **not** be flagged even when checking for weekend bar anomalies. 

Weekend bars can be removed by cleanup. 

**Data Spikes**  
Data spikes detect abnormally volatile moves in High and Low prices, i.e., spikes are seen as *long shadows* on Candlestick charts. The Data Tool cannot correct spikes and only identifies outliers for bars that **may not** accurately represent actual trading in the market.  Detections are discarded for bars whose volume is greater than 1.5 times the 5-bar moving average.  

The detection routine uses a modified average true range and allows for more and more volatility for prices below 10 down to 0.  To limit spike detections for penny stocks, enter a value below which to ignore.  
Checks for data spikes can generate hundreds (or thousands) of **false alarms**.  Many - even most - 'spikes' may represent actual trading. 

%{color:blue}**Notes**% 
- For U.S. Stocks, no spikes will be identifed for 6 May 2010, the date of the **flash crash**. 
- Wealth-Data scrubs tick data for trading outliers and automatically removes spikes.  For more info, see: https://www.wealth-data.com/faq


**OHLC Values with Zero**  
1.  OHLC are all the same as the previous Close and the Volume is 0
2.  OHLC are the same as the previous bar's OHLC and the Volume is 0  
    
**O/C outsite the H/L Range**  
Detects if Open and Close prices are outside the High/Low range of the bar.  During cleanup, the High and/or Low are adjusted to the previously-out-of-range Open or Close value. 

### Perform Data Cleanup
Select the flagged symbols to clean.  It's only possible to clean data that was downloaded by Wealth-Lab.  Other sources, like [ASCII](ASCII), external databases, etc., cannot be cleaned. 

The Data Tool takes no action for Missing Dates or Data Spikes. 
