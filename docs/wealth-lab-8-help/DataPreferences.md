# Data Preferences

 - [take me there now](action:DataPreferences)

---
## Data 
This interface lets you establish and save your data preferences, including colors, what is plotted, and other options. When you make a change, it is reflected in the currently active chart window. Use the **Apply to All Charts** button to apply the changes to all chart windows.

#### ☑ Amount to Load into Chart (Chart Data Range)
This controls how much data is loaded into a [Chart Window](Chart). It does not impact charts in a [Strategy Window](Strategies), since data range there is controlled by the Strategy Settings you establish. Setting a value here can be useful, especially for intraday charts which could easily have hundreds of thousands of bars of data if left uncapped.

#### ☑ Load all Data for Daily+ Scales
If this option is enabled, charts with a scale of Daily or higher will always load all data, ignoring the previous setting. Once again, this does not apply to charts in a [Strategy](Strategies) window.

#### ☑ Default Symbol for Charts
This controls what symbol is initially charted when you open a new [Chart Window](Chart).

#### ☑ Filter out Pre/Post intraday market data
This default setting is used to filter data outside of regular market hours for [Chart](Chart) and [Strategy](Strategies) Windows.  You can change the "Filter Pre/Post" setting on the fly in the Chart's status bar.

For market hours see [Markets & Symbols](MarketsAndSymbols). 

---
## Data Corrections

#### ☑ Refresh Daily+ Data if Update results in %change greater than
Enabling this option will refresh a symbol's Daily (and W/Q/Y) data when the bar after the cached data opens at a price greater than the specified percentage from the previous close.

#### ☑ Refresh Daily+ Data whenever a new Split or Dividend occurs
Enabling this option will refresh a symbol's Daily (and W/Q/Y) data when a new split or dividend is detected in the historical provider's companion event provider.

#### ☑ Allow Data Corrections from Historical Providers
Apart from corrections for splits or special dividends, historical providers like Wealth-Data may also add ad-hoc corrections when errors are found in specific bars. Use this option to get all of a provider's corrections during the symbol's next update.

#### ☑ Enable Streaming Tick Outlier Filter
This preference impacts the tick data that streams in from [Streaming Data Providers](StreamingProviders), 
for example in [Streaming Charts](StreamingCharts) and the [Quotes](Quotes) tool. You specify a percentage threashold here, and any incoming tick that is further away from the previous tick than this amount is ignored. This can eliminate spurious price spikes that occiasional occur in various Streaming Providers.

[![Data Corrections](http://img.youtube.com/vi/WbLnO3cEosI/0.jpg)](https://www.youtube.com/watch?v=WbLnO3cEosI&t=194s "Data Corrections")
