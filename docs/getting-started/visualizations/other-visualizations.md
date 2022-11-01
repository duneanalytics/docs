---
title: Other Visualizations
description: Here are a few non-graph visualizations you can make with Dune!
---

Here are a few non-graph visualizations you can make with Dune!

## Tables

Tables are the default Visualization you'll find labeled <span class="fk-btn-4">Query results</span> whenever you create and run a Query:

![query results table example](images/query-results-table-example.png)

You can also make more Tables to display your data differently using the <span class="fk-btn-2">New visualization</span> button and drop down menu:

![new table visualization](images/new-table-visualization.png)

### Configuring your Table

![table configuration options](images/table-configuration-options.png)

#### Table options

**Title**

The Title appears at the top of your Table.

Leaving default value (`Table`) or making this blank makes your Table title the same as your Query's title/name.

Adding any other value to this field will add that value first, followed by your Query Name:

![table title example](images/table-title-example.png)

Note: the default value for "Query Results" is treated like an added value.

#### "Column [x]:" options

You can configure the following options for each column in your Table

=== "Title"

    The Title appears at the top of your Table.

    Leaving this blank makes your column title the same as your it's Dune database name.

=== "Align"

    This changes the text alignment for the column data and title.

=== "Format"

    Allows you to adjust the numerical format of your data following the [X/Y-axis Tick and Label formats here](../visualizations/charts-graphs.md#xy-axis-tick-and-label-formats).

=== "Hide Column"

    Hides this column from your table.

***

#### Numerical Column options

Columns that return numerical data have these additional options:

=== "Type"

    - `Normal` simply displays the column's numerical data.
    - `Progress bar` shows the column's numerical data with a progress bar visual that is "full" for the columns highest value and "nearly empty" for the columns lowest value, with the rest of the data ranging in between:

    ![progress bar example](images/progress-bar-example.gif)

=== "Colored Values"

    Check these boxes to color <span style="color:var(--success-green)">Positive Values Green</span> and <span style="color:var(--danger-red)">Negative Values Red</span>.

***

## Counters

Counters are a great way to provide your audience with immediate "on a glance" stats.

!["on a glance" stats in https://dune.com/0xBoxer/NFT](images/counters-1.png)

### Configuring your Counter

![Counters 2](images/counters-2.png)

#### Counter options

In this section you can define what kind of data the counter should display:

=== "Title"

    * The Title will appear in all instances of this graph prominently at the top
    * If left blank the Query name will be the only thing that is left standing

=== "Column"

    * In this field you can define which column the counter should show.

=== "Row"

    * This field can be used to define which row of the underlying data table you want displayed e.g. row 1
    * Usually this requires you to sort or limit your Query results in order for row 1 to show the wanted results.

***

#### Formatting

This section is where you can adjust how your numerical data is displayed.

=== "Prefix"

    * This field allows you to define a prefix for your counter value.
    * e.g.: `$`, `€`, `Ξ`, `฿`

=== "Suffix"

    * This field allows you to define a suffix for your counter value.

=== "Label"

    * This field allows you to define a label for your counter value.
    * The label will appear beneath the counter value as text.

=== "Decimals"

    * In this field you can choose how many decimals you want displayed for your counter
    * This is currently limited to 3 decimal places.

***

![label](images/counters-label-1.png)

![label configuration](images/counters-label-2.png)
