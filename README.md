# Introduction to Dune Analytics

## Introduction

**Dune Analytics is a powerful tool for blockchain research. Dune gives you all the tools to query, extract, and visualize vast amounts of data from the blockchain. Dune is unlocking the power of public blockchain data by making it accessible to everyone. This documentation will help you answer questions like:**

[How much volume flows through Uniswap each day?](https://duneanalytics.com/queries/3)

[Which Dex has the highest volume?](https://duneanalytics.com/queries/1847)

[How are important Stablecoins behaving today?](https://duneanalytics.com/hagaetc/stablecoins)

**Try It**

Follow along the **Try it** blocks to get a grasp on Dune.

* [ ] Create a user for free at [duneanalytics.com](./) and set up a basic profile

## Dune Analytics Basics

While navigating Dune Analytics, it helps to have a good understanding of [queries](./#queries), [visualizations](./#visualizations), and [dashboards](./#dashboards). These are the basic building blocks that act as your portal to the world's blockchain information. As a blockchain analyst, you can create custom queries to fetch data, visualize the results of these queries, and then tell stories with your data using dashboards.

Behind the scenes, Dune transforms difficult-to-access data into human-readable tables. These abstractions make it possible to write SQL queries that retrieve information from the blockchain. Dune also gives you access to [other users' public queries](https://duneanalytics.com/browse/queries) so you can pick up where they left off.

**Try it**

* [ ] Browse the [Queries](https://duneanalytics.com/browse/queries) and [Dashboards](https://duneanalytics.com/browse/dashboards) pages, see what information you can find!

## Queries

Dune aggregates blockchain data into SQL databases that can be easily queried. Queries are used to specify what data from the blockchain should be returned.

Maybe you want to know _all the Dex trades that happened today_, or the _total value of stablecoins minted this year_. Whatever the question, the answer likely starts with a Dune query.

Queries return rows and columns of data \(same as traditional SQL queries\) that can later be visualized and presented.

![Screen Shot 2021-04-22 at 9 56 34 AM](https://user-images.githubusercontent.com/76178256/115726979-357d1380-a351-11eb-83ee-16f0d57c6ecb.png)

There are a few ways that a blockchain analyst \(ie. you!\) can get started running queries:

1. Use Dune Analytics _abstractions_ to query commonly used data tables. This is the simplest and most common way to use Dune Analytics. Some popular abstractions include `dex.trades`, `lending.borrow`, and `stablecoin.transfer` \(you can find a complete list of abstractions [here](https://github.com/duneanalytics/abstractions)\)
2. Query the raw ethereum data including blocks, logs, and transactions.
3. It is also possible to query centralized exchange data. Use `prices.usd` to quickly return the price of almost any cryptoasset

**Try It**

* [ ] Run a query using one of the abstractions listed above to return some results
* [ ] Analyze the results and answer the question: what am I looking at? 

Tip: what data populates each row and what populates each column?

If you are having trouble returning results try running this code in the query editor:

```sql
SELECT
    date_trunc('day', block_time) AS day,
    SUM(usd_amount) AS usd_volume
FROM dex.trades
WHERE block_time > now() - interval '7 days'
AND project = 'Uniswap'
GROUP BY 1
ORDER BY 1;
```

Once that is running, edit the query and try to understand how different edits change the results.

## Visualizations

Data presented in table form \(rows and columns\) can be difficult to read. Visualizations take the results of a query and present the information in a clear & precise way.

You can use visualizations to begin to tell a story with your data. With Dune visualizations it is easy to transform this:

![Screen Shot 2021-04-22 at 10 59 48 AM](https://user-images.githubusercontent.com/76178256/115737269-fa331280-a359-11eb-9a31-c0dfe4b038e6.png)

Into this:

![Screen Shot 2021-04-22 at 11 01 02 AM](https://user-images.githubusercontent.com/76178256/115737692-5b5ae600-a35a-11eb-8145-bdcf9396cd03.png)

The bar chart visualization makes it clear that April 19th had the highest transfer volume, and helps the audience see the trend over time.

Dune offers a variety of visualizations that you can use to visually present data including bar charts, area charts, line charts, pie charts, and more.

**Try It**

* [ ] Using the results of your query from the previous section, add a visualization to the query results

## Dashboards

  Now that there is a clear visualization of some query results, it's time to group visualizations together in a dashboard. Dune dashboards are where blockchain data comes to life:

![Screen Shot 2021-04-23 at 10 51 25 AM](https://user-images.githubusercontent.com/76178256/115889404-e7841080-a421-11eb-9e30-8d43e58e28f4.png)

Using carefully planned visuals, a clever blockchain analyst can tell a story about a particular group of data. For example, in the [above dashboard](https://duneanalytics.com/hagaetc/dex-metrics) it is clear at the top that 'Dex' as a category is growing. Below, the audience sees which dex's are the most popular by volume, and finally can view a stacked bar chart that shows changes over time. By just looking at this single dashboard, the audience sees a clear picture of the entire Dex market.

**Try It**

* [ ] Group some visualizations into a dashboard to tell a story about a set of blockchain data

## Dune is a collaborative effort

On Dune, all queries and datasets are public by default.

This introduces a interesting dynamic in which you, the user, can fork and remix the queries of other creators with ease and build on top of their knowledge. On the other side, every time you write a new query, you contribute to the collection of queries that help people query for data on dune. That way, the Dune Community succeeds together through an ever improving range of queries that allow you to easily query for just the stats you need.

If you do need Privacy for your Queries, the Pro Plan has got you covered.

Join our [Community Discord](https://discord.gg/BJBHFR6sdy) to get world class support from our team and the community.







\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

This Intro was mostly written by [zkwaffles](https://twitter.com/zkwaffles), huge thank you for that.



