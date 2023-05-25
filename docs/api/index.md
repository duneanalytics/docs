---
title: API
description: Welcome to the Dune API
---

# Welcome to the Dune API

![dune API Cover](images/dune-api-banner.png)

The Dune API gives you full access to the queries and data you can see on the Dune website. This means you can execute and read results from any public query, as well as any personal private queries your Dune account has access to.

This documentation describes all of the available API calls and properties of the returned objects. If you have any questions or feedback, please reach out to [api-feedback@dune.com](mailto:api-feedback@dune.com) or our #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) Discord channel!

### Obtaining an API Key
All plans on our new [credit-based pricing system](https://dune.com/pricing) come bundled with API access.
You'll have seperate API keys for your [individual accounts](https://dune.com/settings/api) and [team accounts](https://dune.com/settings/teams).

### API Quickstart Guides

Get started with our API in a few lines of code using these quick start guides:

<div class="cards grid" markdown>
- [Python](quick-start/api-py.md)
- [Javascript](quick-start/api-js.md)
</div>

You should check out our [community API clients (sdks)](quick-start/community-clients.md) as well.

For building a simple data ingestion pipeline, see [using Python and Celery](https://adamparrish.xyz/downstream-data-extract-transform-load).

If you aren't sure what queries to start with, check out the [API-ready query list](quick-start/index.md).

### API Pricing
Pricing for API is charged along two dimensions.

| Dimension | Credits Charged | Relevant API endpoints |
|---|---|---|
| Executions | 10 credits per medium query engine executions (Default)<br>20 credits per large query engine executions | Execute Query |
| Datapoints | 1 credit per 1,000 datapoints | Execution Results<br>Latest Query Results |

A datapoint applies to query results after the query is run, and can in most cases be thought of `rows * columns` with an additional limit of 100 avg bytes per cell in a set of results. This can be expressed as: 
```math
Credits = Datapoints/1000 = max(rows*columns, ceil(totalbytes/100))
```
More details can be found on our [FAQ page](https://dune.com/docs/api/faq/#faq-billing-pricing).

### All API Endpoints

Check out full explanations and documentation of endpoints in the [api endpoint reference](api-reference/index.md).
