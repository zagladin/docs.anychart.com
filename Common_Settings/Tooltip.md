# Tooltip

## Overview

Tooltip is a text box that is hidden by default and can be displayed when a point on a chart is hovered over. Tooltip demonstrates the information that each point contains. It may also display some additional information if this is defined by the tooltip settings.

## Default Tooltip

By default, the tooltip is being shown when a point on a chart is hovered over. To disable them from showing at all, set `false` to the {api:anychart.core.ui.Tooltip#enabled}enabled(){api} method.

```
// enable tooltip for all series
chart.tooltip(true);

// disable tooltip
var tooltip = series.tooltip();
tooltip.enabled(false);
```

Hover over each of the series to see the difference.

{sample}CS\_Tooltip\_01{sample}

### Basic settings

**NOTE:** Tooltips inherit settings. When settings are defined for tooltips of a whole chart, the series' tooltips  inherit them and have the same settings. You can override settings for any series.

To change font color and font face use {api:anychart.core.ui.Tooltip#fontColor}fontColor(){api} and {api:anychart.core.ui.Tooltip#fontFamily}fontFamily(){api} methods.

For example, let's set "gold" color to all tooltips and then override it with "green" for one of the series. 

```
// settings
chart.tooltip().fontColor("gold");
series2.tooltip().fontColor("green");
```

You can see that three series have tooltips with text of gold color and only the one has its tooltips text colored green.

{sample}CS\_Tooltip\_02{sample}

You can also change tooltip {api:anychart.core.ui.Tooltip#background}background(){api}, {api:anychart.core.ui.Tooltip#padding}padding(){api}, {api:anychart.core.ui.Tooltip#title}title(){api} and {api:anychart.core.ui.Tooltip#separator}title separator(){api}.

Let's adjust some of these settings to see how it works.

```
// tooltip padding for all series on a chart
chart.tooltip().padding().left(20);

// background color
chart.tooltip().background().fill("#663399");
series2.tooltip().background().fill("green");
```

{sample}CS\_Tooltip\_03{sample}

Formatting title and separator is described the [title formatting section](#title_formatting). 

## Display Mode

There are three modes of a tooltip display:

### Single

Single tooltip is the default mode. In this mode tooltip displays information only for a single point that is hovered over.

```
// create column chart plot
var chart = anychart.column();

// get chart tooltip
var tooltip = chart.tooltip();

// set single mode for the tooltip
tooltip.displayMode("single");
```

Here is a sample of a chart with the tooltip in a **single** state:

{sample}CS\_Tooltip\_04{sample}

### Union

Union display mode helps to display information about all points with the same argument from all series in one tooltip. This display mode is very useful for comparing series data. Here is a sample of the union tooltip:

```
// get chart's tooltip
var tooltip = chart.tooltip();

// set display mode for the tooltip
tooltip.displayMode("union");
```

{sample}CS\_Tooltip\_05{sample}

Note that if your tooltip is in union mode, setting background color for series separately has no sense as this setting is taken from chart tooltip settings

### Separated

Separated display mode shows a single tooltip for all series of the chart at the same time. Set "separated" value as a parameter of {api:anychart.core.ui.Tooltip#displayMode}displayMode(){api} method:

```
var tooltip = chart.tooltip();
tooltip.displayMode("separated");
```

{sample}CS\_Tooltip\_06{sample}

**Note**: It might be necessary to manage tooltips position for each series to prevent overlapping. Information on tooltips position can be found in this article in the [position section](#position). 

## Formatting 

### Title Formatting

You can manage tooltip title visual appearance using {api:anychart.core.ui.Tooltip#title}title(){api} method. You can adjust font's visual settings along with the title's background appearance.

```
var title = chart.tooltip().title();
title.fontFamily("Calibri");
title.fontDecoration("underline");
title.fontWeight(400);
```

Note that all title settings defined for a chart are inherited with the series tooltips. Here is a sample with title adjusted for all tooltips on a chart:

{sample}CS\_Tooltip\_07{sample}

### Separator

Separator is a space between tooltip title and content. Use {api:anychart.core.ui.Tooltip#separator}separator(){api} method to adjust this space.

```
// get tooltip
var tooltip = chart.tooltip();

// disable separator
tooltip.separator(false);
```

Here is a sample with a title separator disabled.

{sample}CS\_Tooltip\_09{sample}

### Text Formatting

You can adjust tooltip content in any way you want. All you have to do is to define custom settings for the {api:anychart.core.Chart#tooltip}tooltip(){api} method.

```
var tooltip = chart.tooltip();
tooltip.fontSize(13);
tooltip.fontFamily("Calibri");
tooltip.fontStyle("italic");
```

Here is a sample with the settings from above.

{sample}CS\_Tooltip\_10{sample}

The default content of a tooltip may vary for different chart types and series, but mainly it displays main points' properties: **x** and **value**. Check out the {api:anychart.core.ui.Tooltip#format}format(){api} method which is described in [Advanced Content Formatting](#advanced_content_formatting) section to find information about changing tooltip content.

### Advanced Content Formatting

There are two parts of a tooltip that can hold some information: its title and its body text. This section describes formatting both parts for making your tooltips more customized and informative in a way you need.

For adjusting text of the tooltip title use the {api:anychart.core.ui.Tooltip#titleFormat}titleFormat(){api} method. This method uses function or string with tokens as a parameter and can help you to format title in any desirable way.

```
tooltip1.titleFormat("Manager: {%x}");
```

{sample}CS\_Tooltip\_14{sample}

In case you need more complex content formatting there is the {api:anychart.core.ui.Tooltip#format}format(){api} method that uses a function or a string token as a parameter. More information on adjusting text can be found in the [Text Formatters article](../Common_Settings/Text_Formatters).

```
var tooltip = chart.tooltip();
tooltip.format(function() {
  /* code of your function */
});
```

There are several possible ways of formatting the tooltip text: tokens, external functions and functions set as a parameter. It's better to use one of them if possible. Using tokens suit situations when you plan to serialize/deserialize your charts to/from xml or json, external functions are good when you need to do the same complex calculations in several series' (of charts' - in case you work with a dashboard) tooltips and setting function as a parameter is the best option if you need to use unique formatter just once. Remember that series tooltips inherit their settings from chart tooltips, so you need to format the text once for the chart to make all tooltips of this chart look the same.

The following sample demonstrates using tokens for formatting tooltips:

```
// enable HTML for tooltips
chart.tooltip().useHtml(true);

// tooltip settings
var tooltip = chart.tooltip();
tooltip.positionMode("point");
tooltip.format("Manager: <b>{%x}</b>\nSales volume: <b>${%value}</b>");
```

{sample}CS\_Tooltip\_15{sample}

Use several formatting ways if there are some series on your chart or charts on a dashboard which tooltips need different formatting:

```
// set the tooltip title and text for the Column Chart
columnChart.tooltip().titleFormat("{%seriesName}");
columnChart.tooltip().format("Department: {%x} \nSum: {%value}");

// set the tooltip content
seriesSpline.tooltip().format(function(e){
  var value = (this.value)/1000000;
  return "Total: $" + value + "M";
});
```

{sample}CS\_Tooltip\_16{sample}

**Note**: You can find information on custom tooltips and an example of using a chart as a tooltip in the [Interactivity article](../Common_Settings/Interactivity#creating_custom_tooltip)

#### Prefix and Postfix

Use {api:anychart.core.ui.Tooltip#valuePrefix}valuePrefix(){api} and {api:anychart.core.ui.Tooltip#valuePostfix}valuePostfix(){api} methods to add symbols, whole words or anything before/after tooltip content. These methods can be used to set dollar symbol as prefix ($) or degrees fahrenheit as postfix (&deg;F).

{sample}CS\_Tooltip\_11{sample}

## HTML

To enable a fully functional HTML tooltip, call the {api:anychart.core.ui.Tooltip#useHtml}useHtml(){api} method with `true` as a parameter:

```
chart.tooltip().useHtml(true);
```

This feature allows you to usa any possible HTML settings: you can adjust background color, font style and size, the separator, and so on - use [inline styles](#inline_styles) or [CSS classes](#css_classes). Tooltips are rendered as separate HTML elements added to DOM. 

**NOTE:** AnyChart font and color settings methods for the default tooltip do not affect the HTML tooltip.

### Inline Styles

The following sample shows how to add an image and font settings to the HTML tooltip using inline styles:

```
// configure tooltips
chart.tooltip().useHtml(true);  
chart.tooltip().titleFormat("<img width='20' src='http://cdn.anychart.com/images/anychart-logo-medium.png'> <span style='font-size:28px;font-family:courier'>{%x}");  
chart.tooltip().format("<span style='font-family:courier'>{%value}</span>");
```

{sample}CS\_Tooltip\_22{sample}

### CSS Classes

You can change the CSS style of the tooltip by overwriting the default CSS classes used in AnyChart: just add new classes with the same names to your web page.

This is how the default div structure of the HTML tooltip looks like: 

```
<div class="anychart-tooltip">
  <div class="anychart-tooltip-title"></div>
  <hr noshade="true" class="anychart-tooltip-separator">
  <div></div>
</div>
```

And here are the default settings:

```
.anychart-tooltip {
  border-radius: 3px;
  padding: 5px 10px;
  background: rgba(33, 33, 33, 0.7);
  border: none;
  display: inline-block;
  box-sizing: border-box;
  letter-spacing: normal;
  color: #fff;
  font-family: Verdana, Helvetica, Arial, 'sans-serif';
  font-size: 12px;
  position: absolute;
  pointer-events: none;
  white-space: nowrap;
  margin: 10px;
}

.anychart-tooltip-separator {
  color: rgba(206, 206, 206, 0.3);
  border: none;
  height: 1px;
  margin: 5px 0;
}

.anychart-tooltip-title{
  font-size: 14px;
}
```

The sample below shows how to change the default settings:

```
.anychart-tooltip {
    border-radius: 23px;
    background: rgba(255, 160, 0, 0.7);
    font-family: Courier, Helvetica, Arial, 'sans-serif';
}

.anychart-tooltip-separator {
    height: 3px;
    background-color: rgba(221, 44, 0, 0.7);
}

.anychart-tooltip-title{
    font-size: 28px;
}
```

{sample}CS\_Tooltip\_23{sample}

### Events

The HTML tooltip has its own events and special methods allowing you to listen to them. These methods can be combined with other [event listeners](Event_Listeners).

Here is the full list of methods:

<table>
<tbody>
<tr>
<th>Method</th>
<th>Description</th>
</tr>
<tr>
<td>{api:anychart.core.ui.Tooltip#onDomReady}onDomReady(){api}</td>
<td>All HTML elements of the tooltip are added to the DOM. Triggered once for every tooltip (in case of separated mode or different tooltips for different series).
</td>
</tr>
<tr>
<td>{api:anychart.core.ui.Tooltip#onBeforeTitleChange}onBeforeTitleChange(){api}</td>
<td> The tooltip title is going to change. Returns `true` or `false`.

If the listener function returns `false`, the rules defined by [formatting methods](#formatting) are not applied to the title, and the {api:anychart.core.ui.Tooltip#onTitleChanged}onTitleChanged(){api} is not triggered.
</td>
</tr>
<tr>
<td>{api:anychart.core.ui.Tooltip#onContentChanged}onContentChanged(){api}</td>
<td>The tooltip content changed.</td>
</tr>
<tr>
<td>{api:anychart.core.ui.Tooltip#onBeforeContentChange}onBeforeContentChange(){api}</td>
<td> The tooltip content is going to change. Returns `true` or `false`.

If the listener function returns `false`, the rules defined by [formatting methods](#formatting) are not applied to the content, and the {api:anychart.core.ui.Tooltip#onContentChanged}onContentChanged(){api} is not triggered.</td>
</tr>
<tr>
<td>{api:anychart.core.ui.Tooltip#onTitleChanged}onTitleChanged(){api}</td>
<td>The tooltip title changed.</td>
</tr>
</tbody>
</table>

In the context, all methods get links to the four HTML elements of the tooltip (see the [CSS Classes](#css_classes) section). For example, this is how the context of {api:anychart.core.ui.Tooltip#onDomReady}onDomReady(){api} looks like:

```
// listen to the onDomReady event
chart.tooltip().onDomReady(function() {
  tooltipParentDiv = this.parentElement;
  tooltipTitleContentDiv = this.titleElement;
  tooltipSeparator = this.separatorElement;
  tooltipContentDiv = this.contentElement;
});
```

In the sample below HTML tooltip listeners and point event listeners are used to draw a chart in the tooltip:

{sample}CS\_Tooltip\_24{sample}

## Size

Width and height can be also set for all tooltips at once or for the determined series. Use {api:anychart.core.ui.Tooltip#width}width(){api} and {api:anychart.core.ui.Tooltip#height}height(){api} to set the corresponding parameters. Don't forget to format the text of the tooltip properly to avoid text overflowing or to set the width corresponding to the maximum text length.

```
// set tooltip size
columnChart.tooltip().width(200);
columnChart.tooltip().height(80);
```

{sample}CS\_Tooltip\_17{sample}

## Background

Tooltip background appearance can be controlled using {api:anychart.core.ui.Tooltip#background}background(){api} method. More information about adjusting background can be found in [Background tutorial](../Appearance_Settings/Background).

```
var background = chart.tooltip().background();
background.fill("#EEE 0.8");
background.stroke("#888");
background.cornerType("roundInner");
background.corners(5);
```

This is how tooltip background with the settings from above looks like:

{sample}CS\_Tooltip\_12{sample}

## Out of chart

In case when a tooltip is too big it may become a problem to demonstrate it within the chart bounds, you can allow the tooltip to be shown out of a chart. Set `true` to {api:anychart.core.ui.Tooltip#allowLeaveChart}allowLeaveChart(){api} to allow tooltips to leave the chart bounds. This method can be applied for the chart so it will affect all series simultaneously, or to series separately:

```
// applies to all series
chart.tooltip().allowLeaveChart(true);

// series settings override chart settings

// allow tooltips to leave the chart bounds
series1.tooltip().allowLeaveChart(true);

// forbid tooltips to leave the chart bounds
series2.tooltip().allowLeaveChart(false);
```

{sample}CS\_Tooltip\_13{sample}

Note that series' individual tooltip settings override the chart's tooltip settings, so the chart's tooltips settings are inherited by the third series with no settings adjusted.

Also note that this method allows or forbids the tooltips to overflow not only the chart, but the element they belong to. For example, if a tooltip of a great size belongs to a [Legend](Legend) or a [Data Grid](../Gantt_Chart/DataGrid), setting `true` to the {api:anychart.core.ui.Tooltip#allowLeaveChart}allowLeaveChart(){api} method will lead to this tooltip allowing to overflow that element.

## Out of stage

A chart may not be the same size as its [stage](../Graphics/Basics). Stage can be smaller or greater, so if it is necessary to allow or forbid the tooltip to be shown outside of the stage, use the {api:anychart.core.ui.Tooltip#allowLeaveStage}allowLeaveStage(){api} method. This method can also be applied for the chart so it will affect all series simultaneously, or to series separately:

```
// applies to all series
chart.tooltip().allowLeaveStage(false);

// series settings override chart settings

// adjust series tooltips
series1.tooltip().allowLeaveStage(true);
series2.tooltip().allowLeaveStage(false);
```

{sample}CS\_Tooltip\_13\_1{sample}

Note: that stage the chart belongs to is considered as the stage of the tooltip of this chart.

### Tooltip global container

*IMPORTANT NOTE:*

When any of the {api:anychart.core.ui.Tooltip#allowLeaveChart}allowLeaveChart(){api} and {api:anychart.core.ui.Tooltip#allowLeaveStage}allowLeaveStage(){api} get `true` as a parameter, the tooltip becomes the child element of the whole page. This may lead to a situation when the tooltip is left on the page after it has been reloaded. In this case, the only way to hide the tooltips  is to call the special {api:anychart.utils#hideTooltips}anychart.utils.hideTooltips(){api} method.

## Out of screen

If it is necessary to show the tooltip regardless of whether the tooltip is shown fully or not, use the {api:anychart.core.ui.Tooltip#allowLeaveScreen}allowLeaveScreen(){api} method. Setting `true` will make tooltips of the series or chart to follow the cursor and to go beyond the screen.

```
// adjust series tooltips
series1.tooltip().allowLeaveScreen(true);
series2.tooltip().allowLeaveScreen(false);
```

The third series inherits the chart's defaults in this sample.

{sample}CS\_Tooltip\_13\_2{sample}

## Position

There are several methods for managing tooltips position on the chart. This section contains information on most of these methods.
  
AnyChart html5 charting library allows to choose should the tooltip be bound to a cursor position, to the point that is hovered over or to the exact place on the chart plot. Use {api:anychart.core.ui.Tooltip#positionMode}positionMode(){api} method to choose a target for binding tooltip to. The `"float"` parameter is the default one for this method and makes tooltip to follow the cursor. Setting `"point"` and a parameter binds tooltip to the series point that is hovered over. Use the `"chart"` parameter for the {api:anychart.core.ui.Tooltip#positionMode}positionMode(){api} method to bind tooltips to a place on the chart plot.

```
chart.tooltip().positionMode("point");
```
Here is a sample with the tooltip stuck to the point that is hovered over:

{sample}CS\_Tooltip\_18{sample}

### Fixed Tooltip Position

You can bind tooltips to a certain point on the chart plot using `"chart"` as a value for {api:anychart.core.ui.Tooltip#positionMode}positionMode(){api}. The sample of such settings can be found below. You have to manage other tooltip parameters along with {api:anychart.core.ui.Tooltip#positionMode}positionMode(){api}.

You can choose which part of the tooltip should be considered as anchor and used for position managing. {api:anychart.core.ui.Tooltip#anchor}anchor(){api} method defines the main part of the tooltip for further positioning.

```
// set tooltip anchor
chart.tooltip().anchor("bottomLeft");
```

Here is a sample of two series with fixed tooltip position. Tooltip settings are the same except for the the tooltip anchor.

{sample}CS\_Tooltip\_19{sample}

Along with the main point for tooltip you can set the point to which the tooltip should be bound. Use {api:anychart.core.ui.Tooltip#position}position(){api} method to set the point for tooltip to be bound to.

```
var tooltip1 = series1.tooltip();
tooltip1.position("leftCenter");
  
var tooltip2 = series2.tooltip();
tooltip2.position("rightCenter");
```

This is how the sample with the code from above looks like:

{sample}CS\_Tooltip\_20{sample}

**Note**: You can shift tooltips position using {api:anychart.core.ui.Tooltip#offsetX}offsetX(){api} and {api:anychart.core.ui.Tooltip#offsetY}offsetY(){api} methods.

## Hiding Time

In some cases you may need to display a tooltip for a couple of moments after a point is no longer hovered over (mouse has been moved out of the point). Use {api:anychart.core.ui.Tooltip#hideDelay}hideDelay(){api} method to set timer to display tooltip a bit longer.

```
// tooltip settings
var tooltip = series.tooltip();

// set delay time in milliseconds
tooltip.hideDelay(1000);
```

## Themes

Tooltips can be adjusted using [AnyChart Themes](../Appearance_Settings/Themes). Themes make it possible to set the same settings for several charts. Here is a sample of adjusting tooltips using themes:

```
var themeSettings = {
  "column":{
    "tooltip": {
    "positionMode": "point",
    "hideDelay": 3000,
    "offsetX": 0,
    "fontFamily": "Menlo",
    "fontSize": 11
    }
  }
};
```

Settings for the tooltip in the sample below are applied using themes. Click "launch in playground" to see how settings for tooltip can be applied using AnyChart themes.

{sample}CS\_Tooltip\_21{sample}