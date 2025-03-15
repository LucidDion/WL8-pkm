# FilterSets

 - [take me there now](action:FilterSets)

The **Filter Sets** tool allows you to create and manage **Filter Sets**, which contain filter conditions that can be applied to [Optimization](Optimization) results or used in the [Strategy Genetic Evolver](StrategyEvolver).

## Filter Conditions
Each Filter Set is composed of one or more Conditions that are based on a [Performance Metric](MetricPreferences). For example, to include only results that have a high Sharpe Ratio and a low Drawdown you could add the following Conditions:

 - SharpeRatio > 1.00
 - MaxDrawdownPct > -20.00

## Filters in Optimizations
You can use Filter Sets while examining the results of a standard [Optimization](Optimization), in the Tabular Results Optimization Visualizer. Select the desired Filter Set, enable filtering using the check box, and the Tabular Results will be filtered out to include only the items that pass the Filter Conditions. When you change the Filter in the Filter Sets Tool and click Save, the Optimization Tabular Results are immediately updated to reflect the change.

## Filters in the Strategy Evolver

The [Strategy Evolver](StrategyEvolver) can be configured to eliminate candidate Strategies that do not pass the selected Filter Set Conditions. Enable this behavior by checking the check box in the Evolver, and select which Filter Set to use from the drop down list.

## Pushing Results into the Filter Sets Tool

In both the Optimization Tabular Results View, and the Strategy Evolver, you can click the **Push Results to Filter Sets Tool** button to load the current items into the Filter Sets Tool. Once loaded, all of the Results appear in the Filter Sets Tool, and the items that did not pass the currently selected Filter Set Conditions are dimmed out. You can manipulate the Filter Conditions and immediately see how the changes effect the Results in the list.
