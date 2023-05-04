---
title: Write API
description: The Dune CSV Upload API allows developers to upload CSV files to a specific table in the Dune database.
---

# Dune CSV Upload API


The Dune CSV Upload API allows you to upload CSV files in the Dune database. This API streamlines the process of importing data into the Dune platform and makes allows you to import off-chain data into Dune with ease. You can simply use your usual API key to authenticate with the API and upload your CSV file.

Currently, the API only supports uploading CSV files with a maximum size of 200 MB. The API will return an error if the file size exceeds this limit. 

**All Data uploaded via this API is public and can be accessed by anyone.**



## Authentication

To authenticate with the API, you must include your API key in the request headers. The header should look like this: 

``X-Dune-Api-Key : <your-api-key>``

## Endpoint

The API endpoint for uploading a CSV file is:

```
POST https://api.dune.com/api/v1/table/upload/csv
```

## Request Parameters

The request payload should be a JSON object containing the following fields:

- `namespace`: (string) The schema in the Dune database. This is static for now and should be set to ``dunecat``.
- `table_name`: (string) The target table in the database where the CSV data should be uploaded.
- `description`: (string, optional) A brief description of the uploaded data. Will be displayed in the Dune UI in the future.
- `data`: (string) The content of the CSV file, passed as a string.

## Example Request

```json
{
    "namespace": "dunecat",
    "table_name": "example_table",
    "description": "Sample data for testing",
    "data": "column1,column2\nvalue1,value2\nvalue3,value4"
}
```

## Response

The API will respond with a status code indicating the result of the upload. A successful upload will return a 200 status code. The response body may contain additional information about the result of the request.

## Example Usage

You can test the API with this google colab notebook: 

<div class="cards grid" markdown>
- [:octicons-arrow-right-24: Google Colab Notebook](https://colab.research.google.com/drive/1dJ9xTT5UfyylIUbMg9r-6FSeMD37HoZN?usp=sharing)
</div>

Alternatively, you can use the following Python code to do the same locally:

```py
# This example demonstrates how to use the new API to upload a CSV file
import os
import json
import requests

api_key = '<YOUR_API_KEY>'
csv_file_path = '<CSV_FILE_PATH>'

url = 'https://api.dune.com/api/v1/table/upload/csv'

with open(csv_file_path) as open_file:
    data = open_file.read()
    
    headers = {'X-Dune-Api-Key': api_key}

    payload = {
        "namespace": "dunecat",
        "table_name": "test_name",
        "description": "test_description",
        "data": str(data)
    }
    
    response = requests.post(url, data=json.dumps(payload), headers=headers)

    print('Response status code:', response.status_code)
    print('Response content:', response.content)

```