---
title: Latest Results
description: Here"s how to get the latest results of a query run
---

# [GET] query/{query_id}/results

Here"s how to get the latest results of a query, regardless of the job id/run. 

## Arguments

`query_id` is the id of the query you are trying to pull results from. It must either be public or a query you have ownership of. 

For query params, we recommend you to not have spaces for a parameter, use underscore instead like `https://api.dune.com/api/v1/query/2340912/results?params.LooksRare%20Wash%20Trading%20Filter=ON`. If no query params provided, will fetch latest results regardless of parameter (not just default!)

## Returns

Returns the latest execution id and results of the run. 

Note that: 
- this endpoint does NOT trigger execution 
- you only need to pass the id in then you get latest results that was executed 
- only get the latest execution triggered thru APP (API execution results will be included soon)


## Example Request

You need to pass the `query_id` like below:

```
GET v1/execution/{{execution_id}}/status

https://api.dune.com/api/v1/query/{{query_id}}/results
```

### cURL

```
curl -X GET "https://api.dune.com/api/v1/execution/{{execution_id}}/status" -H x-dune-api-key:{{api_key}}
```

### Python

```
import dotenv
import os
import json
import requests
import pandas as pd
import time

api_key = os.environ["DUNE_API_KEY"]

# authentiction with api key
headers = {"x-dune-api-key": api_key}

query_id = 1252207
base_url = f"https://api.dune.com/api/v1/query/{query_id}/results"
params = {
    "params.LooksRare Wash Trading Filter": "ON", # one and only param for this query, "ON" value has been executed
}
result_response = requests.request("GET", base_url, headers=headers, params=params)
```

## Example Response

!!! info "Dune API responses are delivered in JSON format."

```json
{"execution_id": "01GXDTYMM2CKFRBEW44X5S0WZE",
 "query_id": 1252207,
 "state": "QUERY_STATE_COMPLETED",
 "submitted_at": "2023-04-07T12:27:09.314513Z",
 "expires_at": "2025-04-06T12:27:15.749155Z",
 "execution_started_at": "2023-04-07T12:27:09.387366Z",
 "execution_ended_at": "2023-04-07T12:27:15.749154Z",
 "result": {"rows": [
    {"24 Hours Volume": 10501366.303435229,
    "7 Days Volume": 83500570.47565666,
    "Rank": 1,
    "Total Volume": 35184444503.17035,
    "project": "opensea"},
   {"24 Hours Volume": 2905815.0342120747,
    "7 Days Volume": 34792342.84606525,
    "Rank": 2,
    "Total Volume": 4897580325.593282,
    "project": "x2y2"},
   {"24 Hours Volume": 21859216.193396263,
    "7 Days Volume": 256722523.89635494,
    "Rank": 3,
    "Total Volume": 4037590713.6422567,
    "project": "blur"}
    ],
   "result_set_bytes": 1524,
   "total_row_count": 26,
   "datapoint_count": 135,
   "pending_time_millis": 72,
   "execution_time_millis": 6361}
}
```