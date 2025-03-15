# Optimization

The process of **optimization** involves running a backtest of a [Strategy](Strategies) using different combinations of values for the Strategy's **Parameters**.  The robustness of a Strategy can be determined by how healthy the model's performance looks over a range of Parameter values.

---
## Strategy Parameters
Strategies can have **Parameters**, numeric values that have a **minimum**, **maximum**, and an **increment**.

In [Building Block Strategies](BuildingBlock), you create **Parameters** by clicking the **Make Optimizable** buttons next to the entry fields in the various [Building Blocks](BuildingBlocks). Click to see how to set up [Optimization Parameters in Building Blocks](https://youtu.be/xaUJ9tZWUcY) on our YouTube channel.

In [C# Coded Strategies](C#CodeBased), you create **Parameters** by calling the **AddParameter** method from within your Strategy's **constructor**, as shown in the next snippet. 

```csharp
namespace WealthScript123
{
	public class MyStrategy : UserStrategyBase
	{
		public MyStrategy()
		{
			AddParameter("Period", ParameterType.Int32, 20, 10, 50, 5);
			AddParameter("Std Dev", ParameterType.Double, 2.0, 1.0, 3.0, 0.5);
		}
```

You can access the **Parameters** using the ***Parameters*** property. Each Parameter is an instance of the [Parameter](Parameter) class.  To access a Parameter's value, use its **Value** property.  The [Parameter](Parameter) class also provides a suite of helper methods, such as **AsInt** and **AsDouble**, allowing you to access a Parameter's value in a strongly-typed manner.

**Example**: 
This example accesses the model's first and second parameters by using index numbers 0 and 1.
```csharp
int period = Parameters[0].AsInt;
double sd = Parameters[1].AsDouble;
```
---
## Selecting a Strategy to Optimize
Strategies that are optimizable have an extra icon next to their name to show that parameters are configured for optimization.  From the [Strategies](Strategies) list, left click one of these Strategies to select it and then click the **Optimize** button. Alternately, right click a **Strategy** directly from the [Strategies](Strategies) list and select the **Optimize Strategy** menu item.

---
## Optimization Settings
There are three different modes of optimizations in Wealth-Lab: 

- [**Standard Optimization**](StandardOptimization)
- [**Walk-Forward Optimization**](WalkForwardOptimization)
- [**Symbol by Symbol Optimization**](SymbolBySymbolOptimization)

For each of the three modes, you can select the **Parameters** to optimize by checking them in the list.  An unchecked Parameter assumes its default value. 

Select the **Optimization Method** from the following options. More Optimization Methods may be available depending on the [Extensions](Extensions) you have installed. 

- **Exhaustive** - runs through every possible combination of Parameter values.  If the Strategy has more than a few parameters, this can lead to very lengthy optimizations.
- **Exhaustive (non-Parallel)** - same as above without the parallel processing.  Use this Exhaustive method if your Strategy uses shared variable data.  For example, BarHistory.UserData could be changed by other parallel runs leading to incorrect results. 
- **Shrinking Window** - uses randomized Parameter values and keeps honing in on the most profitable values as the optimization continues.

### Shrinking Window Optimizer Deep Dive
Permutations of an *Exhaustive Optimization* is easy to understand. Because every combination of parameters is tried, the optimum combination is guaranteed to be found. However, the whole point of the *Shrinking Window* is to optimize with a number of permutations far lower than exhaustive. It's meant as a shortcut - a way to find a decent result, which may not be the *optimum*.  

To clarify how *Shrinking Window* works imagine it's set to 4 [outer] runs and 4 passes and it's optimizing 1 parameter with a range of 0 to 100 step 5. The maximum number of permutations to be run will be 16, but you'll see it can even be fewer. 

Run 1 will do 4 passes with a window that is the full range of 0 to 100. It picks 4 random values snapped to the step value: e.g., 25, 65, 10 and 45. If 65 was the best value, Run 2 shrinks the window centered on 65, so the range is now 35 to 95.  

Run 2 generates 4 values: 40, 70, 55 and 65. Since 65 was already used in run one, it's ignored. If 55 was the best, Run 3 shrinks the window again centered around 55 and the new range is 35 to 75. The 4 new values come up 55, 70, 60 and 40. Only 60 hasn't been tried before so that's the only pass that gets run this time. And it turns out it's the best result so far.  

The last window shrinks again and is centered on 60 for and range of 45 to 75. The four new values generated are 60, 70, 65 and 45. All of these parameter values have been tested already so it doesn't need to perform any strategy runs this last window.  

Now that when multiple parameters are selected for optimization, *Shrinking Window* creates a separate window for each parameter, shrinking all parameter windows simultaneously. 

---
## Optimizing Positon Size
In the Strategy Window, Position Size settings area, you'll notice optimization buttons next to the **Starting** **Capital**, **Position Size Amount**, and **Margin Factor** fields. Each of these Position Size parameters can be enabled for optimization by clicking the associated button. If you want to turn off optimization for a Position Size parameter, click the button again, and then in the resulting **Optimization Parameter Editor**, uncheck the box at the top that says "Make this Parameter Optimizable".
