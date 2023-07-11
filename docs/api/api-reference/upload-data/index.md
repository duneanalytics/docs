---
title: Uploading data
description: The Dune CSV Upload API allows developers to upload CSV files to a specific table in the Dune database.
---

# Dune CSV Upload API

The Dune CSV Upload API allows you to upload CSV files into the Dune database. This API streamlines the process of importing data into the Dune platform and allows you to import off-chain data into Dune with ease. You can simply use your usual API key to authenticate with the API and upload your CSV file.

Currently, the API only supports uploading CSV files with a maximum size of 200 MB. The API will return an error if the file size exceeds this limit. 

For now, all files will be stored in the ``dune_upload`` schema in the Dune database. In the future, we will allow users to specify the schema where the data should be stored. The table name must be specified in the request payload.

You'll be able to query for your data in any query.

```sql
Select * from dune_upload.example_table
```

We automatically infer schemas (=detect datatypes) for all uploaded data. If in doubt, you can check the assumed datatypes in the information schema. 

```sql
SELECT * FROM information_schema.columns 
WHERE table_schema = 'dune_upload' 
AND table_name = 'energy_data';
```

Anything that represents a timestamp is especially tricky for automated systems to detect, if something is not working as intended, try coverting the timestamp to ISO time before uploading and use the applicable TrinoSQL function to convert it back.

**All Data uploaded via this API is public and can be accessed by anyone.**

## How to use the API

The write API allows you to upload any .csv file into Dune. The only limitations are:

- File has to be < 200 MB
- Column names in the table can't start with a special character or digits. 

Below are the specifics of how to work with the API.

### Authentication

To authenticate with the API, you must include your API key in the request headers. The header should look like this: 

``X-Dune-Api-Key : <your-api-key>``

### Endpoint

The API endpoint for uploading a CSV file is:

```
POST https://api.dune.com/api/v1/table/upload/csv
```

### Request Parameters

The request payload should be a JSON object containing the following fields:

- `table_name`: (string) The target table in the database where the CSV data should be uploaded.
- `description`: (string, optional) A brief description of the uploaded data. Will be displayed in the Dune UI in the future.
- `data`: (string) The content of the CSV file, passed as a string.


### Example Request

```json
{
    "table_name": "example_table",
    "description": "Sample data for testing",
    "data": "column1,column2\nvalue1,value2\nvalue3,value4" 
}
```

``"data"`` is simply the raw .csv data in this request. In "real" requests you would probably pass the data to this function inside of your local program instead. It might look something like this: ``"data": str(data)``.  

### Response

The API will respond with a status code indicating the result of the upload. A successful upload will return a 200 status code. The response body may contain additional information about the result of the request.

### Example Usage

You can test the API by forking this google colab notebook and bringing your own API key: 


- [Google Colab Notebook](https://colab.research.google.com/drive/1dJ9xTT5UfyylIUbMg9r-6FSeMD37HoZN?usp=sharing)

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
        "table_name": "example_table",
        "description": "test_description",
        "data": str(data)
    }
    
    response = requests.post(url, data=json.dumps(payload), headers=headers)

    print('Response status code:', response.status_code)
    print('Response content:', response.content)

```


## Querying for the data in Dune

Once the data has been uploaded, you can query it using the following SQL query:

```sql
Select * from dune_upload.example_table
```

to check whether the datatypes are correctly inferred, you can use the following query:

```sql
SELECT * FROM information_schema.columns 
WHERE table_schema = 'dune_upload'
AND table_name = 'example_table';
```

## Updating data

Currently there is no way to update the data of an already existing .csv file.
However, you can simply make a request to the API with the same ``table_name`` and replace the already existing file that way.

Another way to do this would be to use the "query a query" feature to query multiple .csv files at once.

For example:

```sql
--query_2441513

Select * from dune_upload.my_data_upload_2023_04_29

UNION ALL

Select * from dune_upload.my_data_upload_2023_05_05

-- add more as it becomes relevant
```

In your main query, you could then simply refer to this query.

```sql
Select * from ethereum.transactions t
left join query_2441513 q on q.address = t."from"
```

