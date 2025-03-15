# Event Providers

- [take me there now](action:EventProviders)

This list displays the Historical **Event Providers** available to serve fundamental, chart pattern, news, or any type of event. The providers you see here will depend on what [Extensions](Extensions) you have installed.

---
## Selecting Event Providers
When you check the box next to an ** Event Provider** Wealth-Lab will attempt to load its event data whenever it loads historical price data. Since this process can be time consuming be sure to *keep Event Providers turned off* unless you really need them.

---
## Where Event Data is Used
Events are used in the following places in Wealth-Lab:

 - In [Charts](Chart), event data will appear as small icons above the price bars. You can turn off plotting of events entirely in [Chart Preferences](ChartPreferences). For finer control of which fundamental data is plotted, see below.
 - Certain [Indicators](Indicators), namely **Fundamental** and **FundamentalRatio**, use fundamental data and will produce blank results if appropriate fundamental data is not enabled.
 - You can use fundamental data in [Building Block Strategies](BuildingBlock) by selecting the **Fundamental** indicator wherever an Indicator parameter is presented.
 - You can access all types of event data in [C#-Coded Strategies](CSharpCodeBased) via the **BarHistory** class. See the `EventDataPoints` and `GetEventDataPoints` entries in the **BarHistory** page in the [QuickRef](QuickRef) for examples.
 
---
## Controlling which Event Data is Plotted
In [Chart Preferences](ChartPreferences), you can turn on and off plotting of event data in [Charts](Chart). For finer control of which event data items are plotted and returned via `bars.GetEventDataPoints,` click an **Event Data Provider** from the list. This brings up a second list of event data items this provider supplies. To plot specific items in [Charts](Chart) check their boxes in the list. 

---
## Controlling Event Data in Strategies
Summarizing, the checkbox next to the Event Providers serves three purposes: 

 1. To select Providers that you intend to update, and, 
 2. To enable a Provider's events for display on charts, and,
 3. To make the Provider's EventData available to strategies.

Event Providers may use the same name for an event, which could cause conflicts or duplication 
in a strategy. You can overcome this by either unchecking one of the conflicting providers or by conditionally testing the EventDataPoint ProviderName property to ensure you're using the one you want.
