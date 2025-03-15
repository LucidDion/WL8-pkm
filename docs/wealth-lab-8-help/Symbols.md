# Symbols

 - [take me there now](action:Symbols)

Information for **Symbols** is used only when you enable **Futures Mode** in [Backtest Preferences](BacktestPreferences). When enabled, Wealth-Lab attempts to match each symbol in a backtest with one of the **Symbols** you defined here, and use the following properties:

 - **Point Value** - specifies the gain accrued for each one point movement of the symbol.
 - **Margin** - specifies the amount of capital required to take a one share/contract position in the symbol.
 - **Tick Size** - specifies the minimum granularity that the symbol trades at.

---
## Other Properties
 - **Market** - associate a symbol with a [Market](Markets) to establish when it trades.
 - **Display and Quantity Decimals** - overrides the settings specified in the [Market](Markets).  Many markets have symbols that have varying **Display** and **Quantity Decimals**.

---
## Symbol Matching
Wealth-Lab matches symbols to your **Symbol** entries using a # wildcard character. It will match a symbol of equal length. Below are some example **Symbol** wildcard matching results:

 - **AB####** - matches AB0119 and AB0520 but not AC0119 or AB01
 - **ES####** - matches ES0119 and ES1218 but not ES412 or ESX0119

---
## SymbolsV2.txt
Wealth-Lab saves your **Symbols** in the [SymbolsV2.txt](action:SymbolsTxt) file, in your 
[User Data folder](action:DataFolder), which you can quickly access from **File > Open Wealth-Lab User Data Folder**. 

---
## Set Commission
Sets the commission amount on a Symbol basis. Use this facility in combination with the [Backtest Preference](Backtest Preferences) so that backtests use the Symbol's commission amount instead of the amount(s) defined by the Market's Set Commission facility or in Backtest Preferences.  
