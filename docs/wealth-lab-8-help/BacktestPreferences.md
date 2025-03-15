# Backtest Preferences

 - [take me there now](action:BacktestPreferences)

This interface lets you control various settings that impact all backtests.
## Commission/Interest settings
#### ☑ Commission
Controls how much commission is deducted from each simulated entry and exit order during the backtest.

**Use Market/Symbol Commission when Defined**  
The **Set Commission** facility in the [Market and Symbols](MarketAndSymbols) tool lets you specify commission by Market and/or Symbol. Check this box so that backtests use those commission values instead of the amount in Backtest Preferences.

--- 

#### ☑ Interest on Cash
Specifies the rate that will be used to calculate interest on cash that accumulates during a backtest. You'll be able to see the total in the backtest **Metrics Report**. If you check the box **Use UST Yield**, the daily cash interest rate will be based on the  **US Treasury Yield** of the period you specify next to the check box.
#### ☑ Margin Loan Rate
The rate that will be used to calculate interest on margin used during a backtest. Will only come into play if you backtest using a **Margin Factor**, and your Strategy actually goes into margin. You'll be able to see the total in the backtest **Metrics Report**.

--- 

## Slippage
Slippage simulates less-than-perfect fills for your trades that can happen in the real world. 

**Adjust Entry/Exit Prices**  (*Applies to: Market and Stop*)  
Check this box to include the effects of slippage in your system performance results for these order types. This slippage option *adversely* adjusts entry and exit prices for Market and Stop orders by the slippage amount, but never beyond the low/high range of the bar.  

**☑Limit Orders**  
Slippage for Limit orders *does not* adjust the fill price (see **Exception*). Instead it ensures that price reaches the slippage-adjusted price for the order to fill at the limit price. This option makes the probability of limit order execution in backtesting more realistic because many competing limit orders in actual trading may prevent yours from being filled.

**☑ Exception!**  
 If the limit price is exceeded on an opening gap and **Adjust Entry/Exit Prices** is *checked*, slippage will be applied to the bar's opening price to obtain a new execution price to the extent allowed by the bar's range. 

**MarketClose/LimitClose Orders** 
Slippage will be applied, except for exit orders if the following is true:

 - The corresponding MOC/LOC [Trading Preference](TradingPreferences) is enabled
 - The scale is Daily+ or it is the last intraday bar of the trading day

### Slippage Usage Notes

1. Limit Order Slippage is not compatible with zero-range bars, i.e., time-of-sales, or tick data. 
2. Slippage applied to market orders will always penalize a trading system. 
3. Limit Order Slippage *prevents filling trades* if prices don't trade beyond the limit price. This may keep your backtests from participating in trades that ultimately would have resulted in losses (positive impact) or in profits (negative impact). 
4. We recommend disabling limit-order slippage for Live trading of strategies that use limit orders to enter positions because it may prevent a strategy from executing the exit logic. Also, **Use Live Positions** in the [Trading Preferences](TradingPreferences) can help keep most strategies synchronized with broker positions.

--- 

## Other settings

#### ☑ Convert trade quantities to Round Lots
If set, rounds the number of shares in a backtest to the nearest hundred. If the initial quantity is less than 100, rounds to the nearest ten. If the initial quantity is less than 10, does not round.  Round Lots is applied as follows: 
- Futures Mode *enabled* -  all Security types *excluding Options and Futures*
- Futures Mode *not enabled* - all instruments

#### ☑ Futures Mode
If set, uses the **Point Value**, **Margin**, and **Tick Size** established in the [Markets & Symbols](MarketsAndSymbols) window. Wealth-Lab will attempt to match each symbol with an entry in the [Symbols](Symbols) list. This allows you to realistically backtest using futures data. 

> Generally, you can leave Futures Mode enabled. The only time you might need to turn it off is to backtest stock symbols that could potentially match a futures symbol entry - which is more probable when using wildcards. 

In Futures mode, stop and limit prices are adjusted to align with the contract's tick value for stop triggering and fills. The direction of the adjustment is determined by transaction and order types as follows:

| TransactionType | OrderType | Direction |
|--------------|--------------|--------------|
|  Buy or Cover | Limit  |  Floor (down) |
|  Buy or Cover | Stop |  Ceiling (up) |
|  Short or Sell | Limit  |  Ceiling (up) |
|  Short or Sell  | Stop |  Floor (down) |

> **Example**  
You're long a contract which has a 0.25 tick value and the calculated profit target is 51.33. Wealth-Lab will adjust the sell at limit price higher to 51.50 so that the price conforms to the minimum tick variation.

**Position Profit Percent, MFEPct, MAEPct for Futures**  
Profit (and loss) percent for futures contracts are relative to futures margin. To find a Position's profit percentages in terms of absolute price movement in a strategy, calculate the values in your code as opposed to using ProfitPct, MFEPct, MAEPct, or their "AsOf" counterparts. 

> **Example: Profit Percent for Futures Mode**  
2 long ES contracts ($50 point value) purchased at 4000.00 advanced to an intraday high of 4050.00, a 1.25% rise for "non futures mode". The MFE dollar profit is (2 * $50 * 50) = $5,000 and for a futures margin of $18,000 per contract, the MFEPct is 5000/36000 * 100 = 13.89%.

#### ☑ Collect Dividends
If you have an [Event Provider](EventProvidersTab) enabled that supplies dividends, the backtester will add cash from collected dividends back into the equity curve. Any fundamental item with the text "dividend" in its name is considered a dividend for this purpose. To avoid inflated results, do **not** enable this if your backtest is run on data already adjusted for dividends, such as Yahoo! Finance.

If you enable dividend collection, and your benchmark symbol collects dividends, the buy & hold benchmark backtest will **re-invest the dividends** by purchasing more shares of the benchmark symbol. For this reason, you may see multiple positions in the benchmark Metrics Report.

#### ☑ Use Margin in Benchmark Backtest
By default, the benchmark backtest is a buy and hold simulation using approximately 100% of the simulation's starting capital.  (Specify the benchmark symbol in the [Strategy Settings](StrategySettings).)  If your strategy has high margin exposure, mark this preference to compare with a benchmark backtest that uses the full amount of margin.  For example, with a 2:1 margin setting the benchmark backtest will create a 200% position and be charged the Margin Loan Rate (see above) for the full range of the simulation. 

#### ☑ Count trades exited at market open as a full bar
When this option is disabled (by default), the exit bar for market orders is excluded from the Bars Held calculation. Enable it if you want to count the bar the market order was exited at as a full bar in the Bars Held calculation.

#### ☑ Process Cosmetic Strategy Methods in Strategy Monitor
By default, Strategies run in the Strategy Monitor do not process cosmetic Strategy Methods such as DrawLine or DrawBarAnnotation. If you need to have cosmetics methods operational in the Strategy Monitor, set this to true. Doing so will increase Strategy execution time.

#### ☑ Multi-Currency | Base Curr: USD
Enable Multi-Currency for backtests that include instruments that trade in different quote currencies. 

The goal of the multi-currency backtest feature is two-fold: allows backtest results of instruments priced in different quote currencies (USD, EUR, AUD, BTC, etc) to be translated to a single base currency, while accounting for significant currency effects on non-base currency trades that span more than one day. 

The Multi-Currency feature uses **daily currency data only** and synchronizes with the test data. Multi-Currency backtests apply the *Daily closing prices* to trades created on the same date. Note that Forex data closing prices generally come from around 17:00 UTC (12:00 ET).  WealthLab's Wealth-Data supports major cross currencies including Bitcoin on a daily basis. Currency data may be backed up by other currency/forex providers enabled in the Data Manager > Historical Providers view. 

> **Intraday trades** in non-base currencies that open and close the same day will not show a currency effect since the same forex conversion is applied to both open and closing trades.   

With the exception of the Positions Visualizer, values shown and returned by functions like Profit, MFE, etc. will be converted to the single **Base Currency** selected here. 

> **Important!**  
> Strategies that use Position methods like `ProfitAsOf()`, `MFEAsOf()`, etc. will likely generate different *trade exits* for instruments whose currency doesn't match the base currency. To get the same *trade exits* for a Multi-Currency backtest, strategies that use these functions must be modified to use their *NonBase* versions, e.g., use `ProfitNonBaseAsOf(), MFENonBaseAsOf()` instead of `ProfitAsOf(), MFEAsOf()`.  

Multi-Currency will have the following effect on backtests:  
1. **Starting Equity** is specified the base currency.  
1. **Backtest Equity and Cash** update *in the specified base currency*.  
1. Trade profit, commissions and dividends are converted to the base currency when applied to the backtest.
1. **Positions** are sized in the **trade currency (non-base)**, but with respect to the account's equity in the base currency (see example).  
1. **Trade Profit** reported in the **Positions Visualizer** is shown in the trade's non-base currency, however, the column **Fx Gain (Base)** provides the amount that the Position gained/lost in the base currency due to the effect of the currency exchange.  
1. In Futures Mode, WealthLab converts futures margin to the base currency to reduce Cash available. This base value is returned to Cash and Equity curves when exiting the trade, so no gain will be associated with the currency effect. However, the gain applied to the equity curve is the trade gain/loss in the trade currency converted to the base currency *at the exchange rate each day*.  

![Multi-Currency Meta-Strategy Backtest](https://www.wealth-lab.com/Images/WLHelp/MultiCurrencyWL8.png)

> **Example**  
>- The Starting equity base currency is $100,000 USD and your backtest includes AIR.DE in EUR. Position Sizing is set to 10% of Equity. The trade buys AIR.DE with a basis price 116.68 and fills at market at €116.20 when the EURUSD spot price is 1.0663. Position Size is $100,000 * 10% = $10,000 / 1.0663 = €9378. Consequently the share size is 9378 / 116.68 = 80 shares.  
>- Days later, the EURUSD spot price is 1.0955 and the trade is exited at €125.72 for a EUR profit of 80 * (125.72 - 116.20) = €761.60. The trade profit in the *base currency* reflected in the equity curve is: (80 * €116.20 * 1.0663) - (80 * €125.72 * 1.0955) = $1,105.78, of which $293.68 is due to the effect of the increase in EURUSD exchange.

**Trading a Broker Account with Multi-Currency**  
For proper equity-based signal sizing, the Account Value reported by the broker must match the specify Multi-Currency base currency. For example, Interactive Brokers reports account value in the customer-specified BASE currency. If the account BASE is EUR and you're trading a USD-denominated market, enable Multi-Currency with EUR to properly size USD positions for your EUR account.

**Forex/Crypto Multi-Currency Notes**  
Forex trading involves selling one currency position (e.g. USD) in exchange for another currency position (e.g. EUR).  For example, as a Forex trader you could buy EUR with USD and later sell the EUR position to buy AUD. 

WealthLab's Backtester does not currently distinguish currency positions, and instead a position is the currency cross itself (e.g. EURUSD). In other words, in a backtest if you buy 10K EUR using EURUSD, the position is 10K EURUSD, not 10K EUR. While you can mix positions having different quote currencies (e.g., EURUSD, USDGBP, AUDEUR, etc.) in a Multi-Currency backtest each position is managed (bought and sold) using the same currency cross.

> **Forex Trading Side Note**  
> Interactive Brokers does not support negative currency balances. For example, with a 10K USD position you could easily buy a 200K EUR position with typical forex leverage. However, IB will reject the trade since it would result in a large negative USD balance. Instead, unless you're a resident of USA, Canada, and Hong Kong, you can use **CFDs** (Contract For Difference) to make this trade. [See this article (click) for details](https://ibkr.info/article/2707). 

#### ☑ Volume % Limit
Limits the quantity of a backtest position to a percentage of the bar's volume. This can prevent Strategies from showing exaggerated results by taking simulated positions with unrealistically high quantities. This feature has no effect on a BarHistory that has 0 volume for the entire history, e.g., Forex. 

#### ☑ Signals Sort
This option controls how Signals are sorted in the [Strategy](Strategy) window Signals tab. It does not affect how historical Transactions are sorted during a backtest. These are always sorted by Transaction.Weight, with random Weights being assigned to all entry Transactions.

#### ☑ Position Matching
When a strategy has multiple positions for the same symbol, this option determines how Wealth-Lab will match positions if the exit signal does not match a Position by its *positionTag*.  The methods are: 
- First in First out (FIFO) - Oldest Positions are exited first
- Last in First out (LIFO) - Latest Positions are exited first
- Smallest Qty to Largest - Smallest Positions are exited first.  

If your script is rebalancing Positions sizes frequently, exiting Smallest Qty first may be preferred to keep the number of Positions to a minimum. 

#### ☑ Exit Prioritization
Exit Prioritization comes into play if both a limit and a stop order could fill for the same backtest Position **on the same bar**. Select how you want WealthLab to handle this situation in a backtest.
- **Neutral (Random)** - WealthLab's default is to randomly choose between filling the limit or stop order. This method can add to the variability of backtest results. 
- **Favor Stop (Pessimistic)** - stop exit orders are filled instead of limit targets that could have filled on the same bar.
- **Favor Limit (Optimistic)** - limit targets are filled instead of stops that could have filled on the same bar.

--- 

## Performance Visualizers
Lets you control which **Performance Visualizers** appear in the **Backtest Results** tab of the [Strategy Window](Strategies). Certain Performance Visualizer extensions can take a significant amount of time to populate, so it can be useful to disable them here until needed. You can also drag and drop the Performance Visualizers in this list to establish the order they appear in the Backtest Results tab.
