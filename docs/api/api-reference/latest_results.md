---
title: Latest Query Results
description: Here"s how to get the latest results of a query run
---

# [GET] Latest Query Results

Here's how to get the latest results of a query, regardless of the job id/run or if it is run in the app or the api.

## Example Request

`query_id` is the id of the query you are trying to pull results from. It must either be public or a query you have ownership of. 

```
GET v1/query/{{query_id}}/results

https://api.dune.com/api/v1/query/{{query_id}}/results
```
## Returns

Returns the latest execution id and results of the run. 

!!!note "Keep in mind"
    - this endpoint does NOT trigger execution but does consume credits through datapoints

    - you only need to pass the id in then you get latest results that was executed 

    - only get the latest execution triggered thru APP (API execution results will be included soon)
## Query Parameters

For query params, we recommend you to not have spaces for a parameter, use underscore instead like `https://api.dune.com/api/v1/query/2340912/results?params.LooksRare%20Wash%20Trading%20Filter=ON`. If no query params are provided, the request will fetch the latest results regardless of parameter (not just default!)
### cURL

```
curl -X GET "https://api.dune.com/api/v1/query/{{query_id}}/results" -H x-dune-api-key:{{api_key}}
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
    "params.LooksRare Wash Trading Filter": "ON", # one and only param for this query
}
result_response = requests.request("GET", base_url, headers=headers, params=params)
```

You can partially fill parameters as well, say there are three parameters - if you only pass in two then the other one will use the default parameters:

```
# case 4: partial match of the existing params that were executed will work aka 200
query_id = 1064888
base_url = f"https://api.dune.com/api/v1/query/{query_id}/results"
params = {
    "params.Show Today": "No",
    "params.Time Period": "day" 
    # there is one more param for this query "Trailing Num Periods" which we are not passing
}
result_response = requests.request("GET", base_url, headers=headers, params=params)
```

!!! warning "Parameter 404 Behaviors"
    If a certain parameter has never been run before, i.e. putting in "OFF" above when only "ON" has been executed in app, then you will get a 404. Same thing if you try and use a parameter that doesn't exist on the query.


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
