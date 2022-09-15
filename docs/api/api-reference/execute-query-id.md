---
title: Execute Query ID
description: Here's how to execute (run) a query to retrieve updated data.
---
# [POST] Execute Query ID

Here's how to execute (run) a query to retrieve updated data.

## Arguments

None required. You may optionally add query parameters.

## Returns

Returns an `execution_id` for the specified request.

## Example Request

```
POST v1/query/{{query_id}}/execute

https://api.dune.com/api/v1/query/{{query_id}}/execute
```

### cURL

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```

#### cURL example with params

```
curl -X POST -d '{"query_parameters": { "param1":24}}' -H x-dune-api-key:{{api_key}}  "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

```json
{
    "execution_id": "01GB1Y2MRA4C9PNQ0EQYVT4K6R",
    "state": "QUERY_STATE_PENDING"
}
```

 - *execution_id* : A unique ID that is generated every time this API is called. You might want to save it to later pass on to other API endpoints.
 - *state* : The current state of the query's execution. Check our `FAQ` section to see what different status codes mean.