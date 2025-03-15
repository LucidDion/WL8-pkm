# C# Coded Strategies

 - [take me there now](action:CSharpStrategy)

You create these [Strategies](Strategies) by using the [C# programming language](https://en.wikipedia.org/wiki/C_Sharp_%28programming_language%29) to implement your trading logic. Wealth-Lab **Strategies** are .NET classes derived from the **UserStrategyBase** base class. Your **Strategy** code creates a new class that inherits from **UserStrategyBase**, and overrides key methods such as **Initialize** and **Execute**. 

---
## Declaring Variables
Declare class level variables at the bottom of the class definition.  This includes variables that will hold references to [Indicators](Indicators) that your **Strategy** will use.

---
## Initialize
Override the **Initialize** method to perform any one-time initialization that your **Strategy** requires.  The Wealth-Lab **Backtester** calls the **Initialize** method once, prior to beginning the backtesting main loop.  Here you can create any instances of [Indicators](Indicators) that you declared in the variable declaration section.  The **Initialize** method passes you one parameter, **bars**, which is the instance of the **BarHistory** object that represents the historical price/volume data being backtested.

---
## Execute
The Wealth-Lab **Backtester** works by keeping all of the data for the symbols in the [DataSet](DataSets) synchronized by date/time, and processing them bar by bar.  For each bar of data, Wealth-Lab calls your **Strategy's** **Execute** method.  This is where you implement logic to determine if your **Strategy** needs to enter or exit any positions.  Wealth-Lab passes you two parameters in the **Execute** method:

 - **bars** - the instance of the **BarHistory** object that your **Strategy** is currently processing
 - **idx** - the index into the **BarHistory** object, tells you which data point, or bar of data, is currently being processed.
## Accessing Data from the BarHistory
A common operation your **Strategy** will perform is accessing the data in the **BarHistory** object.  You'll use the current and prior market data to make decisions about whether to open or close positions. You can access the **Open**, **High**, **Low**, **Close**, and **Volume** by using the corresponding properties in **BarHistory**.  Refer to the [BarHistory](BarHistory) class reference for more details.

---
## Working with Indicators
[Indicators](Indicators) feature prominently in trading **Strategies**.  In Wealth-Lab, Indicators are .NET classes derived from the **IndicatorBase** base class.  **IndicatorBase** is itself derived from the **TimeSeries** class, which provides access to a history of floating point **double** values.  To work with a specific **Indicator** in your code, you will need to determine its .NET class name.  This is not always the same as the **Indicator** name or abbreviation.  Use the [Indicators](Indicators) list to determine an Indicator's **.NET class name**, as well as see the Indicator's **constructor** code.  

![enter image description here](https://www.wealth-lab.com/Images/WLHelp/IndicatorClassName.png)
 
Armed with this information, we can code up a simple **Strategy** that creates and plots the **Coppock Indicator**:
```csharp
using Wealth-LabBacktest;
using Wealth-LabCore;
using Wealth-LabIndicators;

namespace Wealth-Lab
{
    public class MyStrategy1 : UserStrategyBase
    {
        //create indicators and other objects here, this is executed prior to the main trading loop
        public override void Initialize(BarHistory bars)
        {
			myIndicator = new Coppock(bars.Close, 14, 11, 10);
			PlotIndicator(myIndicator);
        }

        //execute the strategy rules here, this is executed once for each bar in the backtest history
        public override void Execute(BarHistory bars, int idx)
        {
        }

		//declare private variables below
		Coppock myIndicator;
    }
}
```

---
## Placing Trades
Call the **PlaceTrade** method to place a simulated trade in your **Strategy** code.  The **PlaceTrade** method contains parameters where you specify the **transaction type** (**Buy**, **Sell**, **Short**, **Cover**), the **order type** (**Market**, **Limit**, **Stop**), and the **order price** (for **Stop** or **Limit** orders).   Wealth-Lab's **Backtester** always executes  the hypothetical trade on bar of data *following* the bar currently being processed.  This simulates real world trading, as you examine the current trading bar's action, and then make decisions for orders to place on the following bar.

**Example:**  Place a buy order at market open
```csharp
PlaceTrade(bars, TransactionType.Buy, OrderType.Market);
```
**Example:**  Place a limit sell order at 1% above the current bar's high price
```csharp
PlaceTrade(bars, TransactionType.Sell, OrderType.Limit, bars.High[idx] * 1.01);
```

---
## Splitting Positions
**PlaceTrade** always returns a **Transaction** object. You can the transaction to enter or exit precisely the number of shares desired by assigning a value to the Quantity property.  When you specify a quantity less that the total shares of a Position, Wealth-Lab will automatically split the *position matched** and exit the quantity you specify. 

**Example:**  Exit half of the shares determined by the last Position*.
```csharp
Transaction t = PlaceTrade(bars, TransactionType.Sell, OrderType.Market);
t.Quantity = LastPosition.Shares * 0.50; 
```
Note! Even though the number of shares of the **LastPosition** is specified, if multiple Positions are active, a Position *other than the LastPosition* may be sold and/or split. Instead of ```PlaceTrade``` you can use ```ClosePosition``` to specify a Position object to exit. 

*See also:  [Backtest Preferences](BacktestPreferences) > Position Matching

---
## Debugging
You can use the **Debug Log** to view output from your **Strategy** code.  Call the **WriteToDebugLog** method to write a line of output to the **Debug Log**.  The **Debug Log** tab will only appear as the last tab after you've actually output something by calling **WriteToDebugLog**.

---
## Linking to an External Source Code File
You can use the "chain" button in the C# Code Editor's toolbar to select an external file to link this Strategy's code to. The file must be a C# source code file with a .cs extension. Changes you make to the external file (for example, in Visual Studio or another editor like Notepad) will automatically update in the WL8 Strategy Window Code Editor. However, this is a *one-way linkage*. If you change the code in WL's Editor, and then save the Strategy, the changes will not be reflected in the external source code file. Furthermore, the next time you open the Strategy or the next time the external source code file is saved, your changes in Wealth-Lab will be lost.

---
## Class References
Consult the following class references for more details about the Wealth-Lab C# framework. Also, leverage the integrated [QuickRef](QuickRef) help system as you code your **Strategies**.

 - [UserStrategyBase](https://www.wealth-lab.com/Support/ApiReference/UserStrategyBase  )
 - [BarHistory](https://www.wealth-lab.com/Support/ApiReference/BarHistory)
 - [TimeSeries](https://www.wealth-lab.com/Support/ApiReference/TimeSeries)
 - [IndicatorBase](https://www.wealth-lab.com/Support/ApiReference/IndicatorBase)
 - [EventDataPoint](https://www.wealth-lab.com/Support/ApiReference/EventDataPoint)
 - [Parameter](https://www.wealth-lab.com/Support/ApiReference/Parameter)
 - [PeakTroughCalculator](https://www.wealth-lab.com/Support/ApiReference/PeakTroughCalculator)
 - [Position](https://www.wealth-lab.com/Support/ApiReference/Position)
 - [Transaction](https://www.wealth-lab.com/Support/ApiReference/Transaction)

See the latest API Documentation online at wealth-lab.com!
- [API Reference](https://www.wealth-lab.com/Support/ApiReference)
- [Extension API Reference](https://www.wealth-lab.com/Support/ExtensionApi)
