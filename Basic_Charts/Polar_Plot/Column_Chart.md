{:index 2}
# Polar Column Chart

## Overview

This article explains how to create a Polar Column chart in AnyChart.

To learn more about polar charts in general and how to customize them, see [Polar Charts (Overview)](Overview). In addition, you can read the [Column Chart](../Column_Chart) article to learn about other available settings.

## Quick Start

To build a Polar Column chart, use the {api:anychart#polar}anychart.polar(){api} chart constructor. Then call the {api:anychart.charts.Cartesian#column}column(){api} method to create a Column series:

```
// create a chart
chart = anychart.polar();

// create a column series and set the data
var series = chart.column(data);
```

{sample}BCT\_Polar\_Column\_Chart{sample}

## Special Settings

### Point Size

This chart type allows you to set the size of its points. Read more in the [Point Size](../../Common_Settings/Point_Size) article.