[View code on GitHub](https://dune.com/docs/data-tables/community/reservoir/attribute-keys.md)

## Attribute Keys

The `attribute_keys` section of the app technical guide provides information about the `reservoir.attribute_keys` table. This table contains records with information about each attribute key. The table has seven columns: `id`, `collection_id`, `key`, `kind`, `rank`, `created_at`, and `updated_at`. 

- `id`: This is the internal attribute key id.
- `collection_id`: This is the associated collection id.
- `key`: This is the name of the attribute.
- `kind`: This is the value type, which can be string, number, date, or range.
- `rank`: This is the sort order.
- `created_at`: This is the timestamp the attribute key was created.
- `updated_at`: This is the timestamp the attribute key was updated.

The guide also provides a link to query examples for the `reservoir.attribute_keys` table. The link leads to a page on the Dune website that provides examples of queries that can be run on the table. 

Overall, this section of the guide is useful for developers who need to work with the `reservoir.attribute_keys` table in the Dune app. It provides a clear understanding of the table's structure and contents, as well as examples of how to query the table.
## Questions: 
 1. What is the purpose of the `reservoir.attribute_keys` table in the context of the dune docs app? 
   - The `reservoir.attribute_keys` table contains information about each attribute key in the app, including its name, type, and associated collection.
2. How are attribute keys sorted in the `reservoir.attribute_keys` table? 
   - Attribute keys are sorted by their `rank` column in the `reservoir.attribute_keys` table.
3. Are there any examples of queries that can be run using the `reservoir.attribute_keys` table? 
   - Yes, query examples can be found at the URL provided in the app technical guide: [https://dune.com/queries/1302930/2232305](https://dune.com/queries/1302930/2232305).