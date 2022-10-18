---
title: Execution Status
description: Here's how to check the status of an execution request.
---

# [GET] Execution Status

Here's how to check the status of an execution request.

## Arguments

None.

## Returns

Returns the status of a query execution along with relevant metadata of the results if the execution is completed.

## Example Request

You need to pass the `execution_id` you obtained from making a [Execute Query ID POST](execute-query-id.md) request to the complete an Execution Status API request.

```
GET v1/execution/{{execution_id}}/status

https://api.dune.com/api/v1/execution/{{execution_id}}/status
```

### cURL

```
curl -X GET "https://api.dune.com/api/v1/execution/{{execution_id}}/status" -H x-dune-api-key:{{api_key}}
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

### Query Executing

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_EXECUTING",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "1970-01-01T00:00:00Z",
    "execution_started_at": "2022-08-29T06:33:24.916543331Z"
}
```

### Execution Complete

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_COMPLETED",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "2024-08-28T06:36:41.58847Z",
    "execution_started_at": "2022-08-29T06:33:24.916543Z",
    "execution_ended_at": "2022-08-29T06:36:41.588467Z",
    "result_metadata": {
        "column_names": [
            "ct",
            "TableName"
        ],
        "result_set_bytes": 194,
        "total_row_count": 8,
        "datapoint_count": 16,
        "pending_time_millis": 8,
        "execution_time_millis": 24
    }
}
```

 - *execution_id* : The execution ID with which this API was called.
 - *query_id* : The ID of the Dune Query being executed with this request.
 - *state* : The current state of the query's execution. Check our `FAQ` section to see what different status codes for `state` mean.
 - *submitted_at* : The timestamp at which the API for executing this query was called.
 - *expires_at* : The time upto which results from this query's execution shall be stored in our Database.
 - *execution_started_at* : The time at which execution started for this request in our servers.
 - *execution_ended_at* : The time at which the execution for this request got completed in our servers.
 - *result_metadata* : Some properties of the response data generated with this request.
    - *column_names* : Names of the columns in the response data that is generated for this request.
    - *result_set_bytes* : The size of the response data in bytes
    - *total_row_count* : The number of rows in response data
    - *datapoint_count* : Total number of datapoints returned with this request, should equal to (`total_row_count` x number of columns).
    - *pending_time_millis* : The time (in milliseconds) it took to assign a slot in our server for this request.
    - *execution_time_millis* : The time (in milliseconds) it took for the actual execution of the query with this request.

## Check Execution Status FAQ

### What is the difference between the states “Executing” and “Pending”?

Pending means, the execution is waiting for an available execution connection slot.
Executing means the query is currently executing against the database.

Here is a list of all Status Codes for reference.

   - QUERY_STATE_PENDING  - query execution is waiting for execution slot
   - QUERY_STATE_EXECUTING - query is executing
   - QUERY_STATE_FAILED - execution failed
   - QUERY_STATE_COMPLETED - execution completed successfully
   - QUERY_STATE_CANCELLED - execution cancelled by user
   - QUERY_STATE_EXPIRED - query execution expired, result no longer available