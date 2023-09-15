---
title: Quickstart
description: Get started on Dune in five minutes!
---
<p align="center">
  <img src="../images/quickstart-cover.jpeg" alt="A beautiful dashboard" title="Dashboard" /><br />
  <em>The world's blockchain data at your fingertips!</em>
</p>


### Welcome to Dune


This guide will help you get started on Dune in five minutes. We'll walk you through how to:

1. Query blockchain data
2. Create a visualization
3. Present your data

Dune has many more features, but these are the basics you'll need to get started. If you're looking for more advanced guides, check out the [Analytics Guidelines](./learning/index.md) and [Data Tables](data-tables/index.md) sections.

**Prerequisites:**   
- You'll need to have a Dune account to follow along. If you don't have one, you can [sign up here](https://dune.com/auth/register).  
- We also recommend you have a basic understanding of SQL and Blockchain concepts.

### 1. Query blockchain data

To query for blockchain data on Dune you'll need to:

1. Create a new query
2. Write some SQL
3. Run the query
4. Name and save the query

```sql
--Query to get Ethereum's unique daily active users and passive users  in 2023

SELECT  
--truncate time to day
date_trunc('day', block_time) AS time,
-- count distinct addresses that sent a transactions
COUNT(distinct "from") AS users,
-- count distinct addresses that received a transaction
COUNT(distinct "to") AS receiving_addresses
FROM ethereum.transactions
WHERE block_time > DATE '2023-01-01'
GROUP BY 1
```

**[Direct link to query here.](https://dune.com/queries/2335378)**  

<div style="position: relative; padding-bottom: calc(66.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/gT2ctqjvwIuX5xUXPx5S?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dashboards"></iframe></div>



### 2. Create a visualization

To create a visualization you'll need to:

1. Create a new visualization
2. Select the type of visualization you want to create
3. Choose the data source for the x and y axis
4. adjust the visualization settings

In our example below, we'll create a line chart to visualize the number of unique daily active users and passive users on Ethereum in 2023. Additionally, we format the axis label and tick label to `0a`to make the numbers more readable.

<div style="position: relative; padding-bottom: calc(66.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/nNxDjw8vBmp34u3aNU0R?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Dashboards"></iframe></div>


### 3. Present your data

To present your data you'll need to:

1. Create a new dashboard
2. Add a visualization to the dashboard
3. Adjust the layout of the dashboard
4. Name and save the dashboard

<div style="position: relative; padding-bottom: calc(66.66666666666666% + 41px); height: 0;"><iframe src="https://demo.arcade.software/xTAXmlo0nCL0FOn38hW9?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Creating a dashboard"></iframe></div>


### Recap

**Congratulations, you've just queried blockchain data, created a visualization, and presented your data on Dune!**

You can now share your dashboard with the world.

We'll take care of updating this dashboard whenever somebody looks at it, so you don't have to worry about keeping it up to date.

### Next steps

Check out these resources to learn more about Dune:

- [Dune Official Getting Started Video Series](https://www.youtube.com/watch?v=S-cctFmR828&list=PLK3b5d4iK10ext4v-GBySekaA8-GP8quD&index=1) to learn how the data flows and how to navigate the Dune app to create queries, visualizations, and dashboards. 

- [Weekly Web3 SQL problems](https://daodatadesign.notion.site/Web3-SQL-Weekly-0bababb5e59a412bb73594c512db8cc1) to learn wizard tips and tricks in byte-sized bits. Covers things like token balances, protocol integrations, product metrics, and much more.

- [All Ethereum and SQL Basics](https://web3datadegens.substack.com/p/a-basic-wizard-guide-to-dune-sql) to learn all the basic SQL concepts and Ethereum tables you'll need in your analysis.

- For pure SQL practice, try going through the "easy" problems [on hackerrank](https://www.hackerrank.com/domains/sql).

Join the community and learn together [in Discord](https://discord.com/invite/ErrzwBz) by participating in the `#🐥︱beginners` and `#🙋︱query-questions` channels

And when you feel ready to do advanced analysis, check out the [next guide](./learning/index.md)