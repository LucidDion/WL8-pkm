# Streaming Charts
After opening a [Chart](Chart) window, your selected default [Streaming Data Provider](StreamingProviders) will be shown in the **Chart** toolbar. Depending on the symbol's market, you can select another provider from the dropdown list and turn on streaming by pressing the **Stream** button.

![Streaming Controller](https://www.wealth-lab.com/Images/WLHelp/StreamingController.png)


%{color:blue}**Important!**% 
> *Brokerage* streaming feeds (TDA, IB, etc.) are not tick-for-tick, so bars built by Streaming can have small 
differences when compared to a historical charts. On the other hand, a **Streaming Bar** option may be available
in the the [Strategy Monitor](StrategyMonitor) which can produce identical bars to historic charts at the expense 
of a few seconds more delay to generate trading signals.


---
## Pre and Post Market Data
By default, pre and post market data that is streamed is *excluded*. You can include pre and post market data by unchecking the **Filter Market Data** check box in the Chart status bar (bottom of chart window). The **Market** dropdown next to the filter lets you change the [Market](Markets). In this way, you can control that market open and close times that the streaming filter uses.

---
## Auto-Trading from Streaming Charts
**Streaming Charts** come with a toolbar of controls for destination *Account*, *Position Sizing*, and other buttons for manual trading. If a strategy is attached to a Streaming Chart, **Auto-Stage** and **Auto-Place** buttons are also added. The toolbar (non-Expert mode shown) and its buttons are identified in the image below. 

![Streaming Chart Toolbar](https://www.wealth-lab.com/Images/WLHelp/StreamingChartToolbar.png)

---
## Signals from Streaming Charts
If you dropped a [Strategy](Strategies) onto a Streaming Chart, the **Strategy** will execute whenever a new streaming bar of data completes a new interval. **Signals** generated are *pruned* and sent to the [Order Manager](OrderManager) if the **Auto-Stage** or **Auto-Place** button is enabled. Pruning eliminates superfluous orders, for example, a limit exit order signaled with an exit at market.

> Click for demonstration in this [Wealth-Lab Short video](https://youtu.be/uJY0bb0g1IA).

### Auto-Trading with Strategies
To trade a Strategy with a Streaming chart, attach a Strategy by dragging and dropping it into the chart and enable Streaming. Configure the Broker/Account and the Position Sizing to apply to the signals. Auto-Trade will automatically manage and place orders for Strategy-generated signals when a new bar is added to a chart's *BarHistory*. 

> **Important!** - Review and configure your [Trading Preferences](TradingPreferences) before Auto-Trading. 

***Auto-Place*** - sends any generated **Signal** to the [Order Manager](OrderManager) which automatically submits those as orders to the Broker/Account selected in the toolbar. The selected **Broker** must be **connected** in the [Order Manager](OrderManager).  

***Auto-Stage*** - sends the order to the Order Manager where it waits in a *Staged* status. To complete the order, you must manually select and *Place* staged orders. 

Once one or more Strategies are attached to chart windows and configured for trading, save the Workspace to quickly return to it in another session. Launching a Workspace with Auto-Trade enabled will *not* automatically place signals created for the last bar when the charts are initialized with data. 

[![Streaming Strategy Chart Window](http://img.youtube.com/vi/uJY0bb0g1IA/0.jpg)](http://www.youtube.com/watch?v=uJY0bb0g1IA "Streaming Strategy Chart Window")

%{color:red}**Warning!**%  
Streaming charts are **not refreshed** if the data feed disconnects occasionally. Keep this in mind when auto-trading.

> **Checklist: Auto-Trade from a Streaming Chart**  
> ☑ Check [Trading Preferences](TradingPreferences)  
> ☑ Open a chart and select the scale. Don't load too much history - enough to trade your strategy  
> ☑ Drag Strategy from from the list into the chart  
> ☑ Start Streaming - select the broker, account, and position sizing in the Streaming toolbar  
> ☑ Enable the Auto-Trade button  
> ☑ Save the Workspace 


## Manual Trading from Streaming Charts
Manual trading from Streaming Charts comes in two flavors: 
1. Live Order Lines (LOL)
2. Tradable Trendlines (TT and THL)

> **Important!**  
> Portfolio Sync [Trading Preferences](TradingPreferences) DO NOT apply to manual orders, including those described below. WealthLab does not resize manual orders.

### Live Order Lines
*Live Order Lines* (WealthLab's definition for *LOL*) are created using buttons J, K, L, and M in the Streaming Chart toolbar (image above). The checkbox (J) enables buttons K-N to place Buy, Sell, Short, and Cover for Market, Stop, and Limit order types. When enabled, these buttons will ***immediately place live orders*** with the Broker/Account using the Position Sizing configured in the same toolbar. When a Position for the charted symbol exists in the Account (B), clicking *Flatten* (N) immediately places a market order to exit the position. 

With the "eye" (I) button enabled, Stop and Limit orders appear on the chart as horizontal dashed lines (see image) and are placed in a Manual Order block in the Order Manager. An order summary (and status) appear on left below the line. LOL orders can be canceled in two ways:
- Click the 🚫cancel icon left of the order summary
- Cancel/Cancel All in the Order Manager

**Cancel and Replace** a LOL order at a different price level by dragging the line to a new location. The order will be ***immediately canceled and replaced*** upon releasing the mouse button. 

![Live Order Lines](https://www.wealth-lab.com/Images/WLHelp/LiveOrderLines.png)

 
### Tradable Horizontal and Tradable Trend Lines
Tradable Horizontal and [diagonal] Trendlines (buttons O and P in the toolbar) are based on their manual drawing equivalents with the added ability to generate Market orders when the most-recent closing price crosses (or simply closes) above or below the line.
 
Tradable lines apply to the chart for the symbol and scale in which they're drawn. If you duplicate a streaming chart for the same symbol and scale, a duplicate instance of the line(s) may be created and can result in a duplicate or additional order. 

 ![Tradable Trendlines](https://www.wealth-lab.com/Images/WLHelp/TradableTrendlines.png)  

When dropping a line, its Properties dialog gives you a chance to change color, line width and style, as well as these trading properties:
 - Value (price level) - Horizontal line only
 - Trade Type (Buy, Sell, Short, Cover)
 - Quantity - shares/contracts for the order, initialized by the Position Sizing control
 - Trigger when Price (Closes Above/Below,  Crosses Above/Below)  

> **Tip!**  
> If a line seems to be jumping unexpectedly when drawing it, uncheck **Snap to Price** in the line's Properties dialog

**Closes vs. Crosses**  
There is an important distinction between the options ***Closes*** and ***Crosses*** Above/Below.
 - ***Closes (Above/Below)*** - The Closing price of a new bar added to the chart is compared to the Tradable Line. If you choose *Closes Above*, the trade will trigger if the new bar's closing price is above the line's value at the current bar. It is *not required* for price to have traded below the line first. The reverse is true for *Closes Below*. 
 - ***Crosses (Above/Below)*** - *Crosses Above* triggers as soon as the *streaming quote* trades at or above the line *immediately following* a trade (quote) at or below the line's value at the current bar. The reverse is true for *Crosses Below*. 

 > **Example**  
 > Price is currently trading at 34.50 and you Activate a tradable horizontal line to trigger a trade when price *Crosses Over* 34.20. Since price is trading above 34.20, the line will not trigger immediately. However, as soon as a trade occurs at or below 34.20 *and then* at or above 34.20, the line triggers a trade and Deactivates itself automatically. 

Tradable lines can be moved and altered at any time, but caution is warranted when making changes to an Activated line with **Crosses (Above/Below)** since it's possible to instantly trigger a trade. Deactivate the line before making changes and reactivate it when you've verified its new position is correct.
 
< %{color:red}**Warning!**%  Tradable Trendlines drawn in one chart are active for every Streaming chart with the same **Symbol/Scale**. Therefore a line drawn in one chart can trigger the same order more than once - each one submitted to the broker/account specified in its Streaming window. >

**Activating / Deactivating Lines**  
New Tradeable Lines are initialized *Deactivated* from creating trading signals. Activate the line to enable trading by clicking the ▹triangle on the left of the line's description. Likewise, you can deactivate trading by clicking the 🚫cancel icon. Tradable lines are automatically deactivated following a trade trigger. 
 
To remove a line, click it to open the Properties dialog and click the Delete button. Additionally, the button to 🚫Remove all Chart Drawings in the Drawing toolbar will delete all drawing objects, including all Tradable Lines. 

[![Trading from the Chart](http://img.youtube.com/vi/x_71H9ra3SI/0.jpg)](http://www.youtube.com/watch?v=x_71H9ra3SI "Trading from the Chart")
