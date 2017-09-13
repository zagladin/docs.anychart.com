{:index 10}
# Radar Stacked Area Chart

* [Overview](#overview)
* [Quick Start](#quick_start)
* [Adjusting](#adjusting)

## Overview

A Radar Stacked Area Chart is a multi-series Radar Area Chart that displays the trend of the value each series contributes over time or categories.

The concept of stacking in AnyChart is described in this article: [Stacked (Overview)](../Overview).

## Quick Start

To build a Radar Stacked Area Chart, create a multi-series [Radar Area Chart](../../Radar_Plot/Area_Chart) and set the {api:anychart.scales.Linear#stackMode}stackMode(){api} method into <strong>value</strong>:

```
// create a chart
var chart = chart.radar();

// enable the value stacking mode
chart.yScale().stackMode("value");

// create area series
var series1 = chart.area(seriesData_1);
var series2 = chart.area(seriesData_2);
```

{sample}BCT\_Radar\_Stacked\_Area\_Chart{sample}

## Adjusting

The Radar Stacked Area series' settings are mostly the same as other series' ones. The majority of information about adjusting series in AnyChart is given in the [General Settings article](../../General_Settings).