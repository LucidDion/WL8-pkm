# Chart Preferences

 - [take me there now](action:ChartPreferences)

This interface lets you establish and save your chart preferences, including colors, what is plotted, and other options. When you make a change, it is reflected in the currently active chart window. Use the **Apply to All Charts** button to apply the changes to all chart windows or use **Auto-Apply** to immediately apply changes as you make them. 

---

## Themes
A set of chart preferences can be saved as a **Theme**. Wealth-Lab ships with a **Light** and a **Dark** Theme. You can also create your own Theme by using the **Save as New Theme** button.

---
## Chart Style
Select the default chart style to use when opening a new chart or Strategy window.  If needed, you can change the Chart Style and its settings on the fly in the Chart's toolbar. 

---
## Other Settings
Configure the default behavior for new chart and Strategy Windows for **Bar Spacing**, top/bottom **Pane Margins**, **Separator Thickness**, **Cursor Line Thickness**, and **Default Indicator Set**. The selected [Indicator Set](Chart) will appear only for new Chart windows, not Strategy windows. 

The checkbox options below control the behavior when opening a new chart or Strategy window. You can change  these settings on the fly where described.

- **Show Volume Pane** - show/hide Volume Pane with chart right click menu > *Volume Pane Visible*
- **Show Event Item Icons** (e.g., Fundamental Items, Chart Patterns, etc.) - show/hide Event Icons with chart right click menu > *Show Event Icons*
- **Show Trade Arrows** - show/hide rendering of entry/exit arrows.  You can control this in Strategy code with the *ChartDisplaySettings* property **DrawTradeArrows**.  See *SetChartDrawingOptions* in the QuickRef.
- **Price Pane Log Scale** - control in chart toolbar: *log* button
- **AntiAlias** - makes lines in charts smooth at the expense of some blurriness.
- **Disable Rendering Optimizations** - When not checked, a Line style is used in place of Bar or Candlestick style for bar spacings 1 and 2.  Disabling rendering optimizations may hurt performance when drawing many bars on large screens.
- **Show Status Bar** - control in chart toolbar: Show/Hide Status Bar button
- **Always Show Toolbar** - control in chart toolbar. When disabled, the chart toolbar appears on mouse overs.
- **Show Trade Signal Lines** - draws a horizontal signal line for stop/limit signals in Strategy-driven charts.
- **Use Win/Loss Trade Arrow Colors** - Switch between two color schemes for the trade arrows.  The Win/Loss color scheme show winning/losing trades as green/red arrows, respectively, as shown below. 
- **Size Chart (Vertical) to Indicators** - rescales y-axis so that indicator plots are visible.
- **Adaptive Scale Stop/Limit** - rescales y-axis to ensure stop/limit values are visible when plotted using `PlotStopsAndLimits()`.

| Default | Win/Loss | Description      |
|---------|----------|------------------|
| ![Buy](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Buy.png)| ![Buy W/L](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_LongEntry.png) | Long entry (Buy) |
| ![Sell](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Sell.png) | ![Long Winner](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_SellWinner.png) | Long Exit (Win) |
| ![Sell](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Sell.png) | ![Long Exit Loser](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_SellLoser.png) | Long Exit (Loss) |  
| ![Short](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Short.png) | ![Short W/L](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_ShortEntry.png) | Short Entry (Short) |  
| ![Cover](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Cover.png) | ![Short Winner ](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_CoverWinner.png) | Short Exit (Cover, Win) |  
| ![Cover](https://www.wealth-lab.com/Images/WLHelp/Triangle_v7_Cover.png) | ![Short Loser](https://www.wealth-lab.com/Images/WLHelp/Triangle_v6_CoverLoser.png) |  Short Exit (Cover, Loser) |  

