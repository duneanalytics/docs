---
title: Execution Results
description: Here's how to get the results data of an execution request.
---

# [GET] Execution Results

Here's how to get the results data of an execution request.

## Arguments

None.

## Returns

Returns back the status, metadata, and query results from a query execution.

## Example Request

You need to pass the `execution_id` you obtained from making a [Execute Query ID POST](execute-query-id.md) request to the complete an Execution Results API request.

```
GET v1/execution/{{execution_id}}/results

https://api.dune.com/api/v1/execution/{{execution_id}}/results
```

### cURL

```
curl -X GET "https://api.dune.com/api/v1/execution/{{execution_id}}/results" -H x-dune-api-key:{{api_key}}
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_COMPLETED",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "2024-08-28T06:36:41.58847Z",
    "execution_started_at": "2022-08-29T06:33:24.916543Z",
    "execution_ended_at": "2022-08-29T06:36:41.588467Z",
    "result": {
        "rows": [
            {
                "TableName": "eth_blocks",
                "ct": 6296
            },
            {
                "TableName": "eth_traces",
                "ct": 4474223
            },
            {
                "TableName": "eth_creation_traces",
                "ct": 10155
            },
            {
                "TableName": "eth_logs",
                "ct": 2137508
            },
            {
                "TableName": "eth_transactions",
                "ct": 1039890
            },
            {
                "TableName": "sol_transactions",
                "ct": 37185158
            },
            {
                "TableName": "bnb_transactions",
                "ct": 2942005
            },
            {
                "TableName": "optimism_transactions",
                "ct": 120973
            }
        ],
        "metadata": {
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
}
```

 - *execution_id* : The execution ID for which this API was called.
 - *query_id* : The ID of the Dune Query executed with this request.
 - *state* : The current state of the query's execution. Check our `FAQ` section to see what different status codes for `state` mean.
 - *submitted_at* : The timestamp at which the API for executing this query was called.
 - *expires_at* : The time upto which results from this query's execution shall be stored in our Database.
 - *execution_started_at* : The time at which query execution started for this request in our servers.
 - *execution_ended_at* : The time at which the query execution for this request got completed in our servers.
 - *result* :
    - *rows* : The actual rows of data being returned for this request.
    - *metadata* : Some properties of the queried data being returned.
        - *column_names* : Names of the columns in the data returned.
        - *result_set_bytes* : The size of the returned data.
        - *total_row_count* : The number of rows in the data.
        - *datapoint_count* : Total number of datapoints returned with this request, should equal to (`total_row_count` x number of columns).
        - *pending_time_millis* : The time (in milliseconds) it took to assign a slot in our server for this request.
        - *execution_time_millis* : The time (in milliseconds) it took for the actual execution of the query with this request.


## Reading Results Data FAQ

### Can I ingest data by getting a direct connection to the database instead?

Not currently. In the interim we recommend periodically fetching from “max(latestBlockNumber) - 2” to “lastFetchedBlockNumber” in regular intervals. Fetching from 2 behind the latest block number ensures you receive full sets of data from each new request.

### Are query results data saved for faster retrieval?

Yes

### How long are the results data from an execution stored for?

Currently set to 2 years but we may reduce this to something closer to 90 days in the future. This is visible on the API response on the “expires_at” field in the execution status and results body.

### How much data can I retrieve in a single API result call?

There is currently a 1GB limit, but there is a chance we reduce this overall or based on varying paid plan types.