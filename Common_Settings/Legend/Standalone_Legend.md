{:index 12}
# Standalone Legend

## Overview

The standalone legend is one of [Standalones](../../Dashboards/Standalones) – building blocks, independent from the chart, that allow creating advanced data visualizations. For example, you can bind one legend to [multiple charts](#multiple_charts) or add [multiple legends](#multiple_legends) to a chart. See the sections below to learn more.

## Basics

### Legend

The standalone legend is defined as an instance of the {api:anychart.standalones.Legend}anychart.standalones.Legend{api} class.

To add a standalone legend to the chart, use the {api:anychart.standalones#legend}anychart.standalones.legend(){api} constructor:

```
// create a standalone legend
var legend = anychart.standalones.legend();
```

After the legend is adjusted and items are added, it should be drawn:

```
// set the container for the legend
legend.container(stage);

// draw the legend
legend.draw();
```

To adjust a standalone legend, use methods of the {api:anychart.standalones.Legend}anychart.standalones.Legend{api} class. The available settings generally correspond to the settings of the default legend and its elements, which can be found in [Basic Settings](Basic_Settings) and other articles in the [Legend](Overview) folder.

### Legend Items

**You can add items automatically** by using the {api:anychart.standalones.Legend#itemsSource}itemsSource(){api} method and specifying a chart or an array of charts you want the legend to be bound to. This method creates items representing the series or points of the given charts, like in the following sample: [Item = Series / Point](#item_=_series_/_point).

```
// set the source of legend items
legend.itemsSource([chart1, chart2]);
```

**Also, you can add items manually**. Call the {api:anychart.standalones.Legend#items}items(){api} method with an array of items as a parameter, or {api:anychart.standalones.Legend#itemsFormatter}itemsFormatter(){api} with a function returning an array of items. See samples in the [Item = Multiple Series](#item_=_multiple_series) and [Multiple Legends](#multiple_legends) sections.

```
// add items to the legend
legend.items([item1, item2, item3]);
```

**To adjust legend items**, use methods of the {api:anychart.standalones.Legend}anychart.standalones.Legend{api} class that affect items. The items of the default legend have similar settings, which are listed in [Legend Items](Legend_Items).

The settings available for individual items are described in the [Individual Legend Items](Individual_Legend_Items) article. You should keep in mind that the way of adjusting an individual item depends on the way how items are added:

**1.** If legend items are added automatically and the chart type allows adding multiple series, you can adjust an individual legend item by calling the {api:?entry=legendItem}legendItem(){api} method of the series represented by this item. Combine it with the methods of the {api:anychart.core.utils.LegendItemSettings}anychart.core.utils.LegendItemSettings{api} class. 

**2.** If the legend is automatic, but the chart is single-series, for example Pie, individual items are customized by adding special fields to the data. Learn more: [Individual Items: Single Series](Individual_Legend_Items#single_series).

**3.** In case items are added manually, individual settings are specified right in the array of items that is passed to {api:anychart.standalones.Legend#items}items(){api} or {api:anychart.standalones.Legend#itemsFormatter}itemsFormatter(){api}. The available settings are listed in {api:anychart.core.ui.Legend.LegendItemProvider}anychart.core.ui.Legend.LegendItemProvider{api}.

### Interactivity

The [default interactivity settings](Basic_Settings#default_interactivity) apply to legend items that are added automatically: they are bound to points or series of the chart or charts. If items are added manually, you have to manually bind them to elements of the chart with the help of events.

For further information, take a look at samples in the [Item = Multiple Series](#item_=_multiple_series) and [Multiple Legends](#multiple_legends) sections and read the [Events](Events) article.

## Multiple Charts

### Item = Series / Point

In this sample, each legend item represents a point of the Pie chart, and the last item represents the only series of the Line chart:

{sample}CS\_Legend\_Standalone\_01{sample}

The legend is automatically bound to the charts by using the {api:anychart.standalones.Legend#itemsSource}itemsSource(){api} method:

```
// create a standalone legend
var legend = anychart.standalones.legend();

// set the source of legend items
legend.itemsSource([chart1, chart2]);

// set the container for the legend
legend.container(stage);

// draw the legend
legend.draw();
```

### Item = Multiple Series

In the sample below, there are two Spline charts with multiple series. Each item of the standalone legend represents two series: one on the first chart, and one on the second chart.

{sample}CS\_Legend\_Standalone\_02{sample}

The {api:anychart.standalones.Legend#items}items(){api} method is used to add items to the legend:

```
// create a standalone legend
var legend = anychart.standalones.legend();

// create an array for storing legend items
var legendItems = [];

// push legend items to the array
for (var i = 0; i < chart1.getSeriesCount(); i++) {
  var series = chart1.getSeriesAt(i);
  legendItems.push({
    text: series.name(),
    iconType: "spline",
    iconStroke: {color: series.color(), thickness: 3}
  });
}

// add items to the legend
legend.items(legendItems);

// set the container for the legend
legend.container(stage);

// draw the legend
legend.draw();
```

The legend is custom, so the [events of legend items](Events#legend_items) are used to bind items to series.

On the `legendItemClick` event, both series represented by the item are enabled or disabled, and the appearance to the item is adjusted:

```
/* listen to the legendItemClick event,
enable / disable the series on both charts,
and configure the appearance of the legend item */
legend.listen("legendItemClick", function(e) {
  var index = e.itemIndex;
  var series1 = chart1.getSeriesAt(index);
  var series2 = chart2.getSeriesAt(index);
  if (series1.enabled()) {
    series1.enabled(false);
    series2.enabled(false);
    legendItems[index].iconStroke = "3 #999999";
    legendItems[index].fontColor = "#999999";
    legend.itemsFormatter(function() {return legendItems});
  } else {
    series1.enabled(true);
    series2.enabled(true);
    legendItems[index].iconStroke = {
      color: series1.color(),
      thickness: 3
    };
    legendItems[index].fontColor = series1.color();
    legend.itemsFormatter(function() {return legendItems});
  }
});
```

On `legendItemMouseOver` and `legendItemMouseOut`, the color of the series is configured:

```
/* listen to the legendItemMouseOver event
and configure the appearance of the series on both charts */
legend.listen("legendItemMouseOver", function(e) {
  var series1 = chart1.getSeriesAt(e.itemIndex);
  var series2 = chart2.getSeriesAt(e.itemIndex);
  series1.stroke(anychart.color.lighten(series1.color()), 5);
  series2.stroke(anychart.color.lighten(series2.color()), 5);
});

/* listen to the legendItemMouseOver event
and reset the appearance of the series on both charts */
legend.listen("legendItemMouseOut", function(e) {
  var series1 = chart1.getSeriesAt(e.itemIndex);
  var series2 = chart2.getSeriesAt(e.itemIndex);
  series1.stroke(series1.color(), 1.5);
  series2.stroke(series2.color(), 1.5);
});
```

## Multiple Legends

The following sample shows how to add multiple legends to a single chart. Each legend represents a data row, and each legend item stands for a point on the chart:

{sample}CS\_Legend\_Standalone\_03{sample}

The {api:anychart.standalones.Legend#items}items(){api} method is used to add items to the legends:

```
// a function for creating legends
function createLegend(dataRow, alignment) {

  // create a standalone legend
  var legend = anychart.standalones.legend();

  // create an array for storing legend items
  var legendItems = [];

  // get the palette of the chart
  var palette = chart.palette().items();
  
  // push legend items to the array
  for (var i = 1; i < data.data()[dataRow].length; i++) {
    legendItems.push({
      text: "$" + data.data()[dataRow][i],
      iconFill: palette[i-1],
    });
  }

  // add items to the legend
  legend.items(legendItems);

  // set the position of the legend
  legend.position("right");

  // set the alignment of the legend
  legend.align(alignment);

  // set the legend title
  legend.title(data.data()[dataRow][0]);

  return legend;
}

// create the first standalone legend
var legend1 = createLegend(0, "top");

// create the second standalone legend
var legend2 = createLegend(1, "center");

// create the third standalone legend
var legend3 = createLegend(2, "bottom");
```

Since the legends are custom, the [events of legend items](Events#legend_items) are used to bind items to chart points.

When the `legendItemClick` event fires, the point is selected or deselected, and the appearance of the legend item is adjusted:

```
/* listen to the legendItemClick event,
select / deselect the point,
and configure the appearance of the legend item */
legend.listen("legendItemClick", function(e) {
  var index = e.itemIndex;
  var chartPoint = chart.getSeriesAt(index).getPoint(dataRow);
  if (!chartPoint.selected()) {
    chartPoint.selected(true);
    legendItems[index].iconFill = "#455a64";
    legend.itemsFormatter(function() {return legendItems});
  } else {
    chartPoint.selected(false);
    legendItems[index].iconFill = palette[index];
    legend.itemsFormatter(function() {return legendItems});
  }
});
```

On `legendItemMouseOver` and `legendItemMouseOut`, the hover state of the point is enabled and disabled:

```
/* listen to the legendItemMouseOver event
and enable the hover state of the chart point */
legend.listen("legendItemMouseOver", function(e) {
  var index = e.itemIndex;
  var point = chart.getSeriesAt(index).getPoint(dataRow);
  point.hovered(true);
  /* if the chart point is selected,
  prevent the default behavior of the legend */
  if (point.selected()) {e.preventDefault();}
});

/* listen to the legendItemMouseOut event
and disable the hover state of the chart point */
legend.listen("legendItemMouseOut", function(e) {
  var index = e.itemIndex;
  var point = chart.getSeriesAt(index).getPoint(dataRow);
  point.hovered(false);
});
```