# Custom Indicators
**Note**: Creation and use of Custom Indicators is available only when you run WeatlhLab in [Windows Administrator](Navigating) mode.

 - [take me there now](action:CustomIndicators)

You can program your own custom [Indicators](Indicators) in WeatlhLab using C# code and the **Indicator Builder** tool. The **Indicator Builder** provides a user interface where you can define your Indicator's properties and parameters, and it will then generate the boilerplate C# code to get you started. You need to complete your Indicator by coding the implementation of the **Populate** method.

### Launch the Indicator Builder
1. File menu > New Customer Indicator (C#)  Ctrl+Shift+I, or, 
2. **New Indicator** button atop the [Indicators](action:Indicators) sidebar

---
## Indicator Properties

### Indicator Name ... Description
Start your Custom Indicator by providing descriptive details:
- Name
- Class Name (automatically based on Name, but you can change if required)
- Default Plot Color and Style
- Pane Tag
- Description

### Indicator Parameters
In this section, add all the parameters one by one that your indicator will use. The first parameter's label should be ***source*** and should be either a **TimeSeries** or a **BarHistory** type. This represents the source data that is used to populate the Indicator or at least to synch its data to the symbol being charted or processed.

Click **Add Parameter** for each one.  When finished adding parameters, clicking **Generate Indicator Code** takes care of the "house keeping" for an indicator to work seamlessly in WeatlhLab.  You only need to program the **Populate()** method to calculate and assign values to the indicator's ***Values*** property. 

Assigning values can be accomplished in more than one way, and is best shown by reviewing samples of completed indicators.  For samples, click ATR, RSI, or SMA at the top of the Code view. You can go back to the Properties page and generate the code again to start with a fresh code template. 

---
## Charting your Indicator
As you develop and compile your Indicator in the Builder, you can switch to the **Chart** tab to see your Indicator on a chart.

---
## Saving your Indicator
After you are satisfied that your Custom Indicator is working correctly, press the **Compile** button and check the pane at the bottom. If it "Compiled OK" then you can click the button to **Save to My Indicators Folder**. Your Indicator appears in the [Indicators](Indicators) list, under a folder labeled **My Indicators**.

---
## Editing your Indicator
To edit, right click your indicator in **My Indicators** and choose Delete or Edit.  **Edit** opens your indicator in a Code window to make and save changes.  You must close and restart WeatlhLab in Admin mode in order to use the changed indicator. 

---
## IndicatorBase Reference
All Indicators in WeatlhLab are .NET classes that descend from the **IndicatorBase** base class. For more details about **IndicatorBase**, and custom Indicator development in general, see the [IndicatorBase Class Reference]([IndicatorBase (WeatlhLab Framework) - WealthLab](https://www.WeatlhLab.com/Support/ApiReference/IndicatorBase)) on [WeatlhLab.com](https://www.WeatlhLab.com).

---
## Limitations:

1. A custom indicator cannot reference another custom indicator.
2. Creation and use of Custom Indicators is available only when you run WeatlhLab in Windows Administrator mode.

