---
title: Graphs
description: Graphs are good for condensing data points into a Visualization.
---

**Graphs are great for condensing data points into a Visualization.**

![a graph with mixed line and scatter graphs](images/graphs-1.png)

![a stacked bar chart](images/graphs-2.png)

**Dune offers you to create the following graph types:**

* bar charts
* area charts
* scatter charts
* line charts

You can mix all of these graph types together in one Visualization.

***

## Configuring your Visualizations

All graph Visualizations share a common editing schema.

In essence, you can define your Visualization in detail here. The three different sections of this are explained below.

![](images/graphs-3.png)

### Chart options

This section allows you to define how to display your data.

![see explanations below](images/graphs-4.png)

**Title**

* The title will appear in all instances of this graph prominently at the top.
* The graph will always keep the name of the Query, even if you edit this.

**Show chart legend**

* Ticking this box will enable or disable the legend for the chart.

**Enable stacking**

* If applicable, ticking this box will stack the chart values on top of each other based on the x-axis values.
* If this is not turned on, the values will be plotted individually on the y-axis.
* The calculation underpinning this will always group the value corresponding to one value on the x-axis. Make sure your data is clean in able for this to work (avoid gaps in your data).

**Normalize to percentage data**

* This will normalize the chart to display percentage values of the chosen data table.
* The calculation underpinning this will always group the value corresponding to one value on the x-axis. Make sure your data is clean in able for this to work (avoid gaps in your data).

**Show data labels**

* Ticking this box leads to the display of the individual datapoints inside of the graph.
* This only makes sense in cases where you have few datapoints that are spread out far enough from each other to not overlap.

### Result data

Here you can pick the data points that are to be displayed.

![see explanations below](images/graphs-5.png)

You can choose one **x-axis** and multiple **y-axis.**

Alternatively, you can also choose one data series on the y-axis and choose to group it by a different column of your table (as shown in the example above).

### **X-axis options**

Using these options you can influence how your x-axis data gets displayed.

![see explanations below](images/graphs-6.png)

**Axis title**

* This field allows you to specify a title for your x-axis.

**Sort Values**

* by ticking this box you can specify if you want the values in your chart to be ordered.
* If your x-axis is a time series, this will automatically happen.

**Reverse value**

* Ticking this box will reverse the order of the values on the x-axis.

**Logarithmic**

* Ticking this box will make your x-axis values display \_\_ logarithmically.

### **Y-axis options**

With these options you can influence how your x-axis data gets displayed.

![see explanations below](images/graphs-7.png)

**Axis title**

* This field allows you to specify a title for your y-axis.

**Logarithmic**

* Ticking this box will make your x-axis values display \_\_ logarithmically.

**Enable right y-axis**

* Ticking this box will enable an additional y-axis that you can plot values on.
* You can choose in the [chart series section](graphs.md#ordering-your-series) what you want to be displayed on the left and right axis.

### **Tick formats**

![](images/graphs-8.png)

Tick formats will change how values in your chart and the axis labels will get displayed.

It follows this logic:

| Value        | Tick format | Output          | Description                                                                                                                                           |
| ------------ | ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1256784.3745 | left blank  | 1256784,3745000 | Display the full number and 7 decimals                                                                                                                |
| 1256784.3745 | 0           | 1256784         | Only Display whole numbers                                                                                                                            |
| 1256784.3745 | 0,0         | 1,256,784       | Only displays whole numbers with comma separator                                                                                                      |
| 1256784.3745 | 0,0.00      | 1,256,784.38    | Displays the value with decimals points according to the count of zeroes after the dot                                                                |
| 1256784.3745 | 0\[.]0a     | 1.2M            | <p>Displays the value in an abbreviated format.</p><p>Will display decimals of the abbreviated number according to count of zeroes after the dot.</p> |
| 1256784.3745 | $0\[.]0a    | $1.2M           | Adheres to the same methods as before, but adds a $ prefix.                                                                                           |

### Ordering your series

![](images/graphs-9.png)

In this section of the Visualization editor you can finalize your graph.

* You can rename the "series" by simply clicking into the field.
* You can change the chart type by clicking into the dropdown.
* You can change the colors by clicking into the color box.
* Finally you can also change the order of the series.

### Picking Colors

You can pick colors with your browser native color selector.

This might look slightly different for you depending on which browser you use.

![Choose any color you want!](images/graphs-color.gif)
