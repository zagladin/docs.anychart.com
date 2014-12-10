{:index 1}
Quick Start
===========
  
## 4 simple steps to start using GanttChart
###1. Include Gantt into your web page
Include the JavaScript file in the `<head>` section of your web page.  
You can use CDN as shown below or visit the [download page](./Downloading_AnyChart).

```
<head>
    <script src="//cdn.anychart.com/js/latest/anychart.min.js" type="text/javascript"></script> 
</head>
```

###2. Create a container for the chart
Add a block-based HTML element into your page, set the `id`, `width` and `height` attributes. AnyChart uses 100% of the container if other behaviour is not specified. 
Example:
```
<body>
    <div id="container" style="width: 500px; height: 400px;"></div>
</body>
```
###3. Prepare your Data

Comparing with AnyChart, AnyGantt provides much more ways of working with data (such as setting tree like hierarchy with parent/child division), thus it requires preparing data before usage.

```
var data = [
  {
    "id": "1",
    "name": "Phase 1 - Strategic Plan",
    "periods": [
      {"id": "1_1", "start": 1171468800000, "end": 1171987200000, "fill": "green"}]
  },
  {
    "id": "2",
    "name": "Self-Assessment",
    "periods": [
      {"id": "2_1", "start": 1173024000000, "end": 1173715200000, "fill": "yellow"}]
  },
  {
    "id": "3",
    "name": "Define business vision",
    "periods": [
      {"id": "3_1", "start": 1169740800000, "end": 1170172800000, "fill": "green"}]
  },
  {
    "id": "4",
    "name": "Identify available skills, information and support",
    "periods": [
      {"id": "4_1", "start": 1171814400000, "end": 1172419200000, "fill": "green"}]
  },
  {
    "id": "5",
    "name": "Decide whether to proceed",
    "periods": [
      {"id": "5_1", "start": 1171296000000, "end": 1171382400000, "fill": "green"}]
  },
  {
    "id": "6",
    "name": "Define the Opportunity",
    "periods": [
      {"id": "6_1", "start": 1173628800000, "end": 1174320000000, "fill": "green"}]
  }
];
```

###4. Create a chart
Add the JavaScript tag `<script>` with the following code anywhere in the  page. 
This code example uses JavaScript API to create a chart, but you also can use JSON or XML format. <!--See [Supported Data Formats](../Working_with_Data/Supported_Data_Formats) to learn more about supported formats.-->
Example:

```
<script>
anychart.onDocumentReady(function(){
  // data tree settings
  var treeData = anychart.data.tree(data, anychart.enums.TreeFillingMethod.AS_TABLE);
  var chart = anychart.ganttResource();                 // chart type
  chart.bounds(0, 0, '100%', '100%');                   // chart position
  chart.data(treeData);                                 // chart data
  chart.splitterPosition(170);                          // data tree width
  var dataGrid = chart.getDataGrid();                   // create data grid
  dataGrid.column(0).width(30).title().text('#');       //  settings for first column

  // settings for the second column
  dataGrid.column(1).width(140).textFormatter(function(item) {
    return item.get('name');
  }).title().text('Person');

  // set container and initiate drawing
  chart.container('container').draw();
});
</script>
```
  
## The result
###See the result
After all these steps you should have the following result. This example, like any other on our site, can be launched and explored using the samples playground.
{sample}Gantt\_Chart{sample}
###Full source code
You can copy this to a file on your computer and open it in your browser to display the pie chart shown above:  
```
<!doctype html>
<head>
    <script src="//cdn.anychart.com/js/latest/anychart.min.js" type="text/javascript"></script> 
    <script>
      anychart.onDocumentReady(function(){
        // data tree settings
        var treeData = anychart.data.tree(data, anychart.enums.TreeFillingMethod.AS_TABLE);
        var chart = anychart.ganttResource();                 // chart type
        chart.bounds(0, 0, '100%', '100%');                   // chart position
        chart.data(treeData);                                 // chart data
        chart.splitterPosition(170);                          // data tree width
        var dataGrid = chart.getDataGrid();                   // create data grid
        dataGrid.column(0).width(30).title().text('#');       //  settings for first column

        // settings for the second column
        dataGrid.column(1).width(140).textFormatter(function(item) {
          return item.get('name');
        }).title().text('Person');

        // set container and initiate drawing
        chart.container('container').draw();
      });

      // data
      var data = [
        {
          "id": "1",
          "name": "Phase 1 - Strategic Plan",
          "periods": [
            {"id": "1_1", "start": 1171468800000, "end": 1171987200000, "fill": "green"}]
        },
        {
          "id": "2",
          "name": "Self-Assessment",
          "periods": [
            {"id": "2_1", "start": 1173024000000, "end": 1173715200000, "fill": "yellow"}]
        },
        {
          "id": "3",
          "name": "Define business vision",
          "periods": [
            {"id": "3_1", "start": 1169740800000, "end": 1170172800000, "fill": "green"}]
        },
        {
          "id": "4",
          "name": "Identify available skills, information and support",
          "periods": [
            {"id": "4_1", "start": 1171814400000, "end": 1172419200000, "fill": "green"}]
        },
        {
          "id": "5",
          "name": "Decide whether to proceed",
          "periods": [
            {"id": "5_1", "start": 1171296000000, "end": 1171382400000, "fill": "green"}]
        },
        {
          "id": "6",
          "name": "Define the Opportunity",
          "periods": [
            {"id": "6_1", "start": 1173628800000, "end": 1174320000000, "fill": "green"}]
        }
      ];
    </script>
</head>
<body>
	<div id="container" style="width: 500px; height: 400px;"></div>
</body>
</html>
```