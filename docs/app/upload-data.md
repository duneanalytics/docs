---
title: Upload Data
description: Upload your own data to Dune
---

**Upload your own data to Dune**

This feature allows you to upload any csv file to Dune and query it like any other table in Dune. Currently, the we only supports uploading CSV files with a maximum size of 200 MB. The UI will return an error if the file size exceeds this limit.

For now, all files will be stored in the ``dune_upload`` schema in the Dune database.

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

## How to Upload Data

!!! note
    You can also upload data via the API. Check out the [API documentation](../../api/api-reference/upload-data/) for more information.



<div style="position: relative; padding-bottom: calc(57.550713749060854% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/cDBbbBOiYa42Otpv5j5L?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="Upload data"></iframe></div>

1. Click on the "Upload Data" button in the menu of the Dune UI.
2. Select the csv file you want to upload.
3. Name your table and add a description.
4. Click on save to finish the upload.


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

However, you can use the "query a query" feature to query multiple .csv files at once.

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

## Deleting data

We are currently working on a feature to delete data from Dune. For now, you can contact us at support@dune.com and we will delete the data for you.



