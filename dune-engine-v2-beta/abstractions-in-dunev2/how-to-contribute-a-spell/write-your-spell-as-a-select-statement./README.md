# ⛏ Write your spell as a select statement.

Everything in a \`.sql\` file should solely consist of a `select` statement. You don’t need to specify `create view` or `create table`. [Materialization strategies](https://docs.getdbt.com/docs/building-a-dbt-project/building-models/materializations) are handled by JINJA blocks or by the YAML schema file for the model.

Models will (by default) be views but we can override that to make them tables or incrementally loaded tables.

The basic trade-off is that a view is fast to create and doesn’t require additional storage but is slower to query. A table is much slower to create and does require additional storage but is faster to query. Generally, we’ll try to stick to views but upgrade to tables or incrementally loaded tables if performance is an issue.

In our case, we have broken down the spell into a more modular series of spells.

1\) A reformatted transfers table.&#x20;

2\) A daily aggregation of transfers.&#x20;

3\) Rolling sum of daily transfers.&#x20;

4\) Final daily Ethereum ERC20 token balances spell
