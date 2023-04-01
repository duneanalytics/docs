[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/show-stats.md)

The "Show Stats" section of the app technical guide covers the functionality of the `SHOW STATS` command in the Dune Docs project. This command is used to retrieve approximated statistics for a specified table or query. The syntax for using this command is `SHOW STATS FOR table` or `SHOW STATS FOR (query)`.

The returned statistics are presented as a row for each column, as well as a summary row for the table. The columns returned include `column_name`, `data_size`, `distinct_values_count`, `nulls_fractions`, `row_count`, `low_value`, and `high_value`. The `column_name` column displays the name of the column, while the `data_size` column displays the total size in bytes of all the values in the column. The `distinct_values_count` column displays the estimated number of distinct values in the column, while the `nulls_fractions` column displays the portion of values in the column that are `NULL`. The `row_count` column displays the estimated number of rows in the table, while the `low_value` and `high_value` columns display the lowest and highest values found in the column, respectively.

It is important to note that any additional statistics collected on the data source, other than those listed in the table, are not included in the returned statistics. Additionally, if any statistics are not populated or unavailable on the data source, they will be returned as `NULL`.

An example of using the `SHOW STATS` command would be `SHOW STATS FOR my_table`, which would return the approximated statistics for the `my_table` table. Another example would be `SHOW STATS FOR (SELECT * FROM my_table WHERE column_name = 'value')`, which would return the approximated statistics for the results of the specified query.
## Questions: 
 1. What is the data source for the statistics returned by this app?
- The app technical guide does not provide information on the data source for the statistics returned.

2. Can this app be used to gather statistics on tables or queries from a blockchain database?
- The app technical guide does not mention anything specific to blockchain databases, so it is unclear whether it can be used for this purpose.

3. How accurate are the estimated statistics returned by this app?
- The app technical guide does not provide information on the accuracy of the estimated statistics returned.