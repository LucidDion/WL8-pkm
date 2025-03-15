# Strategy Evolver
 - [take me there now](action:StrategyEvolver)

 
## Concept
The Strategy Genetic Evolver generates randomized Strategies over many **Generations**, keeping and mutating the best performing Strategies. You can use the Evolver results to discover the type(s) of Strategies that perform well in backtests of the historical data that you select. 

[![Evolve a Trading Strategy](http://img.youtube.com/vi/vaH6XBwo1gQ/0.jpg)](https://www.youtube.com/watch?v=vaH6XBwo1gQ&t=192s "Evolve a Trading Strategy")

---
## Settings
The upper toolbar of the Evolver lets you control the DataSet, Scale, and Data Range. It also contains shortcut buttons that take you to the [Performance Metrics Preferences](MetricPreferences), and the [Evolver Preferences](EvolverPreferences).

The configured [Metric Preferences](MetricPreferences) are important because they control the columns that are displayed for each generated Strategy. As long as you have not run any Generations yet, changing the Metrics in Preferences will cause the columns to regenerate.

The second toolbar has controls that let you **Start** the generation process, **Stop** it, and subsequently **Resume** it. **Resuming** a **Stopped** run will let you pick up where you left off, while **Starting** again will completely randomize the Strategies and reset the Generation counter to 1.

To the right of these controls is a set of two drop down controls that control the **Target Metric** of the genetic evolution. Here you specify a single performance Metric, and whether high or low values of the Metric are desirable. As the genetic evolution continues, the resulting Strategies will be sorted by the specified Metric, and lower performing instances will be eliminated.  


![Wealth-Lab's Strategy Evolver](https://www.wealth-lab.com/Images/WLHelp/StrategyEvolver.png)

---
## Initial State

When you first open the tool, you'll see 20 Strategies in the list. Some of the Strategies are pre-configured, and some are randomly generated. Here is the breakdown:

 - **Slots 1-5** - Preconfigured Strategies
	 - **Slot 1** - RSI Overbought/Oversold
	 - **Slot 2** - 3x2 Consecutive Closes Down/Up
	 - **Slot 3** - SMA 50/200 Crossover
	 - **Slot 4** - MACD Crosses Signal Line
	 - **Slot 5** - DipBuyer 2% Limit below Low, Highest 2-bar High Limit
 - **Slots 6-10** - Randomly generated Strategies, unless you assigned specific Strategies to these Slot(s) in the [Evolver Preferences](EvolverPreferences).
 - **Slots 11-20** - Randomly generated Strategies.

---
## Evolving Generations
During each Generation processing, the Evolver does the following:

 1. Runs a **backtest** on each Strategy using the specified Settings above and collects all performance Metrics. 
 2. Applies the **Filter Set**, if enabled, and eliminates Strategies that do not conform to the filters. Also eliminates any Strategy with a Net Profit < 0.
 3. **Sorts** the Strategies by the specified Target Metric.
 4. **Retains** the top 5 resulting Strategies, and eliminates the rest.
 5. **Mutates** each of the top 5 Strategies, resulting in 5 new variations.
 6. **Generates** new randomized Strategies to round out the list to 20 again.
 7. **Increments** the Generation counter and goes back to step 1.

Mutations for strategies can change the % of Equity position sizing value (displayed on the right above the Strategy pane), 
conditions, indicators and parameters used for conditions.  

---
## ☑ Enable Apex Strategy Collection
After several hours, the Evolver will usually converge on a number of nearly identical Strategies that dominate the top ranks. At this point the probability of discovering new strategies with better performance is highly diminished. 

With *Apex Strategy Collection* enabled, the following occurs when *strategy convergence* is detected based on the *n-Strategies are x% similar* criteria specified:  
1. WealthLab puts the single top-ranked Strategy into the **Apex Strategies** list. 
1. The current evolution is discarded and cleared.
1. A completely new evolution begins from generation 1 as if the Evolver window were restarted. 

Let the Strategy Evolver run as long as you want and check for the best **Apex Strategies**. Open, test, save the ones you want keep. 

[![Strategy Evolver Apex Strategies](http://img.youtube.com/vi/N-SQAxLfxcg/0.jpg)](https://www.youtube.com/watch?v=N-SQAxLfxcg "Strategy Evolver Apex Strategies")

---
## ☑ Use Filter Set

The **Filter Set** toolbar control lets you optionally specify a performance Metric filter that each Strategy must pass in order to be included in the next Generation. The default Filter Set is named **Default Evolver Filter**. This Filter Set contains the following two filters:

 - **LargestBarsHeldAsPctOfHistory < 20** - This ensures that the Strategy is not simply buying and holding, and accidentally showing inflated results by happening to pick a high performing asset from the DataSet.)
 - **NSFRatio < 2** - This ensures that the number of NSF positions remains at a reasonable level compared to the number of non-NSF positions. As **NSFRatio** increases, the backtest results become less stable, and more likely to substantially change each time it is run.

> **Note:** 
> Define your own Filter Sets at any time using **[Tools > Filter Sets](FilterSets)**.  

**Push to Filter Set Tool**  
See [Pushing Results into the Filter Sets Tool](FilterSets). This button applies only to the Strategies in the *Evolver* tab, not *Apex Strategies*.

---
## Viewing and Opening an Evolved Strategy
At any point, you can select one of the Strategies in the list to see its [Building Block](BuildingBlocks) composition in the pane to the right. Evolved Strategies are ultimately expressed as [Buildng Block Strategies](BuildingBlock). From here you can open the Strategy in a new [Strategy Window](Strategy), at which point you can further modify it and/or save it your your [Strategies](Strategies) list. You can also open any of the Strategies by double-clicking them in the list.

---
## Evolver Preferences

Go to the [Evolver Preferences](EvolverPreferences) tab in the [Preferences](Preferences) tool to control more overall settings of the Strategy Genetic Evolver. It's required to leave selected at least one type of entry and exit pair (Buy-Sell and/or Short-Cover) as well as condition(s) to trigger trades for market order types.  If no conditions are selected when required, a random set will be inserted. **Preferences are applied to the next Strategy Genetic Evolver window that you open**.
