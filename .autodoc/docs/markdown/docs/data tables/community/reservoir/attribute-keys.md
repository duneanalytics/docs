[View code on GitHub](https://dune.com/blob/master/data tables\community\reservoir\attribute-keys.md)

# Attribute Keys

This section of the app technical guide covers the `reservoir.attribute_keys` table, which contains records with information about each attribute key. The table has seven columns, including `id`, `collection_id`, `key`, `kind`, `rank`, `created_at`, and `updated_at`. 

- `id`: This column contains the internal attribute key id.
- `collection_id`: This column contains the associated collection id.
- `key`: This column contains the name of the attribute.
- `kind`: This column contains the value type, which can be string, number, date, or range.
- `rank`: This column contains the sort order.
- `created_at`: This column contains the timestamp the attribute key was created.
- `updated_at`: This column contains the timestamp the attribute key was updated.

The purpose of this section is to provide developers with an understanding of the structure and content of the `reservoir.attribute_keys` table. It also includes a link to query examples that can be used to retrieve data from the table.

For example, if a developer wants to retrieve all the attribute keys associated with a specific collection, they can use the following query:

```
SELECT *
FROM reservoir.attribute_keys
WHERE collection_id = 'collection_id_value';
```

Overall, this section of the app technical guide is essential for developers who are working with the `reservoir.attribute_keys` table and need to understand its structure and contents.
## Questions: 
 1. What is the purpose of the `reservoir.attribute_keys` table in the context of the Dune Docs project?
- The `reservoir.attribute_keys` table contains information about each attribute key in the project, including its name, value type, and sort order.

2. How does the `reservoir.attribute_keys` table relate to blockchain technology?
- It is unclear from the provided information how the `reservoir.attribute_keys` table specifically relates to blockchain technology.

3. Are there any security considerations or best practices that should be followed when working with the `reservoir.attribute_keys` table?
- It is unclear from the provided information whether there are any security considerations or best practices that should be followed when working with the `reservoir.attribute_keys` table.