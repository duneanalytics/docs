---
title: Optimizing Your Usage
description: Optimize your usage with the Dune API!
---

Here are some simple tips to optimize your usage (and billing) with the Dune API.

### The LIMIT keyword

Until your code looks ready and has been tested to fetch the data you need, use the `LIMIT` keyword at the end of any SQL query you are fetching data from. 

Let us take a simple query, for example.

``` sql title="example query"
SELECT * FROM nft.trades;
```
Here is how you can run the same query but only fetch the first ten rows.

``` sql title="example query with LIMIT"
SELECT * FROM nft.trades
LIMIT 10;
```
If you are using queries prepared by accounts other than yours, you can fork and then edit those queries to add this little change.

### Filter with Dates

If you need data for a specific timeframe, you can filter the query you call with a `WHERE` clause.

Here is the same example query in the previous sections, filtered by date.

``` sql title="example query with date filtering"
SELECT * FROM nft.trades
WHERE "block_time" > '2023-01-01';
```

### Filter using Parameters

We recommend using parameterized queries when you need to call the same query multiple times with slight changes.

Here is the same example query from the previous section. But instead of hardcoding the `date` we are filtering with, we pass it as a parameter. You can learn more about parameterized queries in [this section](../getting-started/queries/parameters.md) of our docs.

``` sql title="example query with parameter based filtering"
SELECT * FROM nft.trades
WHERE "block_time" > '{{date}}'
```

!!! Local Storage
    If there is data that you frequently need to call with the API. You can store it locally. And use your local database for that data. You can also keep updating this data dynamically using the tips described in this section, particularly parameterized queries.