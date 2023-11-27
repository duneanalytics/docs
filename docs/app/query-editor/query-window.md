---
title: Writing Queries
description: The query editor allows you to query blockchain data using DuneSQL.
---

The Query Editor is where you construct your queries. You'll probably spend most of your time here.

![Query editor](images/query-window/query-window.png)

To learn more about how to write queries, check out the [query documentation](../../query/index.md).

## Understanding the query editor

The Query editor is pretty straightforward. It's a text editor where you can write SQL code.

The editor has a few features that make your life easier:

- [Autocomplete](#autocomplete)
- [Run selection](#run-selection)
- [Explain Query](#explain-query)
- [Parameters](#parameters)


### Autocomplete

The autocomplete feature will bring up DuneSQL keywords, as well as tables and aliases you've already included in your Query.
You can always bring up the autocomplete menu by pressing `ctrl/cmd + space`.

Turn it on/off in the settings.

### Run selection

To save yourself time while testing and debugging your Queries, you can run just a part of your Query.

To do this, highlight a part of your Query. You'll then see the <span class="fk-btn-1">Run</span> button turn into a <span class="fk-btn-1">Run selection</span> button.

<div style="position: relative; padding-bottom: calc(67.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/Jb2fyuNXBUSLAcMyAOsH?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dune"></iframe></div>


### Parameters

Parameters allow you to implement variables in certain parts of your Query. This is useful if you want to create a Query that you can reuse with different parameters. 

To use parameters:

1. choose the spot in your Query where you want to implement a parameter
2. click on the add parameter button or type `{{example_parameter_name}}``
3. open the parameter options 
4. configure your parameter's name, type, and default value

Parameters can be text, numbers,a date, a manual list of values or a list of values from a different query.

<div style="position: relative; padding-bottom: calc(50.67708333333333% + 41px); height: 0;"><iframe src="https://demo.arcade.software/wEVEG2p4ns4oXV5LSpJ3?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Net flow of stake ETH last 7 days"></iframe></div>



!!! info "Parameter types"

    There are 5 different parameter types:

    - Text
    - Number
    - Date
    - List (single value)
    - List (multiple values)

    Each parameter type has different options. You can read more about each type below.

    === "Text parameters"

        Text parameters are useful if you want to use the same query with different addresses, tokens, or other text values.

        To use a text parameter:

        ``` sql
        Select * from transactions
        where from_address = {{example_parameter_name}}
        ```

    === "Number parameters"

        Number parameters are useful if you want to use the same query with different numbers.

        For example:

        ``` sql

        Select * from dex.trades
        where amount_usd > {{example_parameter_name}}
        ```

    === "Date parameters"

        Date parameters are useful if you want to use the same query with different dates.

        For example:

        ``` sql
        Select * from dex.trades
        where evt_block_time > {{example_parameter_name}}
        ```

    === "List parameters (single value)"

        List parameters are useful if you want to use the same query with different lists of values.

        For example:

        ``` sql
        Select * from dex.trades
        where pair = {{example_parameter_name}}
        ```

    === "List parameters (multiple values)"

        When you use a list parameter, you can choose to allow multiple values. You need to adjust your query to account for this.

        For example:

        ``` sql
        Select * from dex.trades
        where token_pair in (Select pair from unnest(split('{{example_parameter_name}}',',')) as c(pair))
        ```

!!! info "Using query results as a parameter list"

    You can use the results of a different query as the list of values for a parameter. To do this:

    1. choose the spot in your Query where you want to implement a parameter
    2. click on the add parameter button or type `{{example_parameter_name}}``
    3. open the parameter options
    4. choose the parameter type `list`
    5. choose `list options from a query`
    6. input the query id of the query you want to use as the list of values
    7. input the column name of the column you want to use as the list of values
    8. choose if you want to allow multiple values
    9. select default values

    

        
If you want to use the same parameter between different queries on a dashboard, make sure to use exactly the same settings for the parameter in each query. The parameter will  then be shared between the queries and only turn up once in the dashboard's parameter menu.


Text parameters are useful if you want to use the same query with different addresses, tokens, or other text values.

To use a text parameter:

``` sql
Select * from transactions
where from_address = {{example_parameter_name}}
```

#### Number parameters

Number parameters are useful if you want to use the same query with different numbers.

For example:

``` sql

Select * from dex.trades
where amount_usd > {{example_parameter_name}}
```

#### Date parameters

Date parameters are useful if you want to use the same query with different dates.

For example:

``` sql
Select * from dex.trades
where evt_block_time > {{example_parameter_name}}
```

#### List parameters (single value)

List parameters are useful if you want to use the same query with different lists of values.

For example:

``` sql
Select * from dex.trades
where pair in {{example_parameter_name}}
```

#### List parameters (multiple values)

When you use a list parameter, you can choose to allow multiple values. You need to adjust your query to account for this.

For example:

``` sql
Select * from dex.trades
where token_pair in (Select pair from unnest(split('{{example_parameter_name}}',',')) as c(pair))
```




If you want to use the same parameter between different queries on a dashboard, make sure to use exactly the same settings for the parameter in each query. The parameter will then be shared between the queries and only turn up once in the dashboard's parameter menu.




### Parameter list from a different query

A parameter can be a list of values. You can use the results of a different query as the list of values for a parameter.

To do this:

1. choose the spot in your Query where you want to implement a parameter
2. click on the add parameter button or type `{{new_parameter_name}}``
3. open the parameter options
4. choose the parameter type `list`
5. choose `list options from a query`
6. input the query id of the query you want to use as the list of values
7. input the column name of the column you want to use as the list of values
8. 



### Explain Query

The explain query feature utilizes ChatGPT4 to explain your query in plain English. It's a great way to get a quick overview of what your query does.

Simply click the explain query button to see a GPT4 generated explanation of the query.

![Explain query](images/query-window/explain-query.jpeg)


### Shortcuts

Here are a handful of shortcuts to make crafting Queries easier:

| Shortcut      | Action                         |
| ------------- | ------------------------------ |
| ctrl + enter  | execute the Query              |
| ctrl + # or / | comments out the selected code |
| ctrl + space  | brings up a list of keywords   |
| crtl + z      | undoes your last changes       |
| ctrl + y      | redoes your last changes       |
| ctrl + f      | search for keywords            |
| ctrl + h      | search and replace keywords    |

_These shortcuts work on US/UK Keyboards and might vary based on the language setting on your device._

## Query results

The Query results are displayed in a table below the Query editor.

You can sort the results by clicking on the column headers. Click once to sort ascending, click again to sort descending.
Results are paginated, so you can click through the pages to see more results. Each page shows 25 results.

You can full text search the results by using the search bar below the results table.

You can format the results according to the rules laid out in the [tables section](../visualizations/tables.md) of the documentation.

<div style="position: relative; padding-bottom: calc(50.67708333333333% + 41px); height: 0;"><iframe src="https://demo.arcade.software/FrOeNaAh5HBsESAvGUGm?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Net flow of stake ETH last 7 days"></iframe></div>

