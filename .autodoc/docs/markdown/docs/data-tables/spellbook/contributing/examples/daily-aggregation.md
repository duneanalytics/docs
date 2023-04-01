[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/examples/daily-aggregation.md)

# Daily Aggregation

This section of the app technical guide covers the daily aggregation feature of the Dune Docs project. The purpose of this feature is to sum all transfers for the day. The table is materialized as an incrementally loaded table updated every 15 minutes because the next step includes a slower `[window](https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select-window.html)` function to capture a rolling sum.

The guide explains the novel components that make this Spell incremental. The `<div data-gb-custom-block data-tag="if"> </div>` JINJA block allows the addition of an arbitrary filter when running in “incremental” mode. Incremental mode is default and a full refresh is denoted by a command line arg to completely recreate the table. The block is used to filter for all data timestamped in the last two days. The model runs every fifteen minutes, but a look back of 2 days is allowed to account for data arriving late from the blockchain.

To avoid duplicates, a “`merge`” incremental\_strategy is used. Merge strategies require a unique key and deduplicate the table upon each update. The guide shows that a unique key is created by coalescing several transfer features together that are utilized here.

The guide also introduces the first use of “refs” in this spellset. A ref, like `{{ ref('tokens_ethereum_erc20') }}` is simply a reference to another model in the DBT project. The ref references the name of the file itself. That means, duplicate file names cannot exist.

The guide provides an example of the `transfers_ethereum_erc20_agg_day.sql` file, which contains the SQL code for the daily aggregation feature. The code includes a configuration block that specifies the alias, materialized, file format, incremental strategy, and unique key. The SQL code also includes a select statement that retrieves the required data and a group by statement that groups the data by the required fields.

The guide also provides an example of the `transfers_ethereum_schema.yml` file, which contains the schema for the Ethereum transfers. The schema includes the name of the transfer, the blockchain, the sector, the project, the contributors, the tags, and the columns. The columns include the blockchain, the hour, the wallet address, the token address, the symbol, the amount raw, and the amount USD.

In summary, this section of the app technical guide provides a detailed explanation of the daily aggregation feature of the Dune Docs project. It explains the novel components that make this Spell incremental, provides examples of the SQL code and schema files, and introduces the concept of refs.
## Questions: 
 1. What is the purpose of the Daily Aggregation table in the Dune Docs app?
- The Daily Aggregation table sums all transfers for the day and is materialized as an incrementally loaded table updated every 15 minutes.

2. How does the app handle duplicates in the Daily Aggregation table?
- The app uses a "merge" incremental strategy that requires a unique key and deduplicates the table upon each update.

3. What is a ref in the Dune Docs app and how is it used?
- A ref is a reference to another model in the DBT project and is used to reference the name of the file itself. It cannot have duplicate file names.