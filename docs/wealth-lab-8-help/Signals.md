# Signals (a.k.a. Alerts)

After running a Strategy on one symbol or a set of symbols, all trading signals appear in a **Signals** view. Signals - also called "Alerts" - are *notifications* for an order to be placed in the market for the next bar.  

%{color:blue}**Note!**% 
> Signals only appear for transactions that will occur on a future bar and do not refer to historical or past hypothetical trades created by a Strategy.

---
## Signal Management
Signals can be Staged or Placed to the [Order Manager](OrderManager) to the Broker/account you select in the toolbar.  If *Not Connected* or an *account* is not showing, open the Order Manager and **Connect**. 

**Select All** signals using the button, or, select just the signals you want to work with.  A left mouse click in combination with Shift or Ctrl keys will select multiple rows or single items, respectively. 

---
### Stage and Place
**Stage Orders** transfers the selected signals to an Order Manager Order Block with a "Staged" status for the selected broker.  A Staged order can be edited by double or right clicking before Placing it. 

**Place Orders** works the same as Stage Orders without the ability to edit.  Orders are placed immediately with the selected broker. 

---
### Send to Quotes Window
To trigger Limit and Stop signals for end-of-day Strategies at or nearly at a marketable time, send the group of limit/stop signals to the [Quotes Window](Quotes).  When the market approaches the trigger price, the Quotes Window can trigger and Stage or Place the order automatically. 

---
### Auto Stage, Auto Place
When running a Strategy in a Streaming Window or in the Strategy Monitor, selecting Auto Stage or Auto Place will automatically Stage or Place orders at the moment they are triggered. 

---
### Signals for NSF Positions
To assist with order placement for primarily end-of-day Strategies that 
[Retain NSF Positions](AdvancedStrategySettings), exit signals for NSF Positions are marked as 
shown in the image. Although NSF Positions are not included in backtest results, it's possible 
that a live account that isn't synchronized with the backtest Positions could have filled one of these Positions that the backtest rejected. For this reason, all exit signals are shown when [Retain NSF Positions](AdvancedStrategySettings) is in use. 

![Signals View with NSF Exits signals](https://www.wealth-lab.com/Images/WLHelp/NSF_Exit_Signals.png)

### Signal Time in Force (TIF)
Strategy Signals for daily and intraday scales are submitted to brokers with a "Day" Time of Force. Strategies run on weekly or higher scales are submitted with a Time in Force of "Good til Canceled."

%{color:blue}**Note!**% 
> WL8 does not cancel Good til Canceled Strategy orders from Weekly or higher scales. Be sure to manually cancel any open orders over the weekend.
