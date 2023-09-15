---
title: Export Data Out of Dune
description: How to export data out of Dune
---

This guide provides a step-by-step process on exporting data from Dune, either through CSV downloads or the API.

## Identify the Dataset for Export

Begin by pinpointing the dataset or query result you wish to export. For instance, given the recent buzz around Friend.Tech, you might want to export the results from this query: https://dune.com/queries/2945343.

## Export via CSV

- Navigate to the query interface.
- Simply click the "Export to CSV" button.

<div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/ZGmdSGBEqRwUpopdF4RR?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Export via CSV"></iframe></div>

## Export via API

Ensure you have an API key. If not, generate one:

1. Navigate to: Settings → API.
2. Click on "Create new API key".
3. Remember to copy the entire API key before confirming.

<div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/f07eudjtOJz9URF8TGa5?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="how to generate API key"></iframe></div>

For this guide, we'll focus on exporting data using the ['get latest query result'](../../../api/api-reference/get-results/latest-results) endpoint. Here's a Python example:

!!! note 
    First, create a .env file with the API key you just created.
    ```
    DUNE_API_KEY= <insert your key>
    ```

```py

import dotenv
import os
import json
import requests
import pandas as pd

def get_latest_query_result(query_id):
    res_df = pd.DataFrame()
    try:
        result_url = f"https://api.dune.com/api/v1/query/{query_id}/results"
        result_response = requests.get(result_url, headers=headers)
        print(json.loads(result_response.text))
        query_res = json.loads(result_response.text)["result"]["rows"]
        res_df = pd.DataFrame.from_dict(query_res)
    except Exception as e:
        print(f"Error retrieving result for query {query_id}: {e}")
    return res_df

dotenv.load_dotenv('path_to_env_file')  # Replace 'path_to_env_file' with your .env file path
api_key = os.getenv("DUNE_API_KEY")
query_id = 2945343
headers = {"x-dune-api-key": api_key}
latest_res = get_latest_query_result(query_id)
print(latest_res)

```

There are multiple methods to export data via the API, and it's possible to get data in various formats like JSON and CSV. You can even integrate the data with Google Sheets. For a comprehensive guide, refer to [this page](../../../api/api-reference/get-results/).

!!! tip 
    Access the 'get latest result' endpoint directly from the Dune UI. When viewing a query, click the API icon in the top-right corner and copy the endpoint URL.
    
    <div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/8B1oBaaI9LjLubSVjjc9?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Easy access to API data export"></iframe></div>