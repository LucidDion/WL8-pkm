# Charts
 - [open a Chart now](action:Chart)
 
 Charts are populated with historical price/volume data provided by the **Providers** that you configured in the Data Manager's [Historical Price/Volume Providers](HistoricalProvidersTab) interface. Wealth-Lab attempts to get the data from the **Data Provider** you have linked when creating a DataSet and then one by one, in the order you defined in the Data Manager's **Historical Providers** view. The amount of data that is loaded into a chart is controlled in [Chart Preferences](ChartPreferences). 
 
 ---

 ## Chart Toolbar
In the toolbar, you select the **symbol** to chart, the data **scale**, and the **chart style** (candlestick, bar chart, etc.). You can also control several cosmetic settings such as **linear**/**log** **axis**, **bar spacing**, and the selection of a **vertical** or **crosshair cursor**.  Use the buttons to show/hide  Events (e.g. Fundamental Items), the chart's status bar, and even the toolbar itself. 

Hiding the Chart Toolbar enables **auto show/hide**.  Once the toolbar is hidden, move the mouse to the top of the chart area to show it again.   **File > Expert Mode** enables auto show/hide by default. 

%{color:blue}** Expert Tip!**% 
> Hold the **Alt key** while toggling a show/view button will apply the change to all open chart windows in the workspace. Also, you can synchronize the crosshair cursor across multiple charts in the same window by holding down the **Alt key** while clicking the crosshair cursor toolbar button.

[![Synced Crosshair Cursors](http://img.youtube.com/vi/wKFMoJXyC98/0.jpg)](https://www.youtube.com/watch?v=wKFMoJXyC98 "Synchronize the crosshair cursor across multiple charts")

---

## Chart Status Bar
The status bar provides several important pieces of information, including the number of data points charted, the **Data Provider** that supplied the chart data, and the associated [Market](Markets). In [Streaming Charts](StreamingCharts), you can also filter pre and post market data in the status bar.

---
## Chart Drawings
The toolbar along the right edge of the Wealth-Lab main window contains numerous **Chart Drawings** that you can use to annotate the Chart. Your drawings and annotations are automatically saved by symbol/scale.

---
## Indicators
You can drag and drop **Indicators** from the [Indicators](Indicators) list onto a Chart. To edit or delete an **Indicator**, left click its descriptive label along the top edge of the chart pane. You can also drop an **Indicator** atop another **Indicator** to use the target Indicator as the source of the newly plotted one. For example, drop a **Simple Moving Average** (**SMA**) on top of a **Relative Strength Index** (**RSI**) to create a smoothed RSI.

---
## Indicator Sets
The drop down at the right end of the toolbar contains **Indicator Sets** that you previously defined. **Indicator Sets** let you save groups of [Indicators](Indicators) that you drag and dropped onto the chart in a named set. Use the green check-mark button to save a new **Indicator Set** after providing a name. Once you have a few **Indicator Sets** saved, you can use the drop down menu to quickly switch between your preferred indicators on any chart.

---
## Visual Data Editing
If you encounter a spike or similar erratic bar on the chart, it can be fixed by right clicking the bar, choosing **"Edit bar data"** and entering correct OHLC data. Likewise, **"Apply a stock split"** lets you add a stock split if it was missed by data vendor. Just click the first bar of data that was already correctly adjusted for the split before choosing the option and enter the split factor.

[![Edit data from chart](http://img.youtube.com/vi/FRdM769yffI/0.jpg)](https://www.youtube.com/watch?v=FRdM769yffI&t=19s "Edit data from chart")

---
## Strategies and Auto-Trading
You can drop a **Strategy** from the [Strategies](Strategies) list onto a Chart. The **Strategy** will execute whenever you change symbols or when a new bar completes in a [Streaming Chart](StreamingCharts). While Streaming, generated **Signals** can be sent to the [Order Manager](OrderManager) by enabling Auto-Stage or Auto-Place buttons, providing the powerful ability for Wealth-Lab to automatically trade your **Signals**. 

%{color:red}**Warning!**%  
> Auto-Trading is designed to reduced a trader's workload to route orders to the market place with minimal delay. You should monitor automated trading and take appropriate manual action when necessary. Strategies run hypothetically and trading may not be synchronized with live trading accounts. >

---

%{color:blue}**Tip!**% 
> Set up and save a [Workspace](Workspaces) of your Strategies in streaming charts to quickly load a trading environment.



