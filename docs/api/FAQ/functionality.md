---
title: Dune API Functionality
description: Answers to questions about how the Dune API works.
---
# FAQ: Functionality

## General

### How many Requests Per Minute can I make?

The API is currently set to a rate limit of 60 requests per minute. This will soon be set to match the rate limiits specified in the varying API plan tiers. 

### Are there specified SLAs?

SLAs will be available in the future on Enterprise pricing plans.

## Executing Queries

### How do I find a query id?

When navigating to a query, it’s the first number after “/queries/” in the URL.

![query-id-example](../images/query-id-example.jpg)

### Does the API support Query Parameters?

The API does support Query Parameters!

For Dune Queries that include Parameters, you can pass parameter data as part of the [Execute Query ID endpoint](../../api/api-reference/execute-query-id.md)!

Learn more about [building Dune Queries with Parameters here](../../getting-started/queries/parameters.md).

And learn how to pass parameter data using [cURL here](../../api/api-reference/execute-query-id.md#curl-with-parameters) and with [Python here](../../api/quick-start/api-py.md#parameterized-queries).

### What are the performance and overall differences between the Dune API and the Dune web app? What are the differences in what I can query?

There are no major performance differences or differences in what can be accessed between the two if both are using the same app plan tier.

The Dune API gives you programmatic access to the capabilities and data sets that can already be accessed from the Dune web app.

### What is the execution timeout limit and can I request a longer limit?

The query execution timeout limit matches the Dune web app - 30 minutes.

### Can I query using both Dune v2 Engine and the original v1 databases?

Currently yes, but we’re slowly deprecating usage and support of the old v2 engine, so we recommend using the new Dune Engine v2 (Spark SQL) as much as possible.

Dune Engine v2 (Dune SQL) is still in alpha and it's recommended to postpone using this query engine for critical API use cases until mid Feb 2023.

## Check Execution Status

### What is the difference between the states “Executing” and “Pending”?

Pending means, the execution is waiting for an available execution connection slot.

Executing means the query is currently executing against the database.

## Reading Results Data

### Can I ingest data by getting a direct connection to the database instead?
    
Not currently. In the interim we recommend periodically fetching from “max(latestBlockNumber) - 2” to “lastFetchedBlockNumber” in regular intervals. Fetching from 2 behind the latest block number ensures you receive full sets of data from each new request.

### Are query results data saved for faster retrieval?
    
Yes!

### How long are the results data from an execution stored for?
    
Currently set to 2 years but we may reduce this to something closer to 90 days in the future. This is visible on the API response on the “expires_at” field in the execution status and results body.

### How much data can I retrieve in a single API result call?
    
There is currently a 250MB limit, but there is a chance we increase this for certain paid plans. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.
