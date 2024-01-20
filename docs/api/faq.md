---
title: Dune API FAQ
description: Dune API FAQ
---

!!! Warning
    Our API docs have moved to [here](https://dune.mintlify.app/api-reference/overview/introduction), this reference page will be deprecated soon.


# Dune API FAQ

## FAQ: Functionality

#### How many Requests Per Minute can I make?

The API rate limit currently varies by [subscription plan](https://dune.com/pricing). This is an overall rate limit for any type of API call made. 

#### Are there specified SLAs?

SLAs will be available in the future on Enterprise pricing plans.

#### How do I find a query id?

When navigating to a query, it’s the first number after “/queries/” in the URL. For example in `https://dune.com/queries/241/388`, "241" is the query id.

#### Does the API support Query Parameters?

The API does support Query Parameters!

For Dune Queries that include Parameters, you can pass parameter data as part of the [Execute Query ID endpoint](api-reference/execute-queries/execute-query-id.md)!

Learn more about [building Dune Queries with Parameters here](../app/query-editor/parameters.md).

And learn how to pass parameter data using [cURL here](api-reference/execute-queries/execute-query-id.md#curl-with-parameters) and with [Python here](quick-start/api-py.md#parameterized-queries).

#### What are the performance and overall differences between the Dune API and the Dune web app? What are the differences in what I can query?

There are no major performance differences within a specific performance tier when used through the Dune API or Dune web app.

The Dune API gives you programmatic access to the capabilities and data sets that can already be accessed from the Dune web app.

#### What is the execution timeout limit and can I request a longer limit?

The query execution timeout limit matches the Dune web app - 30 minutes.

#### Which query engine should I use with the API?

We recommend using the API with v2 Dune SQL as we’re slowly deprecating usage and support of the old v1 engine and v2 Spark SQL.

#### What is the difference between the states “Executing” and “Pending”?

Pending means, the execution is waiting for an available execution connection slot.

Executing means the query is currently executing against the database.

#### Can I ingest data by getting a direct connection to the database instead?
    
Not currently. In the interim we recommend periodically fetching from “max(latestBlockNumber) - 2” to “lastFetchedBlockNumber” in regular intervals. Fetching from 2 behind the latest block number ensures you receive full sets of data from each new request.

#### Are query results data saved for faster retrieval?
    
Yes!

#### How long are the results data from an execution stored for?
    
The resutls storage period can be found on the API response on the “expires_at” field in the execution status and results body.

#### How much data can I retrieve in a single API result call?
    
There is currently a ~1GB limit. The API does not currently return an explicit error upon hitting this limit but will instead fail (timeout) when attempting to retrieve the results.

## FAQ: Billing & Pricing
    
#### How will API Billing work with the new Team plans?
Any API usage billing will be based on what account the API key is associated with. If you use your team api key to call a public query belonging to yourself, the billing will be associated to the team (and vice versa).

#### What’s a datapoint?

A datapoint can in most cases be thought of rows * columns with an additional limit of 100 avg bytes per cell in a set of results. This can be expressed as:

Datapoints = max(rows*columns, ceil(totalbytes/100))

#### Any other questions?

💭 If you have any questions or feedback, please reach out to our #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) Discord channel or [api-feedback@dune.com](mailto:api-feedback@dune.com)!

💡 Have an idea for additional Dune API features? Please [submit them here](https://feedback.dune.com/)! We value your input and are regularly implementing improvements based on user feedback.

[Find our API Terms of Service Here](https://dune.com/api-terms)
