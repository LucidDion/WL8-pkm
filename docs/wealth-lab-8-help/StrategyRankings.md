# Strategy Rankings

 - [take me there now](action:StrategyRankings)

Use **Strategy Rankings** to compare backtest results side-by-side for a list of Strategies. All of the Strategy runs will share the same DataSet, Scale, Data Range, and Position Size.

![Strategy Rankings Window](https://www.wealth-lab.com/Images/WLHelp/Rankings2.png)

## Configure and Run Rankings

 1. Launch a New Strategy Rankings Window from the Tools menu, or use the shortcut Ctrl+Shift+K.
 2. Specify the **DataSet** or a single **Symbol**, **Scale**, **Backtest Range**, and **Position Size** to be applied in the next step.
 3. Drag and drop Strategies individually, or folders of Strategies in the Rankings tool.  If you wish to allow MetaStrategies to be included, be sure to check the appropriate checkbox in the toolbar.
 4. *Optional:* Click to select a Strategy and use the **Change Parameters** button to modify parameters.  
 5. Repeat Steps 2 - 4 as required
 6. Use **Choose Metrics** to specify the Metrics to be shown for Rankings (and Optimizations). Has effect only if "Run Backtests" has not yet been completed.
 7. Click **Run Backtests** to populate results. 

## Symbol-by-Symbol Rankings

Select the **Symbol Rankings** tab to run a ranking of a single Strategy against each individual symbol in the selected DataSet. You can optionally have the Symbol-by-Symbol Rankings use a 100% of Equity Position Size by checking the "**Use 100% for by-Symbol**" in the toolbar. When selected, this option overrides the established Position Size.

---
 
### Rotation Strategies
**Position Sizing** for Rankings is overridden to use the Percent of Equity sizing based on the Number of Symbols to Hold, which is specified in the Rotation Strategy Settings. 

To change settings for Rotation Strategies, double click, change, and save *before* running the Rankings.  

---
## Strategy Errors
Runtime errors that don't allow a strategy to run to completion will be flagged with a red alert icon. Fix the error in the Strategy Window, save, and finally delete/re-add the Strategy.  Alternatively re-launch Rankings tool from a saved Workspace.

---
## Workspace Support
Save one or more Rankings tool configuration by saving the [Workspace](Workspaces). 
