# Standard Optimization
To run a Standard Optimization, click on the Standard tab and click the green Start Optimization button. 

## Optimization Results
Upon completing an optimization, **Optimization Result Viewers** appear that allow you to explore a completed optimization in a number of different ways, much the same was as [Performance Visualizers](PerformanceVisualizers) let you explore a backtest performance.

### Tabular
The table contains the metrics for all of the optimization runs. Click up to 3 column headers for a multi-sort. Right click on a row to run a backtest using those specific Parameter values or to save the row's Parameters as the new default values for the [Strategy](Strategies).

To **filter** the Tabular results, click **Push Results to Filter Set Tool** to launch and populate a **Filter Sets** window. Add one or more filters in **Filter Sets** to see how many observations met each individual filter criteria. You can save and re-use common filter criteria.

### Parameter History
The history view shows you how the **Parameter** values changed over the course of the optimization. It's not relevant for **Exhaustive** optimizations but allows you to see how the **Shrinking Window** optimization zeroed in on its **Parameter** values.

### Surface Graph
This 3D view lets you select *two* **Parameters** and see a rotatable surface graph of an optimization metric that you select. Left click and drag to change the perspective or right click and drag to move the scale. You can also use the controls provided to establish default values for any **Parameter** not included in the graph.

**Extensions!**  
You may see more **Optimization Result Viewers**, depending on which [Extensions](Extensions) you have installed.
