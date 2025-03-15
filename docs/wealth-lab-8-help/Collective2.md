# Collective2 Integration
[Collective2](https://www.collective2.com) is a web-based service where you can publish trading strategy signals and other users can subscribe to your signals for a monthly fee. WealthLab 8 offers direct integration with Collective2 so you can automate the process of submitting signals to the service.


## Logging in to Collective2
WealthLab connects to Collective2 in two different tools. Only your Collective2 **v4 API Key** is required, and it can be created/obtained by [logging in to your C2 account](https://collective2.com/securelogin) and navigating to [Account Management > API Key](https://collective2.com/apikey). 

> **Important!**  
> To use the Collective2's API to place signals with WealthLab, a Collective2 subscription to the [Basic or Premium Plan](https://collective2.com/choose-plan) is required. 

## C2 Broker
We've implemented Collective2 as a Broker that's available for login in the [Order Manager](OrderManager). The C2 Broker expresses your C2 trading strategies as Broker "Accounts". Like any other Broker in WL8, you can can set up a Strategy to auto-trade, placing the signals to the C2 strategy of your choice, on an intraday basis. Use one of the following tools to auto-trade a C2 strategy:

 - [Streaming Chart](StreamingCharts)
 - [Strategy Monitor](StrategyMonitor)
 - [Quotes](Quotes)

## MOC and LOC Orders
Collective2 handles only Market, Limit, and Close orders. *MarketClose* and *LimitClose* order types will employ WealthLab's *WaitForClose* behavior if *Use MOC / Use LOC* is enabled or disabled. See [Trading Preferences > Special Order Types](TradingPreferences) for information about "Behavior 2" for MOC/LOC orders. 

## Account Monitoring / Staying in Sync with C2 Strategies
 See what your C2 strategies are holding at all times using WealthLab's Accounts tool (Ctrl + T). The contents of your C2 Strategy portfolios are updated every *10 seconds*. 

As a C2 Leader, it's imperative to operate your WL strategy "in sync" with the C2 strategy/account. Except where indicate below, WealthLab runs strategies hypothetically using the data you feed it. Hypothetical results are influenced not only by data, Strategy Settings (Retain NSF, Starting Equity, Position Size),and the OrderType used (Market, Limit, Stop), but also by Backtest Settings like Slippage, especially Limit Order Slippage. 

For most strategies, the following [Trading Preferences](TradingPreferences) are recommended: 

☑ Block Exit Orders when Position not Found
☐ Reduce size of Exit Orders to match Position Quantity  
☑ Always set Exit Order Quantity to full Position Quantity  
☑ Use Broker-reported Account Value for % of Equity Position Size  
☐ Exit Orphan Positions at Market  
☑ Use Live Positions* 

*N/A for Strategy Window and manages only one Position per symbol. See [Trading Preferences](TradingPreferences) for details. 

Below you'll find more *best practices* for trading with C2 depending on the WealthLab signaling tool. 

### Option Trading on C2
Option trading is often illiquid and can have large bid/ask spreads. If possible, use mid-bid/ask pricing in intraday charts for the most up-to-date representation of price. In the IB Provider configuration, for example, select *Midpoint* for *Option Chart: What to Request*.

WealthLab supports trading U.S. stock options on C2. If you place trades manually, see [C2's Option Symbols Guide](https://support.collective2.com/hc/en-us/articles/360051538773-Collective2-Options-Symbols)

To Auto-Trade options (strategy) as either a primary or secondary symbol, use the guidance below.  Use the `OptionsHelper.C2Symbol()` to easily find a C2 option symbol for an underlier, right, strike, and expiration date, or pass an option symbol from another format to convert. 

#### Option is the Primary Chart Symbol
If the data provider uses the same symbology as C2, i.e., IQFeed, then no special treatment is required. However, if the charted symbol using different symbology, you should *map* the chart symbol to the corresponding C2 symbol. 

**Example**  
IB's primary charted symbol for SPY 450 Call expiring Oct 20, 2023 is SPY231020C450. The symbol mapping would be SPY231020C450=SPY2320J450.  Note that you can use a this line of code to return the C2 Option Symbol - `WriteToDebugLog(OptionsHelper.C2Symbol("SPY231020C450"));`  

In both cases, enable the ☑ **Live Positions** Trading Preference to keep the strategy in sync with the C2 Strategy. 

#### Option is a Secondary Traded Symbol
Another way to trade options is based on the price action of the underlying stock. In this case, you access a BarHistory of the option as a secondary symbol. 

If not using IQFeed for option data, the BarHistory can be fictitious. `OptionSynthetic` contracts work for this purpose. The trick is to assign the C2 Symbol to the synthetic BarHistory in order to trade it. 

> **Important!**  
> **Live Positions** will not sync with secondary symbols. To keep your strategy from adding additional positions when the exit logic should be processed instead, access and use the broker positions in your strategy as [discussed here](https://www.wealth-lab.com/Discussion/7914), beginning from Post #18. 

The code below shows how to access IB data for the chart underlier ATM Call with an expiry at least 5 days in the future. `OptionsHelper` finds the C2 symbol from IB option symbol and assigns it to the call's BarHistory, which is passed to `PlaceTrade()` to create a limit order for the option contract at the last live price given by the IB option. 

```
using WealthLab.Backtest;
using System;
using WealthLab.Core;
using WealthLab.Data;
using WealthLab.Indicators;
using System.Collections.Generic;
using WealthLab.InteractiveBrokers;

namespace WealthScript123
{
	public class C2OptionExample : UserStrategyBase
	{
		public override void Initialize(BarHistory bars)
		{
			//intraday data required
			if (!bars.IsIntraday)
				throw new Exception("Intraday chart required.");
		}

		public override void Execute(BarHistory bars, int idx)
		{
			if (idx == bars.Count - 1)
			{
				// get the IB "ATM" option symbol from IB's option chain
				string ibSym = IBHistorical.Instance.GetOptionsSymbol(bars, OptionType.Call, bars.Close[idx] - 20, bars.DateTimes[idx], 5);

				// get the history for pricing limit orders
				BarHistory callBars = GetHistory(bars, ibSym);

				// assign the ocrresponding C2 symbol to the ib's call BarHistory and plot
				callBars.Symbol = OptionsHelper.C2Symbol(ibSym);				
				PlotBarHistory(callBars, "oPane");

				// create a limit order using the *IB live data last close*
				PlaceTrade(callBars, TransactionType.Buy, OrderType.Limit, callBars.LastValue); 
			}
		}
	}
}
```


#### [Signals Publisher](SignalsPublisher)
We offer a Collective2 Signals Publishing Service option in the [Signal Publisher](SignalsPublisher) tool. You can easily link one or more Collective2 strategies with WealthLab Strategies and run them all with the click of a button. The Signal Publisher is perfect for quickly processing all of your **end-of-day Strategies**.

> **Notes:**  
> 1. Each Strategy that you set up in the Signal Publisher can be associated with a different Collective2 strategy.  
> 2. Workspaces are not required to save the configuration of the Signal Publisher! 
> 3. Unlike other WealthLab tools that can send signals to only one C2 account, you can use any number of API Keys (even for different C2 accounts) when connecting strategies in the Signals Publisher. 

The [Signals Publisher](SignalsPublisher) tool automatically synchronizes exit orders with the C2 Position size and uses the C2 Strategy model account size for % of equity-based sizing for new entry signals.  

On rare occasions *orphaned positions* may be detected. An *orphan* is a Position that exists at C2 (or any broker), but not in your hypothetical WL backtest. Check for orphans after each run and take approriate manual *action*. The Signals Publisher will not manage orphaned positions.

Orphans can exist for a few reasons. An obvious one is if you missed running the Signals Publisher for one or more sessions on which the Strategy sold positions. A more subtle reason for orphaned positions is having used different data (bad, uncorrected, etc.) when placing signals than that used on a later run. 

**Example:**   
Your strategy buys at 1% below the previous close. After a 50.00 close, you place a signal to buy ABCD at 49.50 limit. ABCD's low for the next day is precisely 49.50 and C2 creates a position. The next day, the data provider corrects the settled closing price for the previous day to 49.95. The WL strategy will now try to create a hypothetical trade at 49.45. Since ABCD's low was $49.50, the WL Strategy cannot create a position and the result is a orphan broker/C2 position. 

#### [Quotes](Quotes)
The Quotes tool is for EOD strategies that trade more limit and stop orders than an account can handle simultaneously. You can send stop/limit signals to Quotes after running a strategy on a DataSet from the [Strategy Window](Strategy Window) or from the [Strategy Monitor](StrategyMonitor), covered below. 

Using the Strategy Window for C2 is a less desirable option since the *Live Positions* preference does not apply to this tool. This allows for the existence of an orphan Position at C2. For example, changing a Strategy Parameter or an option like *Retain NSF Positions* could create orphans. 

Also, when generating signals for Quotes using the Strategy Window, be mindful of exit orders for hypothetical Positions that don't exist at C2. The *Block Exit Orders when Position not Found* [Trading Preference](TradingPreferences) can assist with this scenario. 

#### [Streaming Charts](StreamingCharts)
Most intraday strategies traded from Streaming charts are recommended to: 
- enable *Use Live Positions*
- load sufficient data such that the Position's price appears in the chart's bar history

#### [Strategy Monitor](StrategyMonitor)
- See the recommendations for the Streaming window. 
- The Strategy Monitor is unique in its ability to employ the *Live Positions* preference for Daily strategies. 


### For more information... 
Read the WealthBlog article:  
 [7 Ways to Publish Signals at Collective2 with WealthLab](https://www.wealth-lab.com/blog/auto-trade-with-c2-collective2)

 Watch an introduction to the C2 integration:  
[![Collective2 Integration](http://img.youtube.com/vi/EQdQjdeTmmg/0.jpg)](https://www.youtube.com/watch?v=EQdQjdeTmmg&t=10s "Collective2 Integration")