
# Historical Providers

 - [take me there now](action:HistoricalData)

Historical market data is the life blood of Wealth-Lab, and you can access data from a wide variety of sources. Wealth-Lab uses **Historical Providers** to organize how historical price/volume data is served.

Whenever you view a [Chart](Chart) or backtest a trading [Strategy](Strategies), the source data comes from one of the **Providers** that you configured. In the [Chart](Chart) status bar, you can even see the Data Provider that supplied the current chart data.

![enter image description here](https://www.wealth-lab.com/Images/WLHelp/SelectedProvider.png)

---
## The Data Provider List
All installed Historical Providers are shown in the list. You can **disable** a Data Provider by unchecking it. The order of Providers in the list is important. Whenever it needs historical data for a symbol, Wealth-Lab goes top down, trying each of the *checked* Providers in the list one by one until it finds one that can provide the required data. You **can change the order** of the Providers by drag and drop.

**Checkmarks** 
- [ ] Q-Data
- [x] WealthData
- [x] IQFeed
- [x] CBOE
- [ ] Yahoo! Finance
- [ ] Alphavantage

Put checkmarks for the Providers that you want to be included in:
 - Historical data searches
 - [Scheduled Data Update](ScheduledUpdateTab)

### Symbol Mappings
This feature lets you support symbols unrecognized by a historical provider by assigning Symbol Mappings (on a by-provider basis). For more information, see Symbol Mappings in the [Order Manager topic](OrderManager). 

> For a demonstration, see this video on our YouTube Wealth-Lab Support channel: [![Symbol Mappings for Historical Data Providers](http://img.youtube.com/vi/WD0OrKW8uTM/0.jpg)](https://www.youtube.com/watch?v=WD0OrKW8uTM&t=186s "Symbol Mappings for Historical Data Providers") 

### Bulk Data Update
To update all data for a specific provider, right click the Provider and select **Perform Bulk Data Update**.  The bulk update will request updates for all DataSets linked to the provider as well as for the Provider's cached symbols in all scales. 

### Historical Data Loading Testbed
You can test the ability to retrieve data from the selected provider using this simple interface.  A successful load will show the number of bars and last date loaded.

### Data Provider-Specific Settings
Selecting a Provider shows Custom Settings, if any, that you need for login or any other configurable set up/action supported by the provider. 
### Delete Local Files
Certain Providers store their data in files on your local file system. For such Providers, you can right click and select the popup menu option to **Delete Local Files**. This deletes all of the locally saved histories, forcing the Provider to download completely fresh data when symbols are requested. You take this action if the service providing the historical data malfunctioned, leaving corrupted data files in your local store.
### Clear Tracking Info
This is another popup menu option for Providers that download data from a remote service. Internally, WL8 keeps a list of symbols that were requested, or that experienced errors when requested. Subsequent requests for these symbols silently fail to avoid lag during data loading. You can select this option to clear these internal tracking lists, or simply restart WL8 to clear them.
