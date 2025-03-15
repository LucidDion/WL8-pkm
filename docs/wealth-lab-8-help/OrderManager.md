# Order Manager

 - [take me there now](action:OrderManager)

The **Order Manager** is the single destination where all [Strategy](Strategies) **Signals** (also called **Alerts**) are sent.  A **Signal** is an indication to **Buy**, **Sell**, **Short**, or **Cover** a symbol, based on the execution of a [Strategy's](Strategies) trading logic.  **Signals** can come from the following sources:

 - Backtests in [Strategy](Strategies) windows
 - Strategies dropped onto [Streaming Charts](StreamingCharts)
 - Strategies dropped onto the [Strategy Monitor](StrategyMonitor)
 - Price Triggers in a [Quotes & Price Triggers](Quotes) window
 - Entered manually from the Order Manager's **trade ticket**

---
## Broker
The Order Manager supports multiple brokers connected simultaneously, organized in separate **Order Blocks**, also called **Signal Blocks** (see below). * broker and account selected at the top of the Order Manager is the destination for **Manual Orders.**  

In other Signal-generating tools, assign the broker/account before Staging or Placing signals using the appropriate control in the [Strategy](Strategies) Window Signals tab, [Streaming Charts](StreamingCharts) toolbar, [Strategy Monitor](StrategyMonitor) strategy item configuration, or the [Quotes & Price Triggers](Quotes) window.  

---
## Symbol Mappings
When a Data Provider's symbol does not match the symbol for the same instrument at your broker, assign Symbol Mappings.  Choose the broker and open the Symbol Mappings dialog by clicking the small button with circular arrow icons in the toolbar.  

You can create mappings using simple substitution or **RegEx** (regular expressions).  For a simple substitution, the Data Provider's symbol goes first, followed by an equals sign, followed by the broker's symbol.  
**Examples:**  
BRK/B=BRK B  
@ES#C=/ES

Indicate **RegEx** by enclosing the entire expression in square brackets. RegEx lets you create general rules so that you don't have to add substitions for every individual symbol. 
**Example:**   
Imagine your data feed uses a period separator for A and B shares  (e.g., BRK.B), but your broker uses a space, e.g., BRK B.  The following expression will substitute a whitespace wherever a period, backslash, or dash or appears in the symbol.
**[[\\.\\/\\-]= ]** 

---
## Signal Blocks
Whenever a set of **Signals** is generated, they get pumped into the **Order Manager** and into their own isolated **Signal Block**. The Order/Signal Blocks appear along the left side of the Order Manager, and you can enable to show or hide their Signals in the **Signals list** using the "Eye" button. You can remove a Signal Block and its associated Signals by pressing its **Remove Signal Block** button. You won't be allowed to remove a Signal Block that contains any active **Signals**.

---
## Toolbar
**Broker Connect / Configure / Account**  
Ensure your broker connection(s) before trading by connecting them here. Most brokers require a configuration, which is often shared with a broker's Historical and/or Streaming Providers. 

< %{color:blue}**Important**% 🚦 The selected Broker and Account are used for **Manual Orders**. Incoming Signals may be Staged or Placed for *any Broker*. >

**Symbol Filter**  
Quickly locate orders for a specified symbol by typing it in the Symbol Filter.  The Symbol Filter is disabled when **Show all Active Orders** is selected.

**Show all Active Orders**  
Enable this button to show only Active Orders.  Orders with other statuses (Cancel, Error, etc.) are removed from the list.  Enabling this option clears and disables the **Symbol Filter**. 

![Wealth-Lab 8 Order Manager](https://www.wealth-lab.com/Images/WLHelp/OrderMgrAccountsWL8B7.png)

---
## Signal Block Granularity

**Signal Blocks** are uniquely maintained on a [Strategy](Strategies)/[DataSet](DataSets)/Scale basis.  This means that if the same [Strategy](Strategies)/[DataSet](DataSets)/Scale combination generates new **Signals**, they replace the **Signals** that currently reside in that **Signal Block**. Active **Signals** (those already submitted to the **Broker** and current in **Active** status) follow these rules:

 - If the new batch of **Signals** does not include the active **Signal**, it is canceled.
 - If the new batch of **Signals** contains a **Signal** matching the active **Signal**, but with a different  **Limit**/**Stop** price, the active **Signal** is cancelled and replaced with the new **Signal** after the cancellation is confirmed.

**Show/Hide Orders**  
By toggling the signal block's eye icon, you can show or hide its orders. The **Show All Active Orders** button in the top toolbar has priority. 

Right click selected order(s) for options to **Place**, **Cancel**, **Edit**, etc.  Orders with inactive statuses like Cancel or Error may be Edited and Placed again.  

In the event that an status does not update, e.g., **CancelPending** does not transition to **Cancel**, you can remove the order(s) by right clicking and choosing **Kill Selected Orders**. Following this action, check your broker's web app for order status and take action if required. 

---
## Portfolio Sync
Please see preferences and guidance for synchronizing account Positions for live trading and other features in the [Trading Preferences](TradingPreferences) topic. 

1. Manual orders and those placed by the [Signals Publisher](SignalsPublisher) will not be synchronized with the broker account. For example, if you sell shares that you don't own, the broker may open a short position. 
1. Strategy signals that don't have a broker Position are entered with an "Error" status and not Placed with the broker.
1. The Signal block's **Show Auto-Traded Positions** is a list of Positions that could be *automatically exited* when the **Exit Orphans** [Trading Preference](TradingPreferences) is enabled.

---
## Special Order Types - MOO, MOC, LOC, and OCO
Please see preferences and guidance for special order types and other features in the 
[Trading Preferences](TradingPreferences) topic. 

### Market On Open (MOO)
A **Market On Open** order is a market order that participates in the primary exchange's opening auction and executes at that auction price. There is no special order type for MOO - it's a regular market order marked with a "OPG" time-in-force. Consequently, MOO is an option that can be used for end-of-day strategies that place market orders with brokers who support MOO. Using MOO will result in a NO SLIPPAGE fill at the primary exchange's (NYSE or NASDAQ) opening price. 

See Exchange rules for placing MOO orders. Currently, MOO must be placed before 09:25 AM for NYSE stocks and before 09:28 AM for NASDAQ. Exchanges will reject MOO orders placed after the deadlines.

> %{color:blue}**Note**%  
> Nearly all EOD providers use the *first full-lot trade on any exchange* as the opening price. Wealth-Data, however, uses the primary exchange's opening price. Click for more about [Wealth-Data](https://www.wealth-data.com)


### MarketClose and LimitClose
**MarketClose** and **LimitClose** are order types available in [C# Coded Strategies](CSharpCodeBased) intended to simulate MOC and LOC trading. MarketClose (MOC) execute at the settled closing price of the session. Similarly, LimitClose (LOC) orders execute at the settled closing price of the session if that price is equal to or better than the limit trigger price. 

For live trading, **Market On Close (MOC)** and **Limit On Close (LOC)** order behavior is  controlled by a group of [Trading Preference](TradingPreferences). Click to read more about the two behaviors for MOC and LOC orders depending on the selected [MOC Trading Preference](TradingPreferences).

> %{color:blue}**Note!**%   
> Current exchange rules indicate that MOC orders must be placed on NYSE or NASDAQ exchanges before 3:50 PM EST, after which time they are not accepted. Therefore, strategy or manual placement should occur before that time, and, **MarketClose Submit Minutes** should be greater than 10 minutes. 

### One Cancels Other (OCO) Orders
Also referred to as bracket orders, OCO orders are a pair of stop (stop loss) and limit (profit) exit orders placed simultaneously. When one of the orders is fully filled (or canceled), the broker will automatically cancel the opposite order. (For partial fills, brokers should adjust the number of shares in the opposite order.)

For broker OCO functionality, ensure that the [Trading Preference](TradingPreferences) *Use OCO When Possible* is checked. There are two ways to activate OCO orders in Wealth-Lab. 

#### OCO Manual Entry 
1. At the top of the Order Manager, select the Broker and Account.
2.  **Stage** two exit orders (Sell or Cover): a Limit (profit) order and a Stop (stop loss) order. The account must have a position for the number of shares entered. 
3. Select both orders using Shift+Click.
4. Click the **Place** button atop the order list (see below). 

If the stop/limit signals are **Auto-Staged** from a Strategy, the process is the same - use Shift+Click to select both orders and then **Place**. 

![Manual OCO Placement](https://www.wealth-lab.com/Images/WLHelp/ManualOCO.png)

#### Automated Entry
When the OCO [Trading Preference](TradingPreferences) is checked, strategies that Auto-Place stop and limit orders on the same bar will automatically get OCO functionality. 

< %{color:blue}**Important!**% 🚦Integrated brokers **do not currently support** *modifying* OCO orders. As the expense of a potential overfill, Strategies that need bracket order protection but that "move the bracket" should not enable the OCO [Trading Preference](TradingPreferences) to avoid hanging or unintended canceled orders. >
 
For brokers that do not support OCO orders, Wealth-Lab 8 includes built in OCO functionality for Auto-Placed orders. Following a fully filled order, Wealth-Lab will auto-cancel the opposite leg with the **Use OCO** [Trading Preference](TradingPreferences) enabled.

[![Auto-trading Order Cancelation Groups](http://img.youtube.com/vi/FRdM769yffI/0.jpg)](https://www.youtube.com/watch?v=FRdM769yffI&t=464s "Auto-trading Order Cancelation Groups")  

#### Auto-Trading Final Order (Last Bar of Session)
Some brokers immediately cancel day orders for the next session if they're submitted moments (or even minutes) after the market close. Orders placed for the final bar of the session are held in the Order Manager with status *FinalOrder*. They'll sit in the Order Manager until N minutes after market close at which time "Final orders" are placed. The default value for N is 15 minutes but may be configurable in the broker adapter.

- The Order Manager must remain open and connected with the broker to placed the orders after the [15-minute] delay. 
- *Enable Pre/Post Market Trading* must be disabled (unchecked) in [Trading Preferences](TradingPreferences) for the order to be accepted for the open of the next session. Otherwise, final bar orders will be placed for the post market session.

---
## Dummy Broker
WealthLab's Dummy Broker provides Manual and Auto-Trading *interaction* with a fictitious (paper-type) broker account. The Dummy Broker is installed with three accounts, and you can remove or add even more accounts by selecting the Dummy Broker atop the Order Manager and clicking *Configure...*

### Limitations  
You can use the Dummy Broker as if it were a real broker for testing and becoming familiar with Auto-Trading, however this simulated broker has limitations for accurate price fills and when trading MOC/LOC order types.

**How the Dummy Broker Fills Orders**  
The Dummy Broker uses the Streaming Provider's companion History Provider for data, primarily. Select your preferred Streaming Provider in the Order Mgr's toolbar. For the best results, select a Streaming Provider whose companion history provider returns data that is *not delayed*.

The Dummy Broker polls symbols with Active orders every few seconds for the current Daily partial bar - *a snapshot* - whose last price is used as the current quote to fill a simulated order. Market orders will fill immediately at this price. If the primary provider doesn't return a quote, the Dummy Broker will request a snapshot from the list of Historic Providers. 

**Limit and Stop Orders in the Dummy Broker**  
Because quotes aren't checked continuously, the Dummy Broker may not execute Stop or Limit orders when expected. It's possible to miss Stop or Limit triggers that "touch and reverse" in between the data requests.  

*Strategy code* always fill Stop and Limit orders whose trigger price is reached (assuming zero slippage) based on a `BarHistory`. However, if the market moves back within the trigger price at the time of the snapshot quote, the Dummy broker won't fill the order, which can cause an out-of-synch condition between the Strategy and the Dummy account. To alleviate this scenario when Auto-Trading with a [Streaming Chart](StreamingCharts) or [Strategy Monitor](StrategyMonitor), consider *Use Live Positions* in [Trading Preferences](TradingPreferences). 

**MOC/LOC Behavior in the Dummy Broker**  
The Dummy Broker does not support true MOC/LOC and therefore always uses *Behavior 2* described in the [Trading Preferences](TradingPreferences) for Special Order types, *Use MOC (Market-on-Close) when Possible*. 


### More Paper Trading Options  
For the best full paper-trading experience, we recommend using a paper account offered by your broker. An [Interactive Brokers](https://www.wealth-lab.com/extension/detail/InteractiveBrokers) paper account is excellent, or you can create a free paper account at [Alpaca](https://www.wealth-lab.com/extension/detail/Alpaca). Both act like real accounts, provide reasonably accurate fills, and the broker will track your Portfolio and trade history as if it were a live account.

