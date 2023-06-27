---
title: API
description: Discover how Dune API seamlessly enhances your data integration workflow, turbocharging your efficiency.
---

**The Dune API simplifies your data integration worflow and turbocharges your efficiency!** 

Dune API is your solution for data infrastructure and workflow management, enabling you to create API endpoints, run queries, and manage them systematically across 12 chains and 700,000+ data tables, thereby unlocking its full potential.

### API Reference

Check out full documentation regarding API features and endpoints [here](api-reference/index.md).

### Obtaining an API Key
All plans on our new [credit-based pricing system](https://dune.com/pricing) come bundled with API access.
You'll have seperate API keys for your [individual accounts](https://dune.com/settings/api) and [team accounts](https://dune.com/settings/teams).

### API Quickstart Guides

!!!note
    The quickstart and community SDKs currently only contains endpoints under [Executing Queries](../api-reference/execute-queries) and [Getting Results](../api-reference/get-results). We will be adding info regarding newer endpoints under [Editing Queries](../api-reference/edit-queries) soon.

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

### Additional Info

💭 If you have any questions or feedback, please reach out to our #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) Discord channel or [api-feedback@dune.com](mailto:api-feedback@dune.com)!

💡 Have an idea for additional Dune API features? Please [submit them here](https://feedback.dune.com/)! We value your input and are regularly implementing improvements based on user feedback.