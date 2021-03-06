# Keltner Channels

## Overview

Keltner Channels are volatility-based envelopes set above and below an exponential moving average (EMA).

This indicator is similar to [Bollinger Bands](Bollinger_Bands), which uses the standard deviation to set the bands. Instead of using the standard deviation, Keltner Channels use the [Average True Range (ATR)](Average\_True\_Range\_(ATR\)) to set the channel distance. The channels are typically set two Average True Range values above and below the 20-day [EMA](Exponential_Moving_Average_(EMA\)). The exponential moving average dictates  the direction, and the Average True Range sets the channel width. Keltner Channels are a trend following indicator used to identify reversals with channel breakouts and channel direction. Channels can also be used to identify overbought and oversold levels when the trend is flat.

Mathematical description of the indicator: [Keltner Channels Mathematical Description](Mathematical_Description#keltner_channels).

## Adding indicator

Keltner Channels indicator is added using {api:anychart.core.stock.Plot#keltnerChannels}keltnerChannels(){api} method. It requires a mapping with three fields: `"high"`, `"low"`, and `"close"`.

```
// create data table on loaded data
var dataTable = anychart.data.table();
dataTable.addData(get_csco_daily_data());

// map loaded data
var mapping = dataTable.mapAs({"open": 1, "high": 2, "low": 3, "close": 4});

// create stock chart
var chart = anychart.stock();

// create a plot on the chart
var plot = chart.plot();

// create ohlc series
var ohlcSeries = plot.ohlc(mapping);

// create a Keltner Channels indicator
var keltnerChannels = plot.keltnerChannels(mapping);
```

Here is a live sample:

{sample}STOCK\_Technical\_Indicators\_Keltner\_Channels\_1{sample}

## Indicator parameters

There are eight parameters a Keltner Channel indicator has, one of them is necessary - the mapping.

The "maPeriod" and "atrPeriod" parameters set the Moving Average period and Average True Range period. The "maType" parameter sets the smoothing type, the next parameter is the multiplier, and the three last parameters allow you to set the series type of Moving Average and the range series.

The following code sample demonstrates a Keltner Channels indicator with parameters set as default:

```
var keltnerChannels = plot.keltnerChannels(mapping, 20, 10, "ema", 2, "line", "range-area");
```

## Visualization

Vizualization of an indicator depends on the type of a series you display it with. Here is a sample where Keltner Channels indicators with different parameters and settings are added to different plots:

```
// create and adjust a Keltner Channels indicator
var keltnerChannels_0 = plot_0.keltnerChannels(mapping, 10, 15, "sma", 4);
keltnerChannels_0.maSeries().stroke("2 #ef6c00");
keltnerChannels_0.rangeSeries().fill("#ffd54f 0.2");
keltnerChannels_0.rangeSeries().highStroke("2 #00bfa5");
keltnerChannels_0.rangeSeries().lowStroke("2 #dd2c00");

// create and adjust a Keltner Channels indicator
var keltnerChannels_1 = plot_1.keltnerChannels(mapping, 10, 15, "sma", 4, "step-line", "step-range-area");
keltnerChannels_1.maSeries().stroke("2 #64b5f6");
keltnerChannels_1.rangeSeries().fill("none");
keltnerChannels_1.rangeSeries().lowStroke("2 #00bfa5");
keltnerChannels_1.rangeSeries().highStroke("2 #00bfa5");
```

Live sample:

{sample}STOCK\_Technical\_Indicators\_Keltner\_Channels\_2{sample}