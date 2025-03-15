# Entry and Exit Building Blocks
These Blocks control when your Strategy enters and exits the market. There are two basic **Entry Blocks**, and several **Exit Blocks** to choose from. You can drop [Condition Blocks](ConditionBlocks) onto Entries and Exits to further refine your Strategy's logic. 

Each Entry and Exit Block has two versions, one for *long positions* (**Buy**/**Sell**) and one for *short positions* (**Short**/**Cover**).

Certain Exit Blocks can optionally support **same-bar exits**. These Blocks will have a check-box along the upper right button bar. When you enable same-bar exits, the backtester will process the limit or stop exit on the same bar as position entry.

---
## At Market Open
These Blocks simulate placing a market order, and are filled at market open price.

---
## At Limit/Stop
These Blocks simulate placing a *limit* or *stop order*, and are quite flexible. You can specify the order price based on a percentage above or below an **Indicator** value. Whenever a Building Block allows you to select an **Indicator**, remember that you can also select the basic Open/High/Low/Close or Volume, which appear at the top of the Indicator dropdown list.

In this example, we simulate placing a limit order with an order price equal to the day's low.

![enter image description here](https://www.wealth-lab.com/Images/WLHelp/BuyAtLimitLow.png)

Here we implement a complete channel breakout system with just two Building Blocks, an Entry and an Exit. The Strategy buys at a stop set to 1% above the highest 10-day high, and sell at a stop set to the lowest 10-bar low.

![enter image description here](https://www.wealth-lab.com/Images/WLHelp/ChannelBreakout.png)

---
## Additional Exit Blocks
The following additional Sell/Cover Blocks are available for exiting your positions:

**After N Bars**  
Exits the positions after a certain number of bars (historical data points).

**At Profit Target**  
Simulates using a *limit order* to exit a position based on a profit target percent.

**At Stop Loss**  
Simulates using a *stop order* to exit a position based on a stop loss percent.

**At ATR Profit Target/Stop Loss/Trailing Stop**  
Simulates using a *limit order* or *stop order* (respectively) to exit a position at an ATR-based profit target or a stop loss (respectively).  You can specify an ATR *multiple* and the ATR indicator's *period*. If *Trailing Stop* is selected, Position is exited at a Chandelier trailing stop from the closing prices using a 22-period Average True Range. 

When *ATR at Entry Bar* is checked, the ATR value is fixed at the bar of entry, otherwise it's evaluated at every bar while the Position remains open.

> Option does not apply to Trailing Stops.
## Same-Bar Exits with Exit Blocks
Some Exit Blocks have a check box that you can activate to enable same-bar Exits. This will allow your Building Block Strategies to employ pre-determined limit and stop Exits that get submitted after the Entry is filled. Same-bar Exits do not use any accompanying Conditions, only the limit/stop order price of the Exit comes into play.

 %{color:blue}**Tip!**% 
> For even more blocks, check out the [Power Pack Extension](https://www.wealth-lab.com/extension/detail/PowerPack). 
