#Text Formatters

* [Overview](#overview)
* [Default fields](#default_fields)
* [Extra fields](#extra_fields)
 * [getDataValue](#getdatavalue)
 * [getSeriesMeta](#getseriesmeta)
 * [getStat](#getstat)


## Overview

Sometimes it might be necessary to display any text with the points on a chart for some reasons. That's when you need to use the {api:anychart.core.ui.LabelsFactory#textFormatter}**.textFormatter**{api} method.

##Default fields

There are some standard fields this method has, which depend on the chart type. Below you can see a table with all chart types and fields avaliable for them by default.


<table class="dtTABLE">
<tr>
<th>Chart type(s)</th><th>Default fields of {api:anychart.core.ui.LabelsFactory#textFormatter}**series.labels().textFormatter()**{api}</th>
</tr>
<tr>
<td>Area<br>Bar<br>Column<br>Error<br>Marker<br>Percent Stacked Area<br>Percent Spline Area<br>Percent StepLine Area<br>Percent Stacked Bar<br>Percent Stacked Column<br>Polar<br>Radar<br>Sparkline<br>Stacked Line<br>Stacked Spline</td>
<td>x<br>value<br>seriesName<br>index</td>
</tr>
<tr>
<td>Range Line<br>Range Spline Area<br>Range Column<br>Range Bar</td>
<td>x<br>seriesName<br>index<br>high<br>low</td>
</tr>
<tr>
<td>
Scatter
</td>
<td>
x<br>seriesName<br>index<br>value<br>valueLowerError<br>valueUpperError<br>xLowerError<br>xUpperError
</td>
</tr>
<tr>
<td>Bubble</td>
<td>x<br>value<br>seriesName<br>size</td>
</tr>
<tr>
<td>Box</td>
<td>x<br>seriesName<br>index<br>lowest<br>q1<br>median<br>q3<br>highest<br>outliers</td>
</tr>
<tr>
<td>Japanese Candlestick<br>Open-High-Low-Close</td>
<td>x<br>open<br>high<br>low<br>close<br>seriesName<br>index</td>
</tr>
<tr>
<td>Pie/Donut<br><!--Funnel--!>
</td>
<td>**Note!** As those types have an only series by default,<br> you should use the {api:anychart.core.ui.LabelsFactory#textFormatter}**.textFormatter()**{api} method with chart.label().<br>x<br>value<br>seriesName<br>index</td>
</tr>
</table>


Let's look at those examples to understand how it works.


```
    //set data series
    var series_1, series_2;
    series_1 = chart.bar(Sales2003);
    series_2 = chart.bar(Sales2004);
    
    //set series name
    series_1.name('Winter');
    series_2.name('Summer');
    
    //set textFormatter
    series_1.labels().enabled(true);
    series_1.labels().textFormatter(function(){
        return(this.seriesName);
    });
    series_2.labels().enabled(true);
    series_2.labels().textFormatter(function(){
        return(this.seriesName);
    });

```

{sample}CS\_TextFormatter\_01{sample}

First of all, you should enable the labels. Then set the fields of values you want those labels to show using the {api:anychart.core.ui.LabelsFactory#textFormatter}**.textFormatter()**{api} function according to the table above.

This function can return more than one value. The sample below demonstrates it.

```
    //set the textFormatter
    series_1.labels().textFormatter(function(){
        return('Size: '+this.size+', value: '+this.value);
    });
    series_2.labels().textFormatter(function(){
        return('Size: '+this.size+', value: '+this.value);
    });

```

{sample}CS\_TextFormatter\_02{sample}

##Extra fields

The number and variety of defalut fields might be not enough in some cases. Sometimes it's necessary to show some extra information. In this case you should use one of following methods: {api:anychart.core.utils.SeriesPointContextProvider#getStat}**.getStat()**{api}, {api:anychart.core.utils.SeriesPointContextProvider#getDataValue}**.getDataValue()**{api} or {api:anychart.core.utils.SeriesPointContextProvider#getSeriesMeta}**.getSeriesMeta()**{api}. Which one to use depends on the unique situation.

###getDataValue

Using these methods, you can display the values from the extra params, if you have added any to the series or to the data. Look at the sample and its code below:

```
  //create box chart series with our data
  var series_1 = chart.box(data_1);
  var series_2 = chart.box(data_2);
  
  //enable the labels
  series_2.labels().enabled(true);
  
  //usage of textFormatter
  series_2.labels().textFormatter(function(){
      return(this.getDataValue('extra_inf'));
  });

```

{sample}CS\_TextFormatter\_03{sample}

In this sample we have added some extra information to the data: we defined the "extra_inf" parameter of "60% redundant" value for the second point of the second series and displayed it, using {api:anychart.core.utils.SeriesPointContextProvider#getDataValue}**.getDataValue()**{api}. Another extra parameter, "extra_inf_long", was added to use it, for example, as an extra field in the tooltip, because it's too long to be shown on the chart. How to add the values from any extra parameters, see in the [Labels and Tooltips]() tutorial.

###getSeriesMeta

You can add extra parameters not only to the data points but to series too. Let's add an extra parameter as to the series of OHLC chart and show it with textFormatter.

To add any parameter to the meta of the series, you need to set the parameter name first and then its value, which can be of any type.

```

    // set first series data
    var series_1 = chart.ohlc([
        {x: Date.UTC(2007, 7, 28), open:511.53, high:514.98, low:505.79, close:506.40},
        {x: Date.UTC(2007, 7, 30), open:517.36, high:518.40, low:516.58, close:516.80},
        {x: Date.UTC(2007, 8, 1), open:513.10, high:516.50, low:511.47, close:515.25},
    ]).xPointPosition(0.5)
    .meta('company', 'ACME Corp.');
     
    // set second series data
    var series_2 = chart.ohlc([
        {x: Date.UTC(2007, 7, 28), open: 522.95, high: 523.10, low: 522.50, close: 522.52},
        {x: Date.UTC(2007, 7, 30), open: 524.49, high: 524.91, low: 524.38, close: 524.61},
        {x: Date.UTC(2007, 8, 1), open: 518.81, high: 520.03, low: 517.51, close: 519.73}
    ]).xPointPosition(0.5)
    .meta('company', 'Duff B. Corp.');

    //textFormatter
    series_1.labels().textFormatter(function(){
        return('C: '+this.getSeriesMeta('company')+'\nL: '+this.low+'\nH: '+this.high);
    });
    series_2.labels().textFormatter(function(){
        return('C: '+this.getSeriesMeta('company')+'\nL: '+this.low+'\nH: '+this.high);
    });

```

{sample}CS\_TextFormatter\_04{sample}

**Note!** There's no {api::anychart.core.utils.SeriesPointContextProvider#getSeriesMeta}**.getSeriesMeta**{api} method in Pie Charts.

###getStat

This method is to be used when you need to display some statistic information. The variecy of fields for this method is not complied the same way as shown above. The avaliable fields for this method are given below.

<table class="dtTABLE">
<tr>
<th>Chart type(s)</th><th>Default fields of {api:anychart.core.ui.LabelsFactory#textFormatter}**series.labels().textFormatter()**{api}</th>
</tr>
<tr>
<td>Area<br>Bar<br>Box<br>Bubble<br>Column<br>Error<br>Marker<br>Percent Stacked Area<br>Percent Spline Area<br>Percent StepLine Area<br>Percent Stacked Bar<br>Percent Stacked Column<br>Polar<br>Radar<br>Range Line<br>Range Spline Area<br>Range Column<br>Range Bar<br>Scatter<br>Sparkline<br>Stacked Line<br>Stacked Spline</td>
<td>max - max value on a chart<br>
min - min value on a chart<br>
sum - sum of all values of a chart<br>
average - average value on a chart<br>
pointsCount - the number of all points on a chart<br>
seriesMax - max value of the series<br>
seriesMin - min value of the series<br>
seriesSum - sum of all values of the series<br>
seriesAverage - average value of the series<br>
seriesPointsCount - the number of all points on a chart</td>
</tr>
<tr>
<td>Japanese Candlestick<br>Open-High-Low-Close</td>
<td>pointsCount - the number of all points on a chart<br>seriesPointsCount - the number of all points on a chart</td>
</tr>
<tr>
<td>Pie/Donut<br><!--Funnel--!></td>
<td>count - number of points<br>
min - min value on a chart<br>
max - max value on a chart<br>
sum - sum of all values of a chart <br>
average - average value (sum / count)</td>
</tr>
</table>

Here is a sample of the {api:anychart.core.utils.SeriesPointContextProvider#getStat}**.getStat()**{api} method usage in the Pie chart. Note there's no need in enabling the labels for a Pie chart, because they are enabled by default.

```
    //textFormatter
    chart.labels().textFormatter(function(){
    return((this.getDataValue('value'))+' / '+this.getStat('sum'));
});

```

{sample}CS\_TextFormatter\_05{sample}