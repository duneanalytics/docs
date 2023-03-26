[View code on GitHub](https://dune.com/blob/master/reference\faq\how-are-results-refreshing.md)

# App Technical Guide: How often do results get refreshed?

This technical guide provides information on how often results get refreshed in the Dune app. The guide starts by directing users to the Meta Monitoring dashboard to see the current time it takes for new data to be added to Dune. 

The guide then explains how results get refreshed in the app. When a visualization is viewed on a query page or dashboard, the Dune backend inspects the age of the most recent result. If the result is stale (currently defined as >3 hours old), Dune automatically queues an execution for this query and runs it in the background. This ensures that dashboards are always kept up to date when they are being viewed, and the query creator does not need to set a refresh schedule. 

The guide also notes that the query execution queue is separate from each individual user's queue when they create and run queries in the query editor. 

Overall, this guide provides important information on how the Dune app keeps results up to date and ensures that dashboards are always displaying the most recent data. It also highlights the Meta Monitoring dashboard as a resource for users to check the current time it takes for new data to be added to Dune. 

Example: If a user is viewing a dashboard and notices that the data is not up to date, they can refer to this guide to understand how results get refreshed in the app. They can also check the Meta Monitoring dashboard to see if there are any delays in adding new data to Dune.
## Questions: 
 1. What is the definition of "stale" data in this app and how is it determined?
   
   The definition of "stale" data in this app is data that is more than 3 hours old. This is determined by the Dune backend when inspecting the age of the most recent result.

2. Is there a way for users to manually refresh the data or set a custom refresh schedule?
   
   It is not mentioned in the app technical guide whether users can manually refresh the data or set a custom refresh schedule. However, it is stated that dashboards will always be kept up to date when they are being viewed and the query creator does not need to set a refresh schedule.

3. How does the query execution queue work and is there a limit to the number of queries that can be queued at once?
   
   The app technical guide mentions that the query execution queue is separate from each individual user's queue when they create and run queries in the query editor. However, it does not provide information on how the query execution queue works or if there is a limit to the number of queries that can be queued at once.