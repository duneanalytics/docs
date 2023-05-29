---
title: Scheduling Queries
description: Learn how to leverage the power of query scheduling for a more reliable and up-to-date dashboard display!
---

**Query Scheduling allows you to schedule a query to run at a specific time and frequency.**

### How to Schedule a Query

<div style="position: relative; padding-bottom: calc(50.67708333333333% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/HDqYf2VdwfwMdHFzKh6u?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Query Scheduler V2"></iframe></div>


1. Start by clicking the scheduler (clock) icon located at the bottom of the query editor, to the left of the "Run" button
2. A dialog will prompt you to set a refresh schedule and an execution tier. Please note that scheduled queries can only be run on medium and large query engines, which will require credits.
3. The dialog will display an estimated monthly credit consumption for this query scheduling, along with a monthly quota. These values will adjust based on the frequency and execution tier you select.
4. Save the schedule
5. Your query will execute once to start the schedule, and then will execute according to the schedule you set.

!!! warning
    - Query scheduling is currently not available for queries with parameters.
    - The query schedule is removed when the queries are archived or when the ownership changes (e.g., when a query is migrated).
    - There are no notifications available for scheduled query failures as of now.
#### Adjusting or Cancelling a Query Schedule

If you need to modify or cancel a query schedule, click on the scheduler icon to open the scheduling dialog. Make changes as needed or click "Stop" to cancel the schedule.

![](images/query-scheduler/schedule_query_cancel.gif)

### Why Schedule a Query? 

Scheduled queries are useful for ensuring that your query or dashboard displays the most up-to-date data. They give you the flexibility to schedule queries to run at a specific time and frequency, and to choose the execution tier (medium or large) for the query. 

Queries that are not scheduled will only update when a user triggers an automatic or interactive execution. This means that if you have a dashboard that is not frequently viewed, the data displayed on the dashboard may be outdated and execution of the queries will only be triggered when a user views the dashboard. Especially for dashboards that contain resource-intensive queries, this can lead to long loading times for the user.

To understand how scheduled queries help with this, a short excursion into how queries are executed on Dune is necessary:   

- **Interactive executions** are manually triggered by a user clicking the "Run" button in the query editor page or a dashboard. Additionally, interactive executions can also be triggered by the [API](../api/README.md). Interactive executions can be routed via the community, medium, or large cluster, depending on the query engine selected.  

- **Automatic executions** are triggered whenever any user on Dune encounters a widget on a dashboard and the widget's underlying query results are "expired". As of now, query results are set to expire every 6 hours, although this is subject to change. These automatic executions are always routed via the community cluster.

Since the community cluster can get quite busy, we cannot guarantee that all automatic query executions will finish within the given 30-minute query timeout limit.

**Scheduling queries allows you to choose a higher execution frequency and execution tier, which will ensure that your queries are executed reliably and in a timely manner.** 
### Additional Info
➕ We plan to extend the functionality of query scheduling with webhooks, alerts, and the ability to update materialized views. We are also working on a allowing you to schedule a whole dashboard at once. Stay tuned for updates!

💭 Have an idea for additional features for scheduled queries? Please [submit them here](https://feedback.dune.com/)! We value your input and are regularly implementing improvements based on user feedback.
