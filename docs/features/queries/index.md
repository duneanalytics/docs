---
title: Queries
---

**The Query Editor is the place to Query for your data.**

![Query editor](images/query-editor.png)

The Query Editor consists of three parts:

* the [**data explorer**](#data-explorer) on the left
* the [**Query window**](#query-window) on the right
* the [**Query results**](#query-results) at the bottom

You can change the sizing of each of these parts by dragging the dune logo around.

![changing the layout is easy](images/layout.gif)

Let's take a look at each of these parts in more detail.

## Data explorer

The data(-set) explorer allows you to search for datasets to use in your Queries.

To learn more about Dune's datasets, please visit the [section datasets](../../tables/index.md).

![Data explorer](images/data-explorer.gif)

You can simply put in any keywords, protocol names, contract names or anything else into the search bar at the top to filter the list of available datasets down to only those you might need at that moment.

The search bar also accepts spaces, that way you can construct a multi keyword search.


Let's explore a few examples of querying for tables to further elaborate on this:

Searching for `uniswap_v2.` \_\_ will bring up all tables related to _the_ `uniswap_v2` _schema_

Searching for `uniswap_v2. evt` will bring up only event tables related to the `uniswap_v2` schema

Searching for just `uniswap` will bring up all tables that contain the keyword `uniswap` in some form.

**Takeaways**

* Always query for data schemas where applicable
* Use spaces to filter down for events, calls or specific contracts after a schema.

## Query window

The Query window is where you can work your magic in Dune.

You can input any SQL code and execute it.

![Query window](images/query-window.png)

### Autocomplete function

You can enable/disable the autocomplete function of the Query editor using the gear wheel in the top right corner. The autocomplete feature will only bring up PGSQL keywords and already used tables and aliases.

![Auto-complete](images/autocomplete.png)

### Shortcuts

A few shortcuts to make working in the Query editor easier are provided below.

| Shortcut      | Action                         |
| ------------- | ------------------------------ |
| ctrl + enter  | execute the Query              |
| ctrl + # or / | comments out the selected code |
| ctrl + space  | brings up a list of keywords   |
| crtl + z      | undoes your last changes       |
| ctrl + y      | redoes your last changes       |
| ctrl + f      | search for keywords            |
| ctrl + h      | search and replace keywords    |

## Query results

The Query results section contains a table with the results of your Query.

![Query results](images/query-results.png)

You can change the formatting and appearance of your table with the options below the table. We don't currently support hiding individual columns for displaying this table on a Dashboard, but we are looking to implement this function soon.

The tick formats follow this logic:

| Value        | Tick format | Output          | Description                                                                                                                                           |
| ------------ | ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1256784.3745 | left blank  | 1256784,3745000 | Display the full number and 7 decimals                                                                                                                |
| 1256784.3745 | 0           | 1256784         | Only Display whole numbers                                                                                                                            |
| 1256784.3745 | 0,0         | 1,256,784       | Only displays whole numbers with comma separator                                                                                                      |
| 1256784.3745 | 0,0.00      | 1,256,784.38    | Displays the value with decimals points according to the count of zeroes after the dot                                                                |
| 1256784.3745 | 0\[.]0a     | 1.2m            | <p>Displays the value in an abbreviated format.</p><p>Will display decimals of the abbreviated number according to count of zeroes after the dot.</p> |
| 1256784.3745 | $0\[.]0a    | $1.2m           | Adheres to the same methods as before, but adds a $ prefix.                                                                                           |

