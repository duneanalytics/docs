[View code on GitHub](https://dune.com/docs/api/FAQ/functionality.md)

# Dune API Functionality

This technical guide provides answers to frequently asked questions about how the Dune API works. The guide is divided into different sections based on the feature of the project app that the file is focused on. 

## General

This section provides general information about the Dune API.

### Requests Per Minute

The API is currently set to a rate limit of 60 requests per minute. However, this will soon be set to match the rate limits specified in the varying API plan tiers.

### SLAs

SLAs will be available in the future on Enterprise pricing plans.

## Executing Queries

This section provides information on how to execute queries using the Dune API.

### Query ID

To find a query ID, navigate to a query, and it's the first number after "/queries/" in the URL. An example is provided in the guide.

### Query Parameters

The API supports query parameters. For Dune Queries that include parameters, you can pass parameter data as part of the Execute Query ID endpoint. The guide provides links to learn more about building Dune Queries with parameters and how to pass parameter data using cURL and Python.

### Performance and Differences

There are no major performance differences or differences in what can be accessed between the Dune API and the Dune web app if both are using the same app plan tier. The Dune API gives you programmatic access to the capabilities and data sets that can already be accessed from the Dune web app.

### Execution Timeout Limit

The query execution timeout limit matches the Dune web app, which is 30 minutes.

### Query Engine

The guide recommends using the API with v2 Dune SQL as the old v1 engine and v2 Spark SQL are slowly being deprecated.

## Check Execution Status

This section provides information on how to check the execution status of a query.

### States

Pending means the execution is waiting for an available execution connection slot, while executing means the query is currently executing against the database.

## Reading Results Data

This section provides information on how to read results data from a query.

### Direct Connection to the Database

Currently, it's not possible to ingest data by getting a direct connection to the database. In the interim, the guide recommends periodically fetching from "max(latestBlockNumber) - 2" to "lastFetchedBlockNumber" in regular intervals.

### Query Results Data

Query results data is saved for faster retrieval.

### Results Data Storage

The results data from an execution is currently stored for two years, but this may be reduced to something closer to 90 days in the future. This is visible on the API response on the "expires_at" field in the execution status and results body.

### Retrieving Data

There is currently a 250MB limit on how much data can be retrieved in a single API result call. However, there is a chance this may increase for certain paid plans. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.
## Questions: 
 1. What is the rate limit for the Dune API and will it change in the future?
- The API is currently set to a rate limit of 60 requests per minute, but it will soon be set to match the rate limits specified in the varying API plan tiers.

2. What is the execution timeout limit for queries and can it be extended?
- The query execution timeout limit matches the Dune web app, which is 30 minutes. It is not mentioned whether it can be extended.

3. Is there a limit to how much data can be retrieved in a single API result call?
- Yes, there is currently a 250MB limit, but there is a chance it may be increased for certain paid plans. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.