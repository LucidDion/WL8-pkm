# Advanced Strategy Settings

### Retain NSF (Not Sufficient Funds) Positions

**NSF Positions** are trades that result in a **Transaction** but that do not become part of the backtest due to insufficient buying power. This switch has the following effect:  

**Checked (default)**  
When checked, backtests retain **NSF Positions**.  Even though these positions do not influence the backtest, strategies execute as if the NSF Positions are *Open* and will generate exit Signals for them.  **Use this option for live trading if there's a chance you entered a NSF Position in a live account.**  
 
**Unchecked**  
Backtests discard **NSF Positions** and they are not added as Open Positions.  A typical strategy using single position logic will continue to process the entry logic block.  The main effects are:
 
1. Strategies have the opportunity to trigger and enter Positions immediately following trades rejected due to buying power. 
2. Large simulations may run noticeably faster. 

%{color:blue}**Note!**%  
> When *Live Positions* is enabled in the [Trading Preferences](TradingPreferences), NSF Position signaling is essentially disabled in the Strategy Monitor and Streaming Strategy windows.

**Script Override for Retain NSF Setting**  
You can override the Retain NSF setting in the `Initialize()`method for individual Strategies by assigning a value to `BacktestSettings.RetainNSFPositions`.  Boolean **true/false** provides the *checked/unchecked* behavior, respectively, described above. 

> For a demonstration, see the [NSF Position tutorial](https://youtu.be/HXA-AetQ3Jk) on our YouTube Wealth-Lab Support channel.

[![What are NSF Positions?](http://img.youtube.com/vi/HXA-AetQ3Jk/0.jpg)](http://www.youtube.com/watch?v=HXA-AetQ3Jk "What are NSF Positions?")

---

### Use Granular Limit/Stop Processing
Assigning a Transaction.Weight instructs Wealth-Lab which trades to prioritize on bars that reject trades, i.e., generate **NSF Positions** (see above).  A realistic simulation when backtesting **Stop / Limit  Strategies** require that higher priorities be assigned to trades that would have been filled *earlier* chronologically.

When **Use Granular Limit/Stop Processing** is checked, Wealth-Lab prioritizes (processes) transactions based on the *time of day* that the transaction would have been filled.  It's accomplished by searching through intraday data at the specified **Granular Scale**. 

While this feature would generally be used while backtesting Daily and higher timeframes.  You can use it for large intraday scales too - 30-minute or hourly bars for example.  

> **Notes:**  
> - **This feature will slow down backtests.**   The lower the Granular Scale, the more memory and resources required.
> - If multiple transactions filled at the same granular time of day are fighting for trading capital, Wealth-Lab chooses a random candidate. 
> - A user-assigned Transaction.Weight will influence trade priority only if no intraday data exists to cover the date of the signal. 
> - If the **Granular Scale** is greater than the base scale under test, Granular Limit/Stop Processing is ignored. 

For a demonstration, see this Youtube video:

[![Use Granular Limit/Stop Processing](http://img.youtube.com/vi/TajAJ4htNb0/0.jpg)](https://www.youtube.com/watch?v=TajAJ4htNb0&t=250s "Use Granular Limit/Stop Processing")

---

### Update Granular Intraday Data during Backtest
When this setting is enabled (which it is by default), WL8 will perform on-demand updates of the Granular Processing intraday data during the backtest. This can significantly slow down performance, so if you are sure your intraday data is already updated, you can disable this setting.
