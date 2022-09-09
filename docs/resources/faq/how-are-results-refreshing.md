---
title: How are results refreshing?
---


# How do results refresh?

When a Visualization is viewed, either on a query page or on a dashboard, the Dune backend will inspect the age of the most recent result. If the result is stale (currently defined as >3 hours old), Dune will automatically queue an execution for this query and run it in the background.

This means that dashboards will always be kept up to date when they are being viewed and the query creator does not need to set a refresh schedule.

Note that the query execution queue is separate from each individual users queue when they create and run queries in the query editor.
