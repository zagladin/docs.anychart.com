{:index 1}
#Box Chart

* [Overview](#overview)
* [Quick Start](#quick_start)
* [General Settings](#general_settings)
* [Special Settings](#special_settings)
  * [Appearance](#appearance)
   * [Median](#median)
   * [Outliers](#outliers)
   * [Stems](#stems)
   * [Whiskers](#whiskers)
  * [Labels](#labels)
  * [Tooltips](#tooltips)
  * [Vertical Box](#vertical_box)


## Overview

A Box Chart is a convenient way of graphically depicting groups of numerical data through their quartiles. Box Charts are useful when it is necessary to describe the values as they spread across the entire range. For example, to analyze salaries in a company, it is necessary to have more information than the sum of salaries for each salary grade. Even a measure of average salary wouldn't depict all. 
  
Box Charts allow showing the minimum and the maximum with a median (a numerical value separating the higher half of a data sample, a population, or a probability distribution, from the lower half) and quartiles, which helps to make the story more complete. But still, giving only the highest, the lowest and the medium values doesn't tell the full story. So it is often useful to display the data in a way that reveals more about values' distribution.

This article explains how to create a basic Box chart as well as configure settings that are specific to the type. You can also see the table below to get a brief overview of the Box Chart's characteristics:

<table border="1" class="seriesTABLE">
<tr><th colspan=2>API</th></tr>
<tr><td>Class</td><td>{api:anychart.core.cartesian.series.Box}anychart.core.cartesian.series.Box{api}</td></tr>
<tr><th colspan=2>DATA</th></tr>
<tr><td>Data Fields</td><td>[x, low, q1, median, q3, high, value, outliers](../Working_with_Data/Overview)</td></tr>
<tr><td>Multiple Series</td><td>[YES](../Working_with_Data/Overview)</td></tr>
<tr><th colspan=2>OPTIONS</th></tr>
<tr><td>Stacked</td><td>N/A</td></tr>
<tr><td>Vertical</td><td>[Vertical Box](Vertical/Box_Chart)</td></tr>
<tr><td>3D</td><td>N/A</td></tr>
<tr><td>Error Bars</td><td>[Error Chart](Error_Chart)</td></tr>
<tr><th colspan=2>SUPPORTED CHART PLOTS</th></tr>
<tr><td>Polar</td><td>N/A</td></tr>
<tr><td>Radar</td><td>N/A</td></tr>
<tr><td>Scatter</td><td>N/A</td></tr>
<tr><td>Stock</td><td>N/A</td></tr>
<tr><th colspan=2>RELATED TYPES</th></tr>
<tr><td></td><td>[Error Chart](Error_Chart)</td></tr>
<tr><td></td><td>[Pareto Chart](Pareto_Chart)</td></tr>
<tr><th colspan=2>SEE ALSO</th></tr>
<tr><td></td><td><a href="http://www.anychart.com/chartopedia/chart-types/box-chart/" target="_blank">Chartopedia: Box Chart</a></td></tr>
<tr><td></td><td>[General Settings](General_Settings)</td></tr>
</table>


## Quick Start

To create a Box chart, use the {api:anychart#box}anychart.box(){api} chart constructor. If you pass the data to this chart constructor, it will create a Box series.

To create a Box series explicitly, call the {api:anychart.charts.Cartesian#box}box(){api} method.

The following sample demonstrates how a basic Box chart is created:

```
// chart data
var data = [
  {x: "1", low: 1000, q1: 1050, median: 1200, q3: 1800, high: 2000, outliers: [800, 2500, 3200]},
  {x: "2", low: 2500, q1: 3000, median: 3800, q3: 3900, high: 4000},
  {x: "3", low: 2000, q1: 2300, median: 2500, q3: 2900, high: 3000},
  {x: "4", low: 4000, q1: 5000, median: 6500, q3: 6500, high: 7000, outliers: [8930]},
  {x: "5", low: 8000, q1: 8400, median: 8500, q3: 8800, high: 9000, outliers: [6950, 3000]}
];

// create box chart
chart = anychart.box();

// create box chart series with our data
series = chart.box(data);

// set chart title text settings
var title = chart.title("Basic Box Chart");
  
// set container id for the chart
chart.container("container");
  
// initiate chart drawing
chart.draw();
```

{sample}BCT\_Box\_Chart\_01{sample}

Note that not all boxes have outliers. Outliers are optional values, which belong to the category, but does not fit the range between the low and the high values.

## General Settings

In AnyChart there are many settings that are configured in the same way for all chart types, including the Area chart (for example, legend and interactivity settings).

Read the overview of general settings: [General Settings](General_Settings).


## Special Settings

### Appearance

Here is a full list of methods used to configure visual settings that are available for the Box series:

* {api:anychart.core.cartesian.series.Box#color}color(){api}, {api:anychart.core.cartesian.series.Box#fill}fill(){api}, {api:anychart.core.cartesian.series.Box#hatchFill}hatchFill(){api}, {api:anychart.core.cartesian.series.Box#stroke}stroke(){api} set the color, fill, hatch fill, and stroke
* {api:anychart.core.cartesian.series.Box#hoverFill}hoverFill(){api}, {api:anychart.core.cartesian.series.Box#hoverHatchFill}hoverHatchFill(){api}, {api:anychart.core.cartesian.series.Box#hoverStroke}hoverStroke(){api} configure the visual settings on hover
* {api:anychart.core.cartesian.series.Box#selectFill}selectFill(){api}, {api:anychart.core.cartesian.series.Box#selectHatchFill}selectHatchFill(){api}, {api:anychart.core.cartesian.series.Box#selectStroke}selectStroke(){api} configure the visual settings on select

You can learn more from the [Appearance Settings](../Appearance_Settings) article.

In the sample below, there are two Box series with some of the appearance settings configured:

```
// color settings
series1.fill("#00cc99", 0.4);
series1.hoverFill("#00cc99", 0.2);
series1.selectFill("#00cc99", 0.6);
series1.stroke("#00cc99", 1, "10 5", "round");
series1.hoverStroke("#00cc99", 2, "10 5", "round");
series1.selectStroke("#00cc99", 4, "10 5", "round");

series2.color("none");
series2.hatchFill("forwardDiagonal");
series2.hoverHatchFill("backwardDiagonal");
series2.selectHatchFill("diagonalCross");
series2.stroke("#000");
series2.hoverStroke("#000", 2);
series2.selectStroke("#000", 4);
```

{sample}BCT\_Box\_Chart\_02{sample}

#### Median

The special line across the box is a median. Median has its own appearance settings methods: {api:anychart.core.cartesian.series.Box#medianStroke}medianStroke(){api}, {api:anychart.core.cartesian.series.Box#hoverMedianStroke}hoverMedianStroke(){api} and {api:anychart.core.cartesian.series.Box#selectMedianStroke}selectMedianStroke(){api}. The following sample demonstrates these methods usage:

```
// adjust median settings for the second series
series.medianStroke("#000");
series.hoverMedianStroke("#000", 2);
series.selectMedianStroke("#000", 4);
```

{sample}BCT\_Box\_Chart\_03{sample}

#### Outliers

There are several methods for adjusting the settings of outliers: {api:anychart.core.cartesian.series.Box#outlierMarkers}outlierMarkers(){api}, {api:anychart.core.cartesian.series.Box#hoverOutlierMarkers}hoverOutlierMarkers(){api} (for configuring outliers settings on hover) and {api:anychart.core.cartesian.series.Box#selectOutlierMarkers}selectOutlierMarkers(){api} (for configuring outliers settings on select). Using those methods allows changing not only the colors but also the type and size of the outliers. Let's add these settings to the previous sample:

```
// outliers setting adjusting
series.outlierMarkers(
  {fill: "#DC143C 0.7",
  stroke: {color: "#DC143C", thickness: 0.5, dash: "5 1", lineJoin: "round"},
  size: 10,
  type: "star5"});
series.hoverOutlierMarkers(
  {fill: "#DC143C 0.5",
  stroke: {color: "#DC143C", thickness: 1, dash: "5 1", lineJoin: "round"},
  size: 10,
  type: "star5"});
series.selectOutlierMarkers(
  {fill: "#DC143C",
  stroke: {color: "#DC143C", thickness: 2, dash: "5 1", lineJoin: "round"},
  size: 10,
  type: "star5"});
```

Note that these settings are adjusted in JSON format. Read more about using JSON in the [Data from JSON article](../Working_with_Data/Data_From_JSON).

{sample}BCT\_Box\_Chart\_04{sample}


#### Stems

Stems are those vertical sticks going beyond the boxes, demonstrating the difference between low value and first quartile and between third quartile and high value. Stems stroking settings are to be adjusted with the following methods: {api:anychart.core.cartesian.series.Box.stemStroke}stemStroke(){api} for boxes in the normal state, {api:anychart.core.cartesian.series.Box.hoverStemStroke}hoverStemStroke(){api} for stem stroke in hovered state and {api:anychart.core.cartesian.series.Box.selectStemStroke}selectStemStroke(){api} for stems of a selected box. Stroke settings include the value (which is usually color but can also be a function, a string parameter or a stroke type - look through the API of these methods), thickness, dash pattern, line join style and line cap style. None of the parameters are necessary.

The sample below demonstrates those methods' usage.

```
// stem settings adjusted
series.stemStroke("#F44336", 1, "5 2");
series.hoverStemStroke("#F44336", 2, "5 2", "round", "round");
series.selectStemStroke("#F44336", 3, "5 2");
```
{sample}BCT\_Box\_Chart\_05{sample}


#### Whiskers

Whiskers are horizontal line segments on the stems' tops. They have "0" width by default, but this can be adjusted with the {api:anychart.core.cartesian.series.Box.whiskerWidth}whiskerWidth(){api} method. Set whiskers stroke with the {api:anychart.core.cartesian.series.Box.whiskerStroke}whiskerStroke(){api} method. For hovered state use {api:anychart.core.cartesian.series.Box.hoverWhiskerWidth}hoverWhiskerWidth(){api} and {api:anychart.core.cartesian.series.Box.hoverWhiskerStroke}hoverWhiskerStroke(){api}, for selected state use {api:anychart.core.cartesian.series.Box.selectWhiskerWidth}selectWhiskerWidth(){api} and {api:anychart.core.cartesian.series.Box.selectWhiskerStroke}selectWhiskerStroke(){api} respectively.

```
// set whiskers
series.whiskerWidth(30);
series.hoverWhiskerWidth(30);
series.selectWhiskerWidth(30);
series.whiskerStroke("#c2b65d", 0.7);
series.hoverWhiskerStroke("#c2b65d", 0.5);
series.selectWhiskerStroke("#c2b65d", 1);
```
{sample}BCT\_Box\_Chart\_06{sample}


### Labels

[Labels](../Common_Settings/Labels) are text or image elements that can be placed anywhere on any chart (you can enable them on a whole series or in a single point). For text labels, font settings and [text formatters](../Common_Settings/Text_Formatters) are available.

### Tooltips

A [Tooltip](../Common_Settings/Tooltip) is a text box displayed when a point on a chart is hovered. There is a number of visual and other settings available: for example, you can edit the text by using font settings and [text formatters](../Common_Settings/Text_Formatters), change the style of background, adjust the position of a tooltip, and so on.

### Vertical Box

Most types of series in AnyChart can be drawn both in horizontal and vertical orientation: [Vertical Charts](Vertical/Overview).

Here is the information about creating Vertical Box series: [Vertical Box](Vertical/Box_Chart).