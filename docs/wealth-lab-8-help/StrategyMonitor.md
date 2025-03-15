# Strategy Monitor

 - [take me there now](action:StrategyMonitor)

The **Strategy Monitor** allows you to store and run one or more Strategies on entire DataSets and set up each one with custom Strategy Parameters, data, scale, and sizing so that you can manage all **trading signals** from one location. The **Strategy Monitor** is a real-time tool that alerts with the *current trading signals* for each **activated** Strategy. It's not possible to access signals for dates/bars prior to the most recent date/bar.

Generally, the **Strategy Monitor** is used to run strategies on all symbols of a DataSet (or a symbol of choice) for live intraday trading. It can also be used to signal trades for Daily strategies, but there are differences with **Strategy Window** simulations and signaling as described below.

### Strategy Monitor vs. Strategy Window
The [Strategy Window](Strategies) provides true *Portfolio simulations* of a DataSet. The **Strategy Monitor** attempts to do the same but favors quickly *generating signals* over waiting for all updates to generate a precisely accurate equity curve. (See below: **Wait for all Updates before processing**.) Also, enabling **Use Broker-reported Account Value** in [Trading Preferences](TradingPreferences) lets you size *Signals* using your brokerage account value for equity-based sizing methods. 

**Strategy Window** 
1. Runs true Portfolio Simulations for detailed analysis. 
2. All Position Sizing methods and Advanced Settings are available for backtests.
3. Strategies can be added to a Streaming Chart Window. 
 
**Strategy Monitor** 

1. Gives priority to generating strategy signals quickly. However, you can enable *Wait for all Updates* to wait for all symbols to update before executing - a requirement for rotation-type strategies. 
2. Preferred for live intraday trading for small to large DataSets of symbols.
3. The **Strategy Monitor** has a *Streaming Bars* option for optimal intraday execution. (See *Scale and Data type * below)
4. Always attempts to acquired the most-recent complete end-of-bar data for the scale specified. The *End Date* is ignored for a *Date Range*. 
 
%{color:blue}**Notes!**%
> Before activating the strategy, we recommended checking **Retain NSF Positions** in [Advanced Strategy Settings](AdvancedStrategySettings) or including this statement in a C# Strategy's ```Initialize()``` method:
```
BacktestSettings.RetainNSFPositions = true;
```  

---
## Configure Strategies
Drag and drop strategies individually into the monitor's window and complete the configuration. 

![Strategy Monitor Settings](https://www.wealth-lab.com/Images/WLHelp/StrategyMonitorSettings.png)

### 1 - Select a DataSet or symbol
The Strategy Monitor works with DataSets but also supports trading one symbol. 

< %{color:Red} **Important!**%  After entering a symbol, strike the Tab key and ensure that the Market is correct (see 2.). >

### 2 - Market  
The Market affects scheduling the Next Run times. If the wrong Market is showing, choose the correct Market from the dropdown. 

< %{color:Red} **Important!**%  Your computer's clock must be synchronized properly with its Time Zone. >

### 3 - Settings
**Data Range** - should be made sufficient to initialize a strategy's indicators and allow it to enter current hypothetical positions so that it can provide exit signals. Loading an excessive number of bars will add delay to signaling/trading. Do not use "All Data" for intraday trading.

**Position Size**  
The Strategy Monitor runs strategies on a per-symbol basis. Equity-based sizers use hypothetical *backtest Equity* unless the Portfolio Sync % of Equity Sizing is enabled in Trading Preferences.

**Portfolio Sync - % of Equity Sizing**  
When Percent of Equity sizing is used, WealthLab applies the selected percentage to the ***brokerage account equity*** value for new trade signal sizes. To ensure exiting the correct number of shares/contracts, enable the appropriate Portfolio Sync [Trading Preferences](TradingPreferences). 

**Fixed dollar sizing**  
Fixed sizing is straightfoward without the need to rely on Portfolio Sync [Trading Preferences](TradingPreferences). If used, fixed sizing should be adjusted periodically to reflect sizes based on your actual Portfolio equity. 
 
%{color:blue}**Tip!**%  
Use *Portfolio Sync* options in [Trading Preferences](TradingPreferences) so that exit signal sizes match the account's actual Position size.

> %{color:blue}**Max Entry Signals - Note!**%  
> When using Max Entry Signals for intraday intraday trading in the Strategy Monitor, consider enabling the setting *Wait for all Updates before Processing* (below) to properly sort weights for all signals. 

### 4 - Intraday Scales and Data source  
1-minute bars are the minimum scale  (fastest) supported by the Strategy Monitor. 

**Streaming** - Most brokerage streaming feeds (TDA, IB, etc.) are not tick-for-tick. Bars built by these conflated tick streams will have small differences when compared to a historical charts. 

**Streaming Bars** - if available for the selected Streaming Provider (see 8.) Streaming Bars produce bars identical to historic charts at the expense of a few seconds more delay. This option is recommended for Providers that support it for all intraday intervals. Streaming Bars or Streaming should be used for intervals 5 minutes or less, especially for large DataSets. For a small number of symbols (6 or less), *Polling* may have better performance. 

**Polling** - requests bar data at the end of each interval and is generally recommended for 10 minute and higher intervals. However, if trading a large DataSet with providers that severely throttle requests (e.g, IB, Kraken, etc.), one of the Streaming options should be used for intraday trading to combat excessive signaling delay.

*Advantages to intraday polling:*   
- Bar data matches that in a historical chart.
- Polling is not affected by data dropouts during the interval.

### 4a - Daily+ Scales and Data source
For Daily+ scales (Daily, Weekly, etc.) specify the precise time to schedule the run after the market close. With almost no exception, **Polling** should be used for Daily+ scales. 

### 4b - At-Close Signaling (Daily, Polling only)
The *At-Close Signaling* option appears only when the Daily scale and Polling are selected. With *At-Close Signaling* the Strategy Monitor performs an extra run a specified number of seconds before the market close. This run uses specialized logic that attempts to load partial daily bar data and appends these partial bars to the daily histories. The extra At-Close Signaling run takes `MarketClose` signals that were generated on the last complete bar and submits them as `Market` orders.

< % Important!%  At-Close Signaling is always based on the *hypothetical backtest* and does not use Live Positions even when *Use Live Position* is enabled. To exit a broker position with the At-Close Signaling feature, the backtest must have an active (or NSF) Position on the last daily bar. >

The feature is intended to trade Daily Strategies that use `MarketClose` orders to enter or exit near the market close based on price and/or indicator values at the close of that bar. Since signals can only be placed for the *following bar*, Strategies that trade at the close of bar N, based on price/indicator values at bar *N*, have to place their MarketClose signals on the previous bar, *N - 1*, and use logic to "peek ahead" at *bar N* to determine if the entry/exit criteria were met. This At-Close Signaling feature lets you "live trade" such Strategies in the Strategy Monitor, and without it these Strategies could not generate signals and are not tradable.

In order to get the most accurate results, specify the smallest value possible for the number of seconds before market close. Since the market can move during those last seconds, the actual close might change after At-Close Signaling completes. However, you also must allow sufficient time for WL to obtain the partial bar values for all of the symbols being processed. Determining the ideal number of seconds will depend on the number of symbols being processed and the Data Providers employed. WL downloads partial bar data from the Providers enabled in the Data Manager > Historical Providers, in the order they are arranged.

### 5 - Wait for all Updates before processing
The Strategy Monitor default behavior is to allow the Strategy to process a run in **multiple batches**. Especially with illiquid markets and intraday trading, some symbols may experience significant lag in updating. Rather than hold up all of the DataSet symbols, the Strategy Monitor will execute a partial backtest on groups of symbols as their data becomes up to date. This ensures timely processing of Signals.

However, some Strategies rely on the complete DataSet being up to date before they can properly run. This is always the case with Rotation Strategies, which activates this option to disable the **multiple batch** processing. For other Strategy types, you can selectively disable the **multiple batch** behavior by checking this box.

When updates for the interval are not available for all symbols, the Strategy Monitor has a cutoff time to wait for updates at which time the run for the interval will complete, as follows:

| Update Type | Cutoff (seconds after the end of interval) |
| --- | --- |
| Polling | 40 |
| Streaming | 15 |
| Streaming Bars| 15 |

### 6 - Enforce Max Open Positions from Pos Size
Use this option to *Enforce* the maximum number of open Positions allowed on a per-Strategy basis. 

It takes the specified number to enforce, say 10, subtracts open positions in the broker account whose symbol matches a symbol in the backtest's open positions (including NSFs), adds `Market` exit signals, and subtracts `Market` entry signals. The threshold exceeded if the resulting number is below zero. 
- A market entry signal decrement occurs as the signals fill, so the threshold impacts the entries only when it's exceeded. 
- Stop and Limit orders also add to the open positions tally as signals fill.

To enable *Enforce Open Max Positions*: 
1. *Wait for All Updates* must be checked, and,
1. At least 1 of the 3 Max Open Position options must be greater than zero in the Position Sizer. 

< %{color:Red} **Important!**% *Enforce* works independently of the *Open Positions* threshold in Trading Preferences. Both will function if enabled. However, *Enforce* does not cancel open limit/stop orders as do the Trading Preference Thresholds. >

### 7 - Broker/Account
Optional for automated trading, choose the broker and account for signal routing and % of Equity sizing (see 3. above).

### 8 - Streaming Provider
Identify the Streaming provider if the monitor mode will use Streaming or Streaming Bars. 

### 9 - Strategy Parameters
If your Strategy implements parameters, use one the options below to assign their values for the Strategy Monitor runs. 
1. Adjust the parameter values using the sliders.  The sliders are ignored if one of the following options are enabled/checked: 
2. If you saved [WFO Results](WalkForwardOptimization), you'll be able to check **WFO** to use the set of optimized variables from the most-recent WFO interval, or,
3. If you assigned Preferred Values from a [Standard Optimization](StandardOptimization), check **PV** to use those values.

To see the WFO parameters, use **File > Open Saved Optimization File**. Alternatively, open the strategy and inspect for the Preferred Values tab to check PVs for specific symbols. 

## Upper Strategy Monitor Pane
Once configured, selecting a Strategy Item will enable the toolbar at the top with the following buttons:

**Activate** - When activated WealthLab updates and loads data. For best results with large DataSets, use the Data Manager's update functions before the market opens and before activation.  When loading is complete the **Next Run** is calculated and displayed in *local time*. 

- **Last Run** and **Next Run** are displayed in your machine's local time.  Internally, strategies consume intraday data in the market's time zone.
- To activate strategies when opening a Workspace, enable the Workspaces menu option: *Auto-Reactivate Strategy Monitor when Workspaces Open*. 

**Remove**  
De-activate a Strategy before attempting to remove it.  The Delete key will also remove an inactive strategy. 

**Configure**  
Click this button or double click an inactive strategy to return to the configuration dialog.

**Auto-Stage/Place**  
Either of these options automatically route signals to the [Order Manager](OrderManager).  

***Auto-Stage*** *stages/parks* orders in the Order Manager for review. You must manually select staged orders and click **Place** to submit them to the broker.  

***Auto-Place*** provides fully-automated trading with no user interaction required to fill orders. Auto-Place automatically places orders for new signals generated for a new bar added to a chart's BarHistory. Launching a Workspace with Auto-Trade enabled will *not* automatically place active signals created for the last bar.  

< %{color:red}**Warning!**%  Auto-Place is designed to reduced a trader's workload to route orders to the market place with minimal delay. You should monitor automated trading and take appropriate manual action when necessary. Strategies run hypothetically and trading may not be synchronized with live trading accounts. For Portfolio Synchronization options, see [Trading Preferences](TradingPreferences). >

**Send to Quotes**  
This setting causes generated **Limit/Stop** signals (only) to be automatically sent to an *Auto-Place-enabled* **Quotes window**. This feature is primarily intended to be used in conjunction with auto-traded Strategies at a daily scale, although intraday Strategies are supported with restrictions ¹. 

A change to Stop/Limit order prices on subsequent bars for the same Transaction/Order type will update the existing price trigger(s) in the Quotes window. When this happens a new reference price is calculated to keep the Trigger % at the same value. 

%{color:blue}**Send to Quotes - Important Notes**%  
1. The Quotes tool will use the Streaming Provider configured in the Strategy Monitor item.
1. Signals for Market orders are ignored and must be staged or placed *manually* from the Signals pane. 
1. OCO is *not supported*. 
1. *New!*  Multiple signals are supported on a per symbol basis if they have different Transaction or Order Types. For example, a strategy signaling to Sell At Stop and Sell At Limit will result in two price triggers orders the Quotes window. 
1. ***All price triggers in the Quotes tool are active until they are triggered or manually canceled***. 

> ¹ While useful in specific intraday scenarios, *Send to Quotes* does not fully support intraday strategies. A Limit or Stop order sent to the Quotes tool remains active until it is: a) replaced with a new price, b) filled, or c) canceled/removed manually. Synchronization with the Strategy will not be maintained. For example, when a Strategy cancels a signal, it is **not** removed from the Quotes tool. 

**View Log Pane**  
The Log Pane keeps a history of the messages that have appeared in the Status column. 

## Signals Pane
Signals (Alerts) for the selected Strategy are displayed here. Select signals to manually **Place** orders or **Stage** them in the [Order Manager](OrderManager). You can also send selected Stop and/or Limit signals from end-of-day systems to the [Quotes Window](Quotes). 

> Signal Date is shown using the market's time zone.

### NSF vs. Live Positions
#### Case 1: Live Positions - enabled
> Enable *Live Positions* in the [Trading Preferences](TradingPreferences) for the best synchronization with live broker positions. For this case the Strategy Monitor will generate exit signals live positions only. This means that if your live account does not have a position to match an active hypothetical strategy Position, the strategy will process the entry logic for that symbol. 

> While the *hypothetical backtest* is affected by a Strategy saved with the NSF Positions option enabled, for Case 1 only symbols with matching broker positions can generate exit signals. NSF Positions are irrelevant. 

#### Case 2: Live Positions - *disabled*; Strategy saved with [NSF Positions option](AdvancedStrategySettings) *enabled*
> For Case 2, Exit signals for NSF Positions from the *hypothetical* Portfolio backtest will be identified in the Signals pane. If not using *Live Positions*, we recommended checking **Retain NSF Positions** in [Advanced Strategy Settings](AdvancedStrategySettings) before activating the Strategy. 

#### Case 3: Live Positions - *disabled*; Strategy saved with [NSF Positions option](AdvancedStrategySettings) *disabled*
> Case 3 is not recommended for live trading since it's possible to have entered a live trade on a signal whose backtest position was rejected due to lack of buying power. The risk is that live trades may not be managed as expected.

## Saving the Strategy Monitor Setup
Save the configuration of the Strategy Monitor by creating and saving a [Workspace](Workspaces). Update and save the Workspace when you make changes. 

## Right click menu options
The first handful of selections mimic the buttons with the same name and are described above: 
- Activate / Deactivate
- Remove
- Configure
- Auto-Stage
- Auto-Place
- Auto-Send to Quotes Window

**Copy to Clipboard** - copies the table of Strategy Item information to the clipboard. 

**Run Now** - temporarily Activates the strategy item, updates with the latest data, and executes it. By default, the strategy will be de-activated following the run. To keep an Activated strategy item activated following **Run Now**, enable it in [Preferences > Trading > Miscellaneous Settings](TradingPreferences).

**Run all Daily+ Now** - same as Run Now, except that it executes *all Strategy Items* that are set up for Daily or higher scales (Weekly, Monthly, etc.). This is a convenient on-demand method to run all end-of-day strategies at once.

**Open in a Strategy Window** - opens the Strategy Item in a Strategy Window with the configured settings. 

**Refresh selected Strategies** - Code changes are not automatically used for Strategy items that are open in the Strategy Monitor. To use saved edits to a strategy during a WealthLab session, select one or more affected strategies, right click, and select this Refresh option. 

## Troubleshooting 
1. Do not attempt to use the Strategy Monitor with delayed data. Strategies execute only if symbols return up-to-date data.
1. Check the Strategy Monitor Log for run information. It's normal for illiquid instruments not to receive updates. However, if you're certain that updates should have occurred for an interval:
- open a chart and ensure that you're not receiving delayed data.
- check the streaming provider connection (if your selected either Streaming or Streaming Bars).
- check the Strategy Monitor's item configuration: the symbol's *Market* must be correct (#2 in the image).