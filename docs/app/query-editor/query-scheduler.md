---
title: Scheduling a Query
description: Queries can now be set to run on a schedule to keep dashboards up to date more reliably!
---

Queries can now be set to run on a schedule to keep dashboards up to date more reliably! We’ll also be adding additional functionality such as webhooks, alerts, and updating materialized views using query schedules.

!!!Caveat

- Scheduling isn’t available on queries with params
- When queries are archived or when the ownership changes (e.g. query migrated), the query schedule is removed
- There are currently no notifications in place for if a scheduled query fails

### How to schedule a query

To schedule a query, click the scheduler icon on the query editor page.
![](images/query-scheduler/schedule_query_start.PNG)

You’ll be prompted to set a refresh schedule and an execution tier. Scheduled queries can **only be scheduled on medium and large query engines, which uses credits**.
An estimated monthly credits consumption for this query scheduling will be shown to you, alongside with a monthly estimated quota. They will be adjusted based on the frequency and execution tier you choose.
![](images/query-scheduler/schedule_query_schedule.PNG)

Your query will be run once saved. You can see a scheduler frequency next to the scheduler icon.
![](images/query-scheduler/schedule_query_see_estimate.PNG)

💭 Have an additional feature request for scheduled queries? [Request them here](https://feedback.dune.com/)! We’re regularly adding additional improvements.
