
# Markets

- [take me there now](action:MarketsAndSymbols)

**Markets** represent exchanges such as the **CME**, or broad groups of exchanges such as **US Stocks**. Wealth-Lab uses **Markets** to determine when historical data needs to be updated, and to establish open and close times for filtering of [streaming data](StreamingProviders).

**Markets** come from:
 - **Wealth-Lab** itself, supplies **US Stocks** and **German Stocks** out of the box.
 - **Historical Data Providers**, for example **Cryptocurrencies** provided by the **Cryptocompare** extension.
 - **You** can create your own **Markets**, and they are stored in the [Markets.txt](action:MarketsTxt) 
 file in the [user data folder](action:DataFolder).

---
## Market Properties

**Time Zone**, **Trading Days**, **Hours**  
Wealth-Lab uses these properties to determine if the Market is currently open or closed, based on your computer's system clock.

**Display Decimals**  
Used to determine how many decimals to use when displaying data in [Charts](Chart). Can be overridden by [Symbols](Symbols) settings.

**Quantity Decimals**  
Used to determine how many decimal places to round to when calculating the number of shares/contracts for a position.

**Benchmark**  
The default symbol to use as a backtesting benchmark. Typically a market index such as **SPY**, or the leading symbol in a market, such as **BTC.USD** for Cryptocurrencies.

**Holidays**  
Determines which holiday days are used by the Market.

---
## New Market.../ Configure Market
To define a new market, start fresh with the **New Market...** button or start from a baseline by selecting a market and then **Create a Copy**. 

Fill in Market Name, Benchmark Symbol, Time Zone, Display and Quantity Decimals. 

### Trading Days and Market Hours
Add checkmarks for all days on which the market trades.  Click on *Default* to adjust the default Open and Close times. If a day has different hours than the default, **Add**, select it, and modify its hours to override the default hours.

%{color:blue}**Note!**% 
> Close Time can be earlier than the Open Time. In this case Wealth-Lab assumes a 24-hour market such that the Close occurs the next day. 

---
## To Associate Symbols to a Market
Use the [Symbols](Symbols) page in the **Markets & Symbols** window.

---
## Set Commission
Sets the commission amount by Market. Use this facility in combination with the [Backtest Preference](Backtest Preferences) so that backtests use the Market's commission amount instead of the amount in Backtest Preferences.  

%{color:blue}**Note!**% 
> A Symbol with Set Commission defined has priority over a Market's commission amount. 