---
title: Cancel Execution
description: Here's how to cancel your Dune API execution requests.
---

# [POST] Cancel Execution

Here's how to cancel your Dune API execution requests.

## Arguments

None.

## Returns

Returns a boolean for whether the execution is successfully canceled.

## Example Request

You need to pass the `execution_id` you obtained from making a [Execute Query ID POST](execute-query-id.md) request to the complete a Cancel Execution API request.

```
POST v1/execution/{{execution_id}}/cancel

https://api.dune.com/api/v1/execution/{{execution_id}}/cancel
```

### cURL

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/execution/{{execution_id}}/cancel"
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

```json
{
    "success": true
}
```

 - *success* : A boolean, indicating whether the request to cancel the query execution was made successfully.