---
title: Formatting Tables
description: Tables are a way to display your data in a tabular format.
---

**Tables are the default Visualization whenever you create and run a Query.**

![query results table example](images/other-visualizations/query-results-table-example.png)

You can also make more Tables to display your data differently using the <span class="fk-btn-2">New visualization</span> button and drop down menu:

![new table visualization](images/other-visualizations/new-table-visualization.png)

### Configuring your Table

![table configuration options](images/other-visualizations/table-configuration-options.png)

#### Table options

**Title**

The Title appears at the top of your Table.

Leaving default value (`Table`) or making this blank makes your Table title the same as your Query's title/name.

Adding any other value to this field will add that value first, followed by your Query Name:

![table title example](images/other-visualizations/table-title-example.png)

Note: the default value for "Query Results" is treated like an added value.

#### "Column [x]:" options

You can configure the following options for each column in your Table

=== "Title"

    The Title appears at the top of your Table.

    Leaving this blank makes your column title the same as its Dune database name.

=== "Align"

    This changes the text alignment for the column data and title.

=== "Format"

    Allows you to adjust the numerical format of your data following the [X/Y-axis Tick and Label formats here](charts-graphs.md#xy-axis-tick-and-label-formats).

=== "Hide Column"

    Hides this column from your table.

***

#### Numerical Column options

Columns that return numerical data have these additional options:

=== "Type"

    - `Normal` simply displays the column's numerical data.
    - `Progress bar` shows the column's numerical data with a progress bar visual that is "full" for the column's highest value and "nearly empty" for the column's lowest value, with the rest of the data ranging in between:

    ![progress bar example](images/other-visualizations/progress-bar-example.gif)

=== "Colored Values"

    Check these boxes to color <span style="color:var(--success-green)">Positive Values Green</span> and <span style="color:var(--danger-red)">Negative Values Red</span>.

    ![colored values example](images/other-visualizations/colored-values-example.jpeg)

