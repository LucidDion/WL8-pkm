# Quotes and Price Triggers

 - [take me there now](action:Quotes)

**Quotes/Price Triggers** (or simply **Quotes**) provides streaming quotes for symbols, and **Price Triggers** that can trigger **Limit** or **Stop** orders when prices reach a certain percentage of their order price. A default [Streaming Data Provider](StreamingProviders) will appear in the upper left corner, but you can choose a different provider from the dropdown control. 

**Quotes** provides a handy way to trade a Strategy that generates many more Limit/Stop orders a day than you could possibly submit to your Broker at one time. 

---
## Adding Symbols
You can enter one or more symbols manually or drag and drop a [DataSet](DataSets) into the symbol list to populate it.

---
## Adding Price Triggers
You can add a **Price Trigger** manually from the toolbar or send a group of **Price Triggers** into a new **Quotes** window from a Strategy Window's [Signals View](Signals) or the Strategy Monitor's [Signal Pane](StrategyMonitor). 

![Create price triggers in Quotes](https://www.wealth-lab.com/Images/WLHelp/CreatePriceTriggers.png)

---
## Managing Price Triggers
**Quotes/Price Triggers** submits orders only when the market reaches or is close to the trigger price as described below.

**Price Triggers** 
Price Triggers stream like plain quotes but also include either a **Limit** or a **Stop** order. You control when a **Price Trigger** triggers by setting a value in the **Trigger Threshold** field. Once the price reaches the specified *Threshold %*, the symbol *triggers* and the order and will be **Auto-Staged** or **Auto-Placed** if one of those options is selected.

**Trigger %**
Trigger % is a measure of how close the last (current) price is to the stop/limit price from the last close (see Note). Example: if yesterday's close was $10.00, and you have a buy at limit order for $9.00, Trigger % will be 50% when price is at $9.50, 75% at $9.25, and 100% at $9.00. 

<%{color:blue}**Note:**% If you enter Quotes/Triggers during market hours, the Trigger % basis is the first tick instead of the previous session's close.>  

### Auto-Stage, Auto-Place
If the **Auto-Stage** or **Auto-Place** option in the toolbar is turned on, Signals that trigger will be automatically sent to the [Order Manager](OrderManager).  ***Auto-Placed*** orders are submitted to the Broker without delay - assuming the [Order Manager](OrderManager) is **connected** to a Broker.  ***Auto-Staged*** orders have a "Staged" status in the Order Manager and must be selected and placed manually. 

> %{color:blue}**Note:**%  
> Loading a Workspace will enable Auto-Stage only. You must enable Auto-Place manually.  

<%{color:red}**Warning!**%  Auto-Place is designed to reduced a trader's workload to route orders to the market place with minimal delay. You should monitor automated trading and take appropriate manual action when necessary.>  

### Broker
Only one broker can be assigned per Quotes window. The selected broker will be used for manual Price Triggers. 

When you "Send [Signals] to Quotes Window" from a Strategy Window or the Strategy Monitor, a new Quotes Window will be opened and the broker is preassigned based on the selection in those signaling tools. Changing the broker in the Quotes Window reassigns existing signals to the new broker, but here positions will NOT be resized based on % of account equity if you're using that [Trading Preference](TradingPreferences). 

---
## LimitMove Orders
**LimitMove** is a special pseudo-order type you can use in [C# Coded Strategies](C#CodeBased). It causes **Price Triggers** to trigger only if price begins **outside** of the Trigger Threshold (at the time you start streaming data), and subsequently **moves** into that range.  LimitMove orders can help prevent a Strategy from entering a trade on extreme price events (gaps) following a press release or earnings report. 

---
## High/Low Daily Quote
When you select a Quote from the list, Wealth-Lab will attempt to lookup the current day's bar for the symbol, and if found, will display a quote containing the day's **high** price, **low** price, and **volume**, atop the Quotes window toolbar.
