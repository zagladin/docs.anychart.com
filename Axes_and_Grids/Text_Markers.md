{:index 9}
# Text Markers

              
* [Overview](#overview)
* [Declare](#declare)
* [Settings](#settings)

## Overview

Text Markers are useful when you want to place custom texts or description with or instead of axes values labels. You can add text markers to any place of a chart.

## Declare

These text markers are just custom text placed on chart.

To add custom text you need to create **.textMarker()** and set **.value()**, **.scale()** and **.text()**.You may 
use other options, but previous three are mandatory.

```
    chart.textMarker()
        .scale(chart.xScale)
        .value(16)
        .text('Custom Marker');
```

Sample below shows several variants of Text Marker usage: marking up values (High, Low), describing values (Historical Maximum) and marking only selected values on certain axis (8.00).

{sample}AGST\_Text\_Marker\_01{sample}

## Settings

You can configure text marker placement, font, anchor and text of any custom text using **.value()**, **.align()**, **.anchor()**, **.fontSize()**, **.offsetX()**, **.offsetY()**, **.text()** methods.

Markers placement is controlled using **.align()** method, possible values are: "Near", "Center", "Far".

```
    chart.textMarker(2)
        .scale(chart.yScale())
        .value(9000)
        .text('Far')
        .align('far')
        .anchor('rightcenter')
        .fontSize(13)
        .offsetX(10)
        .fontColor('green');
```

In the sample below you can see different text markers positions and text formatting:

{sample}AGST\_Text\_Marker\_02{sample}