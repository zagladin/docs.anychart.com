# Legend

* [Overview](#overview)
* [Auto Legend](#auto_legend)
* [Easy Auto Legend for Single Series Charts](#easy_auto_legend_for_single_series_charts)
* [Title](#title)
* [Positioning](#positioning)
* [Visualization](#visualization)
 * [Background](#background)
 * [Size](#size)
 * [Paging](#paging)
 * [Marker Symbol](#marker_symbol)
* [Series Management](#series_management)
* [Tooltip](#tooltip)
* [Custom Item](#custom_item)
* [Custom Legend](#custom_legend)

## Overview
Legend is a table on a chart listing and explaining the symbols and colors used and with additional information that helps user to understand a chart.
  
  
In this article all legends features and setting are explained and demonstrated.

## Auto Legend 

To enable legend you have to specify {api:anychart.core.ui.Legend#enabled}**.enable(true)**{api} parameter of {api:anychart.core.ui.Legend}**.legend()**{api} method:

```
  // create chart
  var chart = anychart.line();
  
  // enable legend
  chart.legend().enabled(true);
```

By default legend shows all series names with a symbol that shows the color and the type of the series.
  
  
To enable such legend in your chart just enable it:

```
  chart.legend().enabled(true);
```

In the live sample, please notice that when you move the mouse over the series name in legend - all series elements are highlighted

{sample}AS\_Legend\_01{sample}

## Easy Auto Legend for Single Series Charts

If you are showing a single series chart and want your legend to show all points names and values you should configure legend:

```
  chart.legend()
    .enabled(true)                  // enable legend
    .itemsSourceMode('categories'); // set source of legend items
```

To create a legend for single series chart you just have to set **categories** value for {api:anychart.core.ui.Legend#itemsSourceMode}**.itemsSourceMode()**{api}.

{sample}AS\_Legend\_02{sample}

## Title

Sometimes you need the title to a legend and sometimes it is superfluous: to enable legend title you have to set {api:anychart.core.ui.Title#enabled}**.enabled(true)**{api} parameter of a legend title method as it is shown below

```
  chart.legend().title().enabled(true);
```

To specify and format your own title for the legend use {api:anychart.core.ui.Title#text}**.text()**{api} method of a {api:anychart.core.ui.Legend#title}**.title()**{api}. For more information about title settings please refer to the [Title](../Appearance_Settings/Title) article.

```
  chart.legend().title()
    .useHtml(true)
    .enabled(true)              // enables legend title
    .text('Total sales<br><i style="color: #999; font-weight: 400; font-size: 11px;">(Year 2004)</i>')
    .fontSize(14)               // set font size
    .hAlign('center');
```

Here is a sample bar chart and the legend has tuned title:

{sample}AS\_Legend\_03{sample}

## Positioning

Depending on the layout and type of your chart you can position legend to a desired place using {api:anychart.core.ui.Legend#position}**.position()**{api} method of {api:anychart.core.ui.Legend}**.legend()**{api}. 
  
  
As an addition to the {api:anychart.core.ui.Legend#position}**.position()**{api} method, method {api:anychart.core.ui.Legend#align}**.align()**{api} controls legend alignment.

{sample}AS\_Legend\_04{sample}

*Note:* possible values that can be passed to the {api:anychart.core.ui.Legend#align}**.align()**{api} method are: *Left, Right, Top, Bottom and Center*. Also, possible values depend on the {api:anychart.core.ui.Legend#position}**.position()**{api} parameter. With *Top* and *Bottom* legend position it is possible to use *Left, Right* and *Center* parameters of {api:anychart.core.ui.Legend#align}**.align()**{api}. For *Left* and *Right* values of {api:anychart.core.ui.Legend#position}**.position()**{api} it's possible to use *Top, Bottom* and *Center* parameters of {api:anychart.core.ui.Legend#align}**.align()**{api} method.

## Visualization

As far as a legend is a part of a chart, its appearance should be tuned properly. Main aspects of legend visual appearance are described in this section.

### Background

Legend background allows you to configure the border and the inner color of the legend. Method {api:anychart.core.ui.Legend#background}**.background()**{api} controls background visual appearance. To learn more about background setting please study the [background tutorial](Background).

{sample}AS\_Legend\_05{sample}

### Size

Legend size is controlled by {api:anychart.core.ui.Legend#height}**.height()**{api} and {api:anychart.core.ui.Legend#width}**.width()**{api} parameters. 
  
  
Sample Pie Chart with a legend of a fixed (75px - width, 140px height) size positioned to the *"Left"* of the chart, aligned to *"Top"*, with padding of 10 pixels:

```
  chart.legend()
    .height(140)  // set legend height to 140px 
    .width(95)    // set legend width to 95px
```

Here is a sample with adjusted legend size

{sample}AS\_Legend\_06{sample}

*Note:* the space between data plot and legend is controlled using {api:anychart.core.ui.Legend#padding}**padding()**{api} method.


### Paging

If legend items can't be displayed on a plot of a legend, **{api:anychart.core.ui.Legend#paginator}paginator(){api}** method controls legend page. Paginator can be placed anywhere inside the legend.

```
  // legend settings
  chart.legend().enabled(true)
    .paginator()
      .layout('vertical')       // set paginator layout
      .orientation('right')     // place paginator on the right
```

{sample}AS\_Legend\_07{sample}

### Marker Symbol

When you are working with line and spline chart you may use markers to distinguish different series. By default AnyChart shows marker symbols in legend - only color representation is used in a small line icon. If you want to tune markers in legend icons you have to adjust {api:anychart.core.ui.LegendItem}**legendItem()**{api} method. Sample code presented below.

```
  // chart data 
  chart.line([
    {x: "John", value: 16000},
    {x: "Jake", value: 21000},
    {x: "Peter", value: 22000}
  ])
    .legendItem()               // settings for legend item of the series
      .iconMarkerFill('gold')   // set inner color of icon marker
      .iconMarkerStroke('red')  // set border of icon marker
      .iconMarkerType('star6'); // set type of icon marker
```

Here is a sample with different settings for a marker of legend item.

{sample}AS\_Legend\_08{sample}

### Tooltip

If you want to configure legend tooltips - you should do that using {api:anychart.core.ui.Legend#tooltip}**.tooltip()**{api} methods. You can tune its visual appearance and format. In the following sample we will format tooltips of the legend to show detailed description information.

{sample}AS\_Legend\_09{sample}

## Series Management

You can easily control series of the chart using chart legend. You can hide and show any of the series by clicking on the legend items. Here is a sample of column chart with four series. One of the series is already disabled. Click on the last legend item to show hidden series. 

{sample}AS\_Legend\_10{sample}

## Custom Item

When creating legend you can add your own items with any information you want to see on the legend, to do that use {api:anychart.ui.Legend#itemsFormatter}**itemsFormatter()**{api} method. 

```

chart.legend()
    .itemsFormatter(function(items){        // adjust legend items
      items.push({                          // push into items array
        text: 'item text '                  // set text of a new item
      });
      return items;                         // return items array
    });

```

In the sample chart below we've used custom item that adds *Total* data to legend.

{sample}AS\_Legend\_11{sample}

## Custom Legend

AnyChart sets no limits to the amount of legends on one chart plot. Legend can be a part chart as well as a separate unit. Sample below demonstrates three custom legend at the bottom of the chart. 

{sample}AS\_Legend\_12{sample}