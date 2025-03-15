# Evolver Preferences

## Gene Roster
This list shows the available genes that the Evolver uses when generating random Strategies. You can disable specific genes by unchecking them. 

Entries and should be paired with appropriate exits, e.g., a Buy should have at least one of the Sell order types selected. Additionally, market orders require that you select at least one condition (Crosses Signal Line, Price Grid, Smoother Crossovers, etc.) to trigger. 

Changes to Preferences are applied to the next Strategy Genetic Evolver window that you open. 

## Buy/Short Entry Conditions
The tabs labelled "Buy" and "Short" are areas where you can drop [Condition Building Blocks](ConditionBlocks). Dropped Condition Blocks are injected into each generated Strategy's Long/Short Entries. These Conditions are not injected into template Strategies (see below.)

## Sell/Cover Exit Blocks
The tabs labelled "Sell" and "Cover" are areas where you can drop [Exit Building Blocks](EntryAndExitBlocks), and their accompanying [Conditions](ConditionBlocks). These Exit Blocks are injected below each corresponding Entry Block in each generated Strategy. The Exit Blocks are not injected into template Strategies (see below.)

[![Inject Exits into Evolver Strategies](http://img.youtube.com/vi/3oCJYZYFIsg/0.jpg)](https://www.youtube.com/watch?v=3oCJYZYFIsg&t=116s "Inject Exits into Evolver Strategies")

---
## Indicator Exclusions
**☑ Exclude Lengthy Run-Times**  
Some indicators are identified internally to have *lengthy calculation times*. Check this option to exclude these indicators from being used in the Evolver. 

You can add any other indicator to a list of exclusions to be ignored by the Evolver.  

> Note!  
> Preconfigured Strategies may use indicators that you want to be excluded. Before starting the Evolver, check each of the *top five* Strategies. Right click / remove strategies if they contain indicators that you want to be excluded.

---
## Slots 1-5 Templates
The first 5 Evolver slots are reserved for prototypical Strategies to use as a proven kickstart to the evolution. You can selectively disable one or more of these template Strategies by unchecking their boxes. To see what each template Strategy is composed of specifically, just open an Evolver window and click the first 5 Strategies in the list, observing their structure in the tree to the right.
## Slots 6-10 Custom Templates

The Evolver reserves slots 6-10 for [Building Block Strategies](BuildingBlock) that you can drag and drop here. Not all Building Block Strategies will be compatible with the Evolver, so you might receive a message indicating such after you drop a Strategy into a slot. You can remove a Strategy from a slot by right clicking.

## Default Position Size
By default, the Evolver will assign Position Size in a dynamic way. If preferred, you can force the Evolver to adopt a single specified Position Size. Optimization parameters for position sizing will be ignored here. 

---
## External Symbols
Some genes in the Evolver are applied to an external symbol. This Preference allows you do define the external symbols that the Evolver can draw from when this happens. A random symbol will be selected from the ones specified.

---
## Evolver Timeout
Evolved strategies have the specified amount of time to execute for each bar of the backtest for all symbols collectively. If a timeout is triggered, the backtest stops and the Strategy is discarded.