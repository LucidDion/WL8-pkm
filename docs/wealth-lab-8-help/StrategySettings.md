# Strategy Settings
Strategy Settings control the test data used for a Strategy's backtest, the Position Sizing rules applied when the Strategy enters a trade, and, if they exist, the Strategy Parameters.  

---
## Backtest Data
You can run backtests on one symbol or an entire DataSet of symbols, which is referred to synonymously as a **Multi-Symbol Backtest (MSB)** or a **Portfolio Backtest**.  The tab that you last configured will be used for the backtest. 

### Data Scale
Here you select the base time frame that your strategy trades.  

A strategy can include time compression to create indicators in other scales. For example, you might want to check for trade signals every 30 minutes, but keep track of the 20-day moving average.  You'd select 30 minutes for the Data Scale and use [TimeSeriesCompressor.ToDaily()](https://www.wealth-lab.com/Support/ApiReference/TimeSeriesCompressor) to return a TimeSeries in the Daily scale to obtain a 20-day moving average. 

### Data Range and Number
These controls give you fine control of the backtest data range. If you selected an intraday scale, another option to ***Filter Pre/Post Market Data*** appears. 

If you find yourself selecting specific data ranges frequently, take advantage of the ability to save **Named Date Ranges** by pressing the **Save** button (with a "floppy disk" icon) next to the data range dropdown. After you name and save a data range, it appears in the all subsequent data range controls, allowing you to select your favorite data ranges with just one action.

%{color:blue}**Note!**%  
> The IQFeed Historical Provider exposes a *Regular Session Only* option to prevent downloading Pre/Post Market data. 
> For best backtest performance use the IQFeed's *Regular Session Only* option and leave *Filter Pre/Post Market Data* 
> unchecked.

### Benchmark
WealthLab uses the Benchmark symbol as a baseline to compare your Strategy's performance against the overall market by running a "buy and hold" strategy to compare your strategy's results in several Performance Visualizers, like the Metrics Report and Equity and Drawdown Curves.  

---
## Position Sizing
Strategies determine ***when*** to buy and sell, but ***how much*** is determined by the Position Sizing selection.  

All backtests occur in a *portfolio simulation* environment the begins with the cash amount of starting capital. This implies that if the simulated portfolio runs out of *buying power*, the backtest will not be able to fill/enter new positions.

### Starting Capital
The amount of starting capital to use for the backtest/simulation. This represents the amount of cash only at the beginning of the test period. Actual buying power changes bar-to-bar over the test period and depends on cash available for new trades and margin. See *Margin Factor* below.

### Position Size 
Below we describe the four basic sizing options. For a host of Advanced Position Sizers and more get the [Power Pack for WealthLab 8](https://www.wealth-lab.com/Extension/Detail/PowerPack) extension!

- **Fixed Value**  
Gives each position an equal dollar size for stocks and options or equal margin value for futures.  

%{color:blue}**Note!**%  
The term "dollar" is always relative to the currency in use, e.g., if trading in European markets, the *value* would be *euros*.

Stocks - a fixed value per trade normalizes per-trade dollar profit metrics over the life of a backtest. For example, if you found that the *Average Profit* using $5,000 positions was $150 per trade, the *expected* dollar profit for a $5,000 position would be the same for a $10 stock at the beginning of a backtest as for a $200 stock anywhere in the backtest period. Compare with *Percent of Equity* sizing.  
 
 Futures - for a given futures contract margin, fixed margin sizing results in the same number of *contracts* for all positions. Example: if a future's contract's margin is $2,150, a $5,000 fixed value size would result in 2 contracts for all positions. In practice - especially for index futures - a contract's margin can change significantly with the intrument's price and volatility. In this case, average dollar profit metrics are not useful measures. 
 
See also:  
*Profit Per Bar* in the  [MetricsReport](MetricsReport), which always assume a $5,000 fixed size, and, Futures Mode in [Backtest Preferences](BacktestPreferences).  

- **Shares/Contracts**  
Assigns a specified number of shares (stocks) or contracts (futures/options) to a position. Generally, this setting would used when testing/trading a specific asset and perhaps only during live trading. For example, use this sizer to set up a streaming chart in trading workspace to always trade 3 Micro Nasdaq (MNQ) contracts. 

- **Percent of Equity**  
Lets you scale position sizes based on the changing portfolio equity level. Specify the percentage of the total account equity that each position should take. Account equity is based on cash available plus the value of open positions on the Signal bar - the bar prior to the trade. Once this value is determined, position sizing proceeds along the same lines as the Fixed Dollar/Margin options above. With *Percent of Equity* sizing the dollar value of each trade can change significantly during a backtest making the per-trade dollar profit metric simply an *average value* that should not be used as an *expected value*. 

%{color:blue}**Example**%  
> Suppose you want each new position to be worth 10% of your account's equity. If the account's equity was $50,000 at the time your strategy generated an entry signal, the position size would be $5,000. For a stock trading at $20 per share, this would translate into 250 shares.

- **Max Risk %**  
Sets a position size such that if the trade is stopped out, it results in the specified percentage loss. The amount value specifies the maximum percentage of the current backtest equity that you're willing to risk on every trade. See the [Max Risk Percent](MaxRiskPercent) help topic for details on this position sizing method.  

%{color:blue}**Tips!**%  
> 1. When enabled in [Trading Preferences > Portfolio Sync](TradingPreferences), WealthLab will use ***brokerage account equity*** to size **Signals** for Equity-based sizing methods for the Strategy Monitor, Streaming, and Strategy windows. 
> 2. More *Portfolio Sync* options synchronize exit signal sizes to reflect the account's actual Position size. 

#### Advanced Pos Sizer(s)
For dozens of Advanced Pos Sizers, install the [Power Pack Extension](https://www.wealth-lab.com/extension/detail/PowerPack). Select the Pos Sizing method from the dropdown and then click the *Configure Position Sizer* button. Core Advanced Pos Sizers installed with WealthLab include: 

- **Equal Shares**  
Provides a way to keep a consistent % of Equity sizing when the number of symbols in the DataSet can vary over time like the WealthData dynamic DataSets. *Always assuming 100 symbols in your DataSet*, specify the % of Equity to apply and the Position Sizer will adjust accordingly. In other words, to divide equity equally between all symbols in the DataSet, no matter the number of symbols, use 1%. Likewise, 2% indicates to spread equity evenly between half the symbols in a DataSet.  
  
  For specific examples, to equally divide equity so that all symbols of the Dow 30 can be traded for each bar, specify **1%**. Nominally, the sizer will apply 3.33%, which is 1% x 100 / 30.  Likewise, to divide equity equally for 50 positions in the S&P 500, specify **10%**. Nominally, the sizing actually applied will be 2.0%, which is 10% x 100 / 500.

- **Indexitor**  
Indexitor calculates a % of equity size using the RSI indicator of a specified symbol and increases Position size as it becomes more oversold or overbought. The formula is as follows: 

  1. Increase when Oversold: % of Equity = (1 - RSI/100) * (Max% - Min%) + Min%
  2. Increase when Overbought: % of Equity = (RSI/100) * (Max% - Min%) + Min%
  
  For example, assume increasing when Oversold and Max% = 50%, Min% = 5%, and RSI is 40.  
  % of Equity = (1 - 40/100) * (50 - 5) + 5 = 23%

- **Meritocratus**  
Fluctuates the position size between a minimum and maximum percent of equity based on the percentage of this symbol's closed positions that were profitable to date. If the profitability percentage exceeds the specified threshold, the maximum percent of equity value will be used. 

  If *Rolling Method* is enabled, it will use rolling percentage of winners based on a specified number of last trades. When "Rolling method" is disabled (*by default*), the percentage of winners is calculated from the first closed trade to the the last closed trade. When enabled, the "Rolling Method" will:

  1. Size positions based on the initial size (%) until the number of closed positions exceeds the user-specified "Number of trades"
  2. After that, it average the winning percentage over user-specified number of last trades ("Number of trades") - like a moving average of the N trades


**Position Size Override**  
You can also dynamically size positions in your strategy code. The **PlaceTrade** call will always returns a 
**Transaction** object that has a **Quantity** property.  By assigning a quantity to the Transaction object you 
can override Position Size in your script.  This works for Signals too.


%{color:blue}**Example**%   
Override the Position size with 100 shares
```csharp
	Transaction t = PlaceTrade(bars, TransactionType.Buy, OrderType.Market);
	t.Quantity = 100;
```

### Basis Price
Whenever your strategy signals to buy or short at market, WealthLab determines the number of shares for the order by dividing the dollar size by the share value, or ***Basis Price***.  By default, the basis price is the last closing price. However, consider this case:

The Closing Price for a market order is $25 and the backtest currently has $100,000 of capital to invest. The number of shares to purchase at 100% of Equity is 4,000. If price opens the next day at $26, the total size of a 4,000-share position would be $104,000.  Assuming no margin, the simulation does not have enough money to take this trade, so it is "dropped".  The number of dropped trades appear in the Metrics Report as **NSF Position Count**, where NSF means *Not Sufficient Funds*.  (For more info, see Retain NSF Positions in 
[Advanced Strategy Settings](AdvancedStrategySettings).)

By changing the Basis Price selection to ***Market Open next Bar***, you can eliminate NSF Positions due to price gaps of the *traded symbol*. In our example, the size would be calculated using the $26 opening price, or 100,000 / 26 = 3,846 shares, and the trade would *likely occur*. It's not guaranteed because positions that exit at market can affect the portfolio equity such that insufficient buying power is available. In the example, $99,996 (26 * 3,846) buying power is required for the trade. If the value of positions that exit at the market open cause the equity to drop by more than $4, the 26-share trade would still become an NSF Position.

#### Important Notes for Market Open Basis
1. This option allows the dollar-size to adjust the number of shares at the market price and is compatible with brokers that let you manually enter orders in dollar sizes, such as with mutual funds.
2. Signal Quantity for entry orders is shown in the dollar amount for ***display only***.  Exit signals are always shown in number of shares (see image below).
3. Signal Quantity is always **Staged** or **Placed** with the number of shares using the Market Closing price basis. 

![Signals with Basis Price Market Open option](https://www.wealth-lab.com/Images/WLHelp/BasisMarketOpen.png)

### Margin Factor
Set Margin Factor to a ratio greater than 1 to allow a backtest to borrow cash for new purchases when required. You can set the Margin Loan Rate in the [Backtest Preferences](BacktestPreferences). 

This margin setting does not apply to futures and you should set it back to 1 when simulating futures trading. Contract margin for futures is set in the [Market & Symbols](MarketAndSymbols) window.

WealthLab uses a simplified, but reasonable margin model that differs somewhat in comparison to the [Regulation T](http://www.sec.gov/investor/pubs/margin.htm) (Reg. T) rules used by U.S. brokers. When enabled, the amount of buying power for new purchases is calculated as follows:

    BuyingPower = (( MF - 1 ) * Equity) + Cash,

where, 
MF is the Margin Factor, 
Equity is the total Portfolio Equity, and,
Cash is the amount of free cash available for purchases.
  
The **Benchmark Buy & Hold** Strategy will use margin - and is charged the Margin Loan Rate for the duration of the backtest - if you check the option to "Use Margin in Benchmark Backtest" in the [Backtest Preferences](BacktestPreferences). 

### Max Open Settings
The "Max Open" settings provide a way to *backtest* different Position options without the need to change your code. They are applicable in backtesting and *not in live trading*.

**Max Open Pos**  
The maximum number of Positions the Strategy can hold open simultaneously.  Default is 0 for no maximum. 

**Max Open Long**  
The maximum number of *long* Positions the Strategy can hold open simultaneously.  Default is 0 for no maximum.  The value -1 disables long Positions. 

**Max Open Short**  
The maximum number of *short* Positions the Strategy can hold open simultaneously.  Default is 0 for no maximum. The value -1 disables short Positions. 

**Max Open Per Symbol**  
The maximum number of Positions the Strategy can hold open simultaneously on a per Symbol basis. Default 
is 0 for no maximum. 

%{color:blue}**Important!**%
> The Max Open options are not available for trading in Streaming charts or the Strategy Monitor. They are used for backtest only.
> To limit Positions for live trading, you need to modify the Strategy with that condition. 

### Max Entry Signals
Intended primarily for strategies the use Market order entries, this option limits the number of signals/orders generated for each bar of the backtest. As always, transactions are sorted by their assigned weight (random if not assigned) and only the n signals with the highest weight are considered. Specify 0 for all signals. 

This option is not recommended for most Stop/Limit strategies because it will remove candidate trades that *might* fill in favor of others that *might not* fill. 

[![Max Entries per Bar Position Sizing Option](http://img.youtube.com/vi/5YMuPxxqEM0/0.jpg)](https://www.youtube.com/watch?v=5YMuPxxqEM0&t=10s "Max Entries per Bar Position Sizing Option")

## Strategy Parameters
Parameters hold the values used for variables in a Strategy. For example, 50 could be the value for the period parameter in a 50-day moving average. You can assign Parameters in a C# Strategy's constructor using **AddParameter()** or with a building block strategy by clicking the "Make Optimizable" button, when shown. Parameters have a name, type, default value, a min/max range, and a step value. [Optimizations](Optimization) attempt to find the value for parameters that "optimize" an objective metric (e.g.,  APR% or Sharpe Ratio) within the range that you define. 

[![Optimization Parameters in Building Blocks](http://img.youtube.com/vi/xaUJ9tZWUcY/0.jpg)](http://www.youtube.com/watch?v=xaUJ9tZWUcY "Optimization Parameters in Building Blocks")

### Standard Opt Parameters
Without actually optimizing, you use parameter sliders and re-run backtests with the new values to see the effect. 
With these controls you can: 
- Reset the parameter value(s) to their original default(s), or,
- Save the currently configured values as the new default values.

If the Strategy has [Preferred Values](PreferredValues) defined, you'll see a check box here enabling you to 
**Use Preferred Values** in a backtest.

### WFO Opt Parameters
If you saved a strategy after running a Walk-Forward Optimization, this tab will appear. By checking the box and then clicking **Run Backtest**, you can perform an Out-of-Sample backtest using the WFO parameters for the Data Range selected.  The controls allow you to inspect the parameters for each of the WFO periods. 
