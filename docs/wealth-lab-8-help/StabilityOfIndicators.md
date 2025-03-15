## Stability of Indicators

Traders new to technical analysis (and some not so new) often assume that they can apply a technical indicator as soon as it begins churning out "valid" values. For many indicators such as *SMA, WMA, StochK*, etc., the assumption is fine. For example, the value of a 20-period Simple Moving Average (SMA) will always be the same at the end of the same 20 bars. Values of these indicators at the end of the Period are not affected by data prior to the Period.

 Another large group of indicators such as *EMA, WilderMA, RSI, MACD, Kalman*, etc. are in fact, calculated using the indicator's own previous values. You're likely to find that progressively-calculated indicators like these generally have reduced lag, but that the initial short-term values that they produce are unstable. 

---
## Avoid Using Unstable Indicator Values 

Some indicators can produce wildly different results in the short term. The trick is to understand the indicators that you're using, and to ignore their values until they're stable. For meaningful and reproducible results from a trading strategy, you must use indicators when they're stable. Alternatively, see the *Programming Pattern Workaround* below. 

You can ignore trading with initial indicator values by setting the [**StartIndex**](action:QuickRef) on a bar index after which the longest indicator is estimated to be stable. For the four 20-period indicators in the example, you may have noticed that the RSI requires a significant amount of "seed data" to stabilize. Consequently, we would assign a StartIndex = 60 in a Strategy's Initialize() method and preferrably StartIndex = 120 if sufficient test data is available. A reasonable rule of thumb is to ignore progressively-calculated indicators for 3 to 4 times their period from the start of their calculation. Inidicators with longer periods over 100 require less, relatively speaking, perhaps 2 times the period.

---
## Which Indicators?
The following lists of indicators are calculated using previous values and consequently have the potential to produce unstable values at the beginning of the series. 

**Standard Indicators**:  
AccumDist, ADX, ADXR, ATR, ATRP, ATRBandLower, ATRBandUpper, DI-, DI+, DSS, EMA, FAMA, HV, 
Kalman, KST, KVO, MACD, MAMA, OBV, PMO, PSAR, RMI, RSI, SMMA, StochRSI, UltOsc, Vidya, VPT, WilderMA

**TASC**:  
AEMA, APTR, BandPass, CyberCycle, DecyclerOscillator, ESDBandLower/Upper, EStdDev, ExpDev, 
ExpDevBandUpper/Lower, FAMA, FourierCTS, FourierSeries, FractalDim, MAMA, MESAStochastic, MHLMA, Midas, MidasLower/Upper, QuotientTransform, Reflex, ReverseEMA, RMO, RoofingFilter, RSMK, SimpleDecycler, SRSI, STMACD, SuperPassbandRMS, SVSI, Trendflex, VossPredictor, VFI, VMACDH, WeeklyMACD, WeeklyPPO...
 
**Advanced Smoothers**:  
AdaptiveLaguerre
 
**PowerPack**:  
MACZ, Parabolic2, SmoothedParabolic

## Programming Pattern Workaround
With C# strategies, the best way to work with these type of indicators (especially for Daily+ scales) is to use the programming pattern shown in the snippet below, which calculates the indicator values on all bars available and then synchronizes the result to the chart's date period. Assuming the same Historical Provider source data is used, the indicator values will not change for any given date, no matter the start of the backtest. 

```
// get all data available - the start data will always be the beginning of the available data
BarHistory allBars = GetHistoryUnsynched(bars.Symbol, bars.Scale, null);

// create the indicator as a TimeSeries type using "all data"
TimeSeries ema = EMA.Series(allBars.Close, 200);

// synchronize the result to the chart bars
ema = TimeSeriesSynchronizer.Synchronize(ema, bars);
PlotTimeSeries(ema, "EMA(200)", "Price", WLColor.Aqua);
```

**Disadvantages:**  
1. This method is recommended mainly for Daily+ strategies for which the number of "seed bars" could be limited. Accessing all available Intraday data requires more resources and long intial load times, which could slow down backtests.
2. Requires working with the indicator as a pure TimeSeries type instead of IndicatorBase. 
