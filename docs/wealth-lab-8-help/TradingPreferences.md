# Trading Preferences

 - [take me there now](action:TradingPreferences)

## Portfolio Sync
The first two Portfolio Sync preferences help to ensure that exit sizes from Strategy signals match the size actually held in the destination account.  Consequently, these options apply to orders created from Strategy signals and *do not apply to Manual Orders* typed in the [Order Manager](OrderManager).  

#### ☑ Block Exit Orders when Position not Found
Enabling this preference prevents placing an exit order if the Position is not found in the broker account for Auto or Manual trading. For example, it prevents creating unwanted short positions when a backtest signals to sell a positions that your account doesn't own. In this case, the Order Manager will show an **Error** - "Could not find a matching Position to exit."

#### ☑ Reduce size of Exit Orders to match Position Quantity
With this option enabled, exit Signals that are sized larger than the brokerage account Position will automatically be reduced in size when Staged or Placed to match the Position. If the size is smaller than the Position, this option has no effect, and therefore may be useful to exit a Position in various lots.

#### ☑ Always set Exit Order Quantity to full Position Quantity
This option causes exit Signal sizes to match the brokerage account Position when Signals are Staged or Placed. 

#### ☑ Use Broker Account value for Equity-based PosSizers
When this option is enabled Wealth-Lab replaces the backtest Equity value with the actual brokerage account equity when a **Position Sizer** requires an equity value to size **Signals (Alerts)**. This allows **Position Sizers** to size new positions using real account values. 

> **Note!** This preference is not applicable to [Meta Strategies](MetaStrategy).  

%{color:blue}**Important!**%  
1. When using **Broker-reported Account Value**, you should select **Reduce size** and/or **Always set Exit Order Quantity** so that a position's exit size matches the live account's position. Otherwise the exit could result in either under or overselling a position. 
2. For multi-currency backtests and trading, the account value is converted to the trade currency so that equity-based sizing reflects the specified percentage of the account value. Set the account's base currency in [Backtest Preferences > Other Settings > Multi-Currency](BacktestPreferences). 

%{color:blue}**Notes**% 
1. Assigning Transaction.Quantity in a script is a manual override and cannot access brokerage equity. UserStrategyBase's *CurrentEquity* property, if used, always returns backtest equity. 
2. If the starting capital is considerably less than the broker-reported value so that some Signals failed to generate, the adjustment does not apply by design. This means that regardless of the live account equity value, the backtest equity must be sufficient to generate a signal. 
3. Portfolio Sync options do *not* apply to manual orders or orders placed by the [Signals Publisher](SignalsPublisher).

%{color:blue}**Example**% 
>Strategy Settings Position Sizing is set for an account value of $100,000 and 10% sizing, however, your brokerage account 
>has $80,000. The backtest will size hypothetical positions using the backtest equity curve based on $100,000 (nominally 
>$10,000 positions) but 10% of the broker-reported $80,000 ($8,000) will be used when sizing the Signals for new Positions. 


#### ☐ Exit Orphan Positions at Market

%{color:blue}**Note!**% 
> This preference and Use Live Positions described below are mutually exclusive. If you enable Exit Orphan Positions, then Use Live Positions will become disabled.

This preference allows Wealth-Lab to track the Positions that were generated during auto-trading, and if they do not exist in the broker account in subsequent runs of the backtester Strategy, they'll be automatically closed. This handles cases of a Position being filled in real life, but not in the backtest.

An *Orphan Position* is a broker account position created by Auto-Trading but that remains in the account after the strategy has exited its *hypothetical* (backtest) position. Enabling **Exit Orphans** instructs Wealth-Lab to detect and exit *Orphans* using a **market order** while Auto-Trading. All of the following conditions are required:  
1. The position was created by Auto-Trade during the Wealth-Lab session. 
2. The position was **fully filled**. No orphan exits for partial fills.
3. Shares are found in the broker account but not in the strategy following a hypothetical exit.

< %{color:red}**Warning!**%  The market order exit for an orphan position could take place at a *far worse* price than the strategy's hypothetical exit at the limit/stop price. The tradeoff of enabling **Exit Orphan Positions** favors keeping the strategy in sync with the broker account at the expense of potentially unfavorable exit prices. >

Below are a few **expected** scenarios: 

**Scenario 1: No Fill at Limit/Stop Price**  
An orphan may occur while exiting a position when price hits a limit target, but the live position fails to exit. Similarly, depending how the broker triggers stop orders, it's even possible that price hit a stop but the order to exit is not triggered, creating an orphan. 

**Scenario 2: Same Bar Exits**  
Strategies that enter using a stop or limit order and use same bar exits by assigning values to a Transaction's ```AutoProfitTargetPrice``` and/or ```AutoStopLossPrice``` are at risk of an Orphan exit if the entry bar's range covers either price. To avoid an undesired Orphan, we recommend not assigning ```AutoProfitTargetPrice``` on the entry bar when using a limit order entry. Likewise, assigning ```AutoStopLossPrice``` for entries using a stop order also risks creating an orphan at the end of bar. 

**Scenario 3: Odd Lot Entry Fills**
Charts are created only from full-lot fills, which are trades with 100 shares or more. Odd lots, trades with fewer than 100 shares, do not appear in charting, so a strategy is blind to those transactions. If you trade odd lots, it's possible to enter a limit/stop trade without the strategy filling the hypothetical order if trigger price did not appear in the chart data. In this case, **Exit Orphans** would flatten the odd-lot position at the end of the interval to keep the account in sync with the strategy. 

**Scenario 4: Odd Lot Exit Fills**
Not an orphan scenario, but like Scenario 3, an odd-lot order filled in the account at stop or limit may not occur for the hypothetical strategy position, which remains intact. Later you can expect exit order *errors* because the strategy can no longer sync with an account position. 

< %{color:red}**Warning!**%  *Manually canceling* auto-trade stop/limit exit orders does not deactivate Orphan exit logic. Wealth-Lab will exit the account position at market after the strategy hypothetically exits the position even after having manually canceled exit orders. >

[![Sell Orphan Positions](http://img.youtube.com/vi/0NdXa8aZQ3A/0.jpg)](https://www.youtube.com/watch?v=0NdXa8aZQ3A&t=465s "Sell Orphan Positions")


#### ☑ Use Live Positions

> %{color:blue}**Note!**%  *Use Live Positions* and *Exit Orphan Positions* are mutually exclusive. Enabling *Use Live Positions*  will disable *Exit Orphan Positions*. 

 *Use Live Positions* instructs WealthLab to manage exits for open positions reported by the broker in [Streaming Charts](StreamingCharts) and the [Strategy Monitor](StrategyMonitor) with Strategies. This can be a good way to keep your live trading in sync with your live account for common scenarios like:
 1. keeping a limit order strategy in sync when the limit price was "touched" but your account position did not exit.
 2. exiting a discretionary (or any) position with a Strategy. 
 
The preference works by interrupting the backtester's execution on the last bar of data being processed. WealthLab then removes any theoretical open positions that the backtester has generated. It queries the associated broker and account, and injects the live position returned by the broker. It then executes the strategy logic on the remaining bar of data, allowing the strategy to issue exit orders for a live position. In effect, this preference moves the backtester from the purely theoretical realm into your trading reality.

The backtester remembers the bar on which the live positions were first queried and will retain a memory of the live trades as the intraday trading session progresses. On a [Streaming Chart](StreamingCharts), trades that were the result of live broker positions are highlighted with a circle. You can clear WealthLab's memory of live positions using the **Clear Saved Live Positions** button.


 There are several important factors to consider before enabling *Use Live Positions*, and not all strategies are compatible.  See **IMPORTANT considerations** below. 

![Demo Use Live Positions Scenario](https://www.wealth-lab.com/Images/WLHelp/LivePositionsNotInSync.png)

%{color:red}**IMPORTANT considerations:**%  
 - Avoid creating discretionary/manual trades on symbols Auto-Trading with Live Positions. It could cause Live Position synchronization to fail. 
 - Brokers typically report only one position for each symbol. So, this approach might not work as expected for strategies that are managing multiple positions per symbol.
 - Strategies that rely on timing the exit of trades might not work as expected. This is because the broker does not report an "entry date" for a position, so WealthLab does it's best by assigning an entry date based on the most recent bar of data that can accommodate the price that the broker position was established.
 
 *Use Live Positions* is **not compatible** with:
 1. *pair trading strategies* - or more generally, trading external symbols.
 2. trading multiple positions for the same symbol.
 3. the Strategy Monitor's [At-Close Signaling](StrategyMonitor) feature, which uses backtest positions only. 
 4. strategies that use WealthLab's `CloseAtTrailingStop()` signal. It will work if the backtest positions are actually in sync with the live positions, but it's best to control the Trailing stop price in a C# coded strategy and pass that price to `ClosePosition()` with `OrderType.Stop`.

 Click the image for a live demonstration.  
 [![Use Live Positions](http://img.youtube.com/vi/S8fRB9v0F3c/0.jpg)](https://www.youtube.com/watch?v=S8fRB9v0F3c&t=437s "Use Live Positions")

---
## Trading Thresholds
This section contains several **Trading Thresholds** that, when enabled, WealthLab checks whenever a Signal is ***Auto-Placed***. If the Threshold condition has been met, the Signal is *Staged with an Error* in the [Order Manager](OrderManager) rather than directly *Placed*. Use this feature to limit the amount of trading that can automatically occur. 

You can exclude an account from participating in **Trading Thresholds** by enabling that option for the broker account in the [Accounts](Accounts) tool. 

< %{color:red}**Warning!**% Manually placed orders do not check **Trading Thresholds,** and are always *placed* directly with the broker. >

### Default and Broker-Specific Settings
When the **Specific Broker/Account** check box is checked, you can specify Trading Thresholds that should apply to a particular account only. Any accounts that are not specified in this way will adopt the Trading Threshold settings specified when the **Defaults** check box is checked.

#### ☑ Account Buying Power Below
This Threshold is met when any account's **Buying Power** falls below the value you specify.

#### ☑ Account Cash Below
This Threshold is met when any account's **Cash** falls below the value you specify.

< %{color:red}**Warning!**% Some broker implementations do not provide values for **Buying Power** and/or **Cash**. Check the [Accounts](Accounts) tool to see if these values are listed. If the broker does not provide a value, the corresponding **Trading Threshold** is ignored for accounts belonging to that broker. >

#### ☑ Open Positions
With this checkbox enabled, WealthLab will not place new orders and also cancel any outstanding orders if an account already has the number of open positions. The Open Positions threshold *cannot be used* for trading Rotation Strategies. 

#### ☑ Number of Entry Orders Filled Exceeds
This Threshold is met when the specified number of entry (buy or short) orders have been filled during the current WL8 session. Below this option is displayed the current number of filled entries. You can reset this counter back to zero by pressing the **Reset Counter** button. The Entries Filled counter is global in nature, so fills in different accounts will increment the same global counter.

#### ☑ Pattern Day Trader
This Threshold is met when the account value is below $25,000 and there have been 3 day-trades within the past 5 trading days. WL8 considers an entry and an exit for the same symbol on the same trading day a day-trade. WL8 maintains a local trade history of fills to track these day-trades. Click the **Clear History** button to clear this local trade history for ***all accounts***.

#### ☑ Pattern Day Trader
Enabling the *PDT* option prevents placing trades that would open new positions when 3 *day trades* have already filled in the account in the past 5 trading sessions - but *only for accounts whose value is already below $25,000* to prevent the account from being flagged for *PDT*. WealthLab counts the day trades from its local transaction log only. Click **Clear History** to delete the local transaction log. 

#### ☑ Cancel all open Entry Orders when a Trading Threshold is hit
When *Cancel all* is checked, all Active orders for the corresponding account will be automatically cancelled. 

### Pre-Threshold Signal Blocking (Strategy Monitor only)
Trading Thresholds are a function of broker-reported values for cash, buying power and/or trading fills. They prevent new trades only *after* a threshold has been exceeded. However, WealthLab will *predict* exceeding Open Positions, Cash, and/or Buying Power Thresholds (if enabled and in that order) and *block* **At Market** entry orders that would result in exceeding a threshold. Also, **At Market exits** can increase the "credit" for new entries - see Example below.

**Notes:**  
1. *Pre-Threshold* works for the Strategy Monitor only. For expected results, the Strategy Monitor item should be configured to "Wait for all Updates Before Processing".
1. When trading instruments in currencies other than your account's base currency, enable Multi-Currency in [Backtest Preferences](BacktestPreferences). "Base Curr" should be set to the currency used by the broker to report Account Cash and Buying Power. 
1. A Market entry signal for a symbol with an existing position in an account will add shares to that position, cancelling another potential open position. For this edge-case example, Open Positions Threshold is set to 2 and the account is holding 1 position in IBM. A new group of 5 entry signals includes another entry for IBM, which has the greatest Transaction.Weight. This new entry for IBM is selected to fill the "slot" for the second position, and all other signals are rejected. The account will remain with 1 position in IBM, which now had added shares from the new trade.

%{color:blue}**Example**%  
- A trading account is holding 3 Positions, and, 
- the *Open Positions Threshold* is enabled and set to 5.  
Using the Strategy Monitor to trade the Nasdaq 100, a strategy signals to Sell At Market one of the 3 existing positions and Buy 4 new positions At Market. Since the account will have only 2 positions when the Market Sell is filled, there is room for 3 *At Market* entries. The entry with the lowest Weight will be blocked, i.e, not Placed.

[![Trading Thresholds](http://img.youtube.com/vi/b4nYRHdHfU4/0.jpg)](https://www.youtube.com/watch?v=b4nYRHdHfU4&t=255s "Trading Thresholds")

---
## Max Risk Percent Settings

☑ Automatically issue a Stop Loss Order
☑ Adjust Stop Loss Level bar-by-bar Trading

See the help topic [Max Risk Percent](MaxRiskPercent) position sizing for more details about these settings.

---
## Special Order Types
#### ☑ Use OCO (One-Cancel-Other) when Possible
Orders (especially Stop and Limit exit orders) that are placed at the same time will be attempted to be placed OCO. Two chain-link icons will appear next to an Active OCO order pair. The first order to execute will automatically cause the companion order to be canceled.

To place OCO orders **manually**, **Stage** two orders, **Select** both using the Ctrl+Click multi-select technique, and then **Place** the orders. Buy/Short OCO entries may be allowed, depending on the order type and receiving broker.

When **Use OCO** is enabled but not supported by the broker, Wealth-Lab will simulate OCO functionality when one order is **fully filled** by canceling the opposite leg. 

< %{color:blue}**Important**%  Integrated brokers **do not currently support** *modifying* OCO orders. Wealth-Lab handles this situation by canceling the old OCO and re-submitting both orders as a new OCO. >

#### ☑ Use MOO (Market-on-Open) when Possible
MOO orders allow your end-of-day market order to participate in the opening auction. MOO orders will fill at the primary market's opening price (the price Wealth-Data uses for Open) instead of some random market price. 

%{color:blue}**Notes**% 
> 1. You must place MOO orders for stocks (and CFDs) prior to 09:28 AM ET on a market trading day. 
> 2. Especially for staggered NYSE openings, it's possible for a stock to trade on electronic exchanges for several minutes before the NYSE primary market opening print, the moment at which MOO orders are filled.


#### ☑ Use MOC (Market-on-Close) when Possible
**Behavior 1: Use MOC - enabled**  
Broker providers that support MOC will place a **MOC** order instead of a regular **Market** order for `OrderType.MarketClose`. MOC orders are placed immediately with the broker and subject to exchange rules to be accepted.

**Behavior 2: Use MOC - not enabled**  
The Order Manager will hold `OrderType.MarketClose` orders in a *WaitForClose* status until the predetermined number of seconds before the end of the session.  At that time the Order Manager will place a regular Market order. This works in conjunction with the preference: *Submit Market/Limit orders in place of MOC/LOC this many seconds before market close* (see below).

#### ☑ Use LOC (Limit-on-Close) when Possible
**Behavior 1: Use LOC - enabled**  
When selected, broker providers that support LOC will place a **LOC** order instead of a regular **Limit** order for `OrderType.LimitClose`. LOC orders are placed immediately with the broker and subject to exchange rules to be accepted.

> **Note!**  
> MOC and LOC orders that are signaled or placed manually before the close may be **rejected** by the exchange if placed after the exchange's cutoff time. At this time, **Nasdaq** stops accepting MOC orders 5 minutes before the close and **NYSE** stops accepting them 10 minutes before the close. 

**Behavior 2: Use LOC - not enabled**  
The Order Manager will hold `OrderType.LimitClose` orders in a *WaitForClose* status until the predetermined number of seconds before the end of the session. At that time the Order Manager will place a regular Limit order. This works in conjunction with the preference: *Submit Market/Limit orders in place of MOC/LOC this many seconds before market close* (see below).

> **Note!**  
> Brokers may reject Limit orders placed when the market is already trading at a price "better" than the limit price. In the same scenario, other brokers will fill the order "at market", which is the desired *WaitForClose* LOC behavior. 

#### ☑ Use Fractional Shares when Possible
This preference applies to stock brokerages that support fractional shares, currently only Alpaca. Crypto and Forex brokerages support fractional shares by nature. If you enable this option, Wealth-Lab will submit a Strategy-generated Signal as a fractional share order if the following conditions apply:
 - The [Position Size Basis Price Setting](StrategySettings) is **Next Bar Market Open**.
 - The Order Type is **Market**.
 
#### ☑ Use GTC for all Orders
When enabled, WL8 will submit all Strategy-generated orders to brokers as Good-til-Cancel.  When not enabled, this only occurs for Strategy-generated orders operating in a scale of weekly or higher.

---
## Miscellaneous Trading Settings

#### ☑ Submit Market/Limit orders in place of MOC/LOC this many seconds before market close
When **Use MOC** and/or **Use LOC** are disabled (Behavior 2 above) strategies that submit **MarketClose** (MOC) or **LimitClose** (LOC) orders will be held in *WaitForClose* status and then finally placed as regular Market and Limit orders when the number of seconds before close is reached. The maximum value possible is 3600 seconds (1 hour). 

If you need to make a trading decision very near the market close, say 3:59 pm, you can use this option for intraday strategies that use MarketClose or LimitClose orders to place a Market or Limit order seconds before the closing bell to obtain a nearly "On-the-Close" order behavior. 

#### ☑ Strategy Monitor Daily+ scale processing delay (minutes)
This setting sets the *default* number of minutes after the close that you want Daily and higher (Weekly, etc.) strategies to be scheduled. You set precise run time when configuring a Daily+ strategy in the [Strategy Monitor](StrategyMonitor). 

For example, if you enter 30, Daily strategies that operate on the U.S. Stock Market will be scheduled to run at 16:30 EST.  

%{color:blue}**Note!**% 
> Scheduled and last run times in the Strategy Monitor are provided in your computer's local time zone.


#### ☑ Strategy Monitor keeps a Strategy Active on Run Now
If you interrupt an active, scheduled item with **Run Now**, the default behavior is to deactivate the Strategy Monitor item. Checking this preference overrides that behavior. 

#### ☑ Enable Pre/Post Market Trading
Check this option if you want Wealth-Lab to place orders outside of the regular market session. Generally speaking, Limit and Stop-Limit orders are supported. Stop orders will be placed as Stop-Limit orders with equal Stop and Limit prices.

#### ☑ Convert Limit/Stop to Market if current quote exceeds price
When enabled, Strategy-generated Limit/Stop orders will be submitted to the broker as Market orders if the current quote exceeds the limit/stop price. This behavior only occurs during market hours.
> **Note!**  
> WL8 needs to request a quote for each Limit/Stop order processed with this preference enabled, so it may introduce some delay in order submission.