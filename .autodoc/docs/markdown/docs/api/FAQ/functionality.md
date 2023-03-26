[View code on GitHub](https://dune.com/blob/master/api\FAQ\functionality.md)

# Dune API Functionality

This technical guide provides answers to frequently asked questions about how the Dune API works. The guide is divided into sections that cover different aspects of the Dune API functionality. 

## General

This section provides general information about the Dune API.

### How many Requests Per Minute can I make?

The API is currently set to a rate limit of 60 requests per minute. 

### Are there specified SLAs?

SLAs will be available in the future on Enterprise pricing plans.

## Executing Queries

This section provides information on how to execute queries using the Dune API.

### How do I find a query id?

When navigating to a query, it’s the first number after “/queries/” in the URL. An example is provided in the guide.

### Does the API support Query Parameters?

The API does support Query Parameters. The guide provides information on how to pass parameter data using cURL and Python.

### What are the performance and overall differences between the Dune API and the Dune web app? What are the differences in what I can query?

There are no major performance differences or differences in what can be accessed between the two if both are using the same app plan tier. The Dune API gives you programmatic access to the capabilities and data sets that can already be accessed from the Dune web app.

### What is the execution timeout limit and can I request a longer limit?

The query execution timeout limit matches the Dune web app - 30 minutes.

### Which query engine should I use with the API?

The guide recommends using the API with v2 Dune SQL as the old v1 engine and v2 Spark SQL are being deprecated.

## Check Execution Status

This section provides information on how to check the execution status of a query.

### What is the difference between the states “Executing” and “Pending”?

Pending means the execution is waiting for an available execution connection slot. Executing means the query is currently executing against the database.

## Reading Results Data

This section provides information on how to read results data from a query.

### Can I ingest data by getting a direct connection to the database instead?

Not currently. In the interim, the guide recommends periodically fetching data in regular intervals.

### Are query results data saved for faster retrieval?

Yes!

### How long are the results data from an execution stored for?

Currently set to 2 years but may be reduced to something closer to 90 days in the future.

### How much data can I retrieve in a single API result call?

There is currently a 250MB limit, but there is a chance this may increase for certain paid plans. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.
## Questions: 
 1. What is the maximum rate limit for requests per minute and will it change in the future?
   
   The API is currently set to a rate limit of 60 requests per minute, but it will soon be set to match the rate limits specified in the varying API plan tiers.

2. How long are the results data from an execution stored for and will it change in the future?
   
   Currently, the results data from an execution are stored for 2 years, but it may be reduced to something closer to 90 days in the future.

3. Is there a limit to the amount of data that can be retrieved in a single API result call and will it change in the future?
   
   There is currently a 250MB limit, but there is a chance it may increase for certain paid plans. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.