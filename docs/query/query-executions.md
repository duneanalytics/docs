---
title: Executions
description: When and how do queries on Dune get executed?
---

# Overview

**Queries on Dune need to be triggered and will be executed on one of our query engines.**

Query executions can be triggered by any user/team in Dune for public queries and by the owner of the query for private queries. Query executions can be triggered through the query editor, the dashboard editor, or via the API. We also automatically refresh popular dashboards automatically in regular intervals. 

The query engine determines the amount of resources allocated to your query. The larger the query engine, the more resources are allocated to your query. This means that queries executed on a larger query engine will run faster and are less likely to time out.

## Query executions triggers

Query executions on Dune are triggered in four ways:

1. **Interactive executions** are manually triggered by a user clicking the "Run" button in the query editor page or refreshing an entire dashboard. Interactive executions can be routed via the community, medium, or large cluster, depending on the query engine selected.

2. **Scheduled executions** are triggered at a specific time and frequency. Scheduled executions can be routed via the medium or large cluster, depending on the execution tier selected.

3. **API executions** are triggered by an API call. API executions can be routed via the community, medium, or large cluster, depending on the query engine selected.

4. **Popular dashboards** are automatically refreshed based on their popularity. We measure popularity based on the number of views a dashboard has received. The most popular dashboards are refreshed every hour, the less popular dashboards are refreshed every 24 hours. Popular dashboards are refreshed via the community cluster.

**Here is an overview of the different execution triggers:**

=== "interactive dashboard execution"

    <div style="position: relative; padding-bottom: calc(57.58333333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/inelINzxmsLyvP2pj7Re?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="interactive dashboard executions"></iframe></div>

=== "interactive query execution"

    <div style="position: relative; padding-bottom: calc(57.58333333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/9RYMKYvePPjNV4kVjIt4?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="interactive query execution"></iframe></div>


=== "scheduled query execution"

    <div style="position: relative; padding-bottom: calc(50.67708333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/HDqYf2VdwfwMdHFzKh6u?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Query Scheduler V2"></iframe></div>

=== "scheduled dashboard execution"

    <div style="position: relative; padding-bottom: calc(63.83333333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/doDebCcmeiVj5xKiq4nK?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Meta Monitoring"></iframe></div>

=== "API query execution"

    You can trigger query executions via the API. This is useful if you want to embed a query result in your own application or if you want to trigger a query execution via a cron job.

    [→ API executions](../api/api-reference/execute-queries/index.md)

=== "popular dashboard executions"

    Popular dashboards are automatically refreshed based on their popularity. We measure popularity based on the number of views a dashboard has received. The most popular dashboards are refreshed every hour, the less popular dashboards are refreshed every 24 hours. Popular dashboards are refreshed via the community cluster.

    ![](../query/images/popular%20dashboard.jpeg)

**Learn more about the different execution triggers:**


<div class="cards grid" markdown>

-   #### Interactive executions

    ---

    Trigger: user clicks "Run" button in query editor or refreshes dashboard

    [→ Interactive executions](../app/query-editor/query-window.md)

-  #### Scheduled executions

    ---

    Trigger: scheduled dashboard or query

    [→ Scheduled queries](../app/query-editor/query-scheduler.md)
    [→ Scheduled dashboards](../app/dashboards.md#keeping-your-dashboard-up-to-date)

- #### API executions

    ---

    Trigger: API call

    [→ API executions](../api/api-reference/execute-queries/index.md)

- #### Popular dashboards

    ---

    Trigger: Dashboard popularity


</div>


## Query engine size

Dune has three query engine sizes: **community**, **medium**, and **large**. The query engine size determines the amount of resources allocated to your query. The larger the query engine, the more resources are allocated to your query. This means that queries executed on a larger query engine will run faster and are less likely to time out.

<div style="position: relative; padding-bottom: calc(57.58333333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/qEa2Yifc6aUHvSO3p0QA?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Query engine size selector"></iframe></div>



#### Community engine

The community engine is the default query engine for all queries on Dune. It is a shared cluster, meaning that it is used by all Dune users. This means that the community cluster can be busy at times, if many users are running queries at the same time. 
To avoid long loading times and timeouts, we recommend using the medium or large engine for resource-intensive queries.   
Executions on the community engine are free of charge.

#### Medium engine

The medium engine is built to handle most queries on Dune. It is cheap, reliable and fast. The medium engine will scale up and down depening on the demand. In contrast to the community engine, that means that running a query on the medium engine will not be affected by other users' queries.   
Executions on the medium engine cost 10 credits.

#### Large engine

The large engine is built to handle the most resource-intensive queries on Dune. It's blazing fast, reliable and can easily deal with large amounts of data. The large engine also scales up and down depending on the demand. Running a query on the large engine will not be affected by other users' queries.   

In addition to that, the large engine is also the only engine that can handle queries that requires lots of planning time. This mostly happens when you query a large amount of data, when you use a lot of joins or large aggregate window functions.
   
Executions on the large engine cost 20 credits.
