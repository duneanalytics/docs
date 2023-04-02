# Reserved keywords

The following table lists all of the keywords that are reserved in
DuneSQL, along with their status in the SQL standard. These reserved
keywords must be quoted (using double quotes) in order to be used as an
identifier.

For example to query the transactions table for all transactions from a specific address you would use the following query with `from` in double quotes:   
```sql
Select * from ethereum.transactions 
where "from" = 0xc8ebccc5f5689fa8659d83713341e5ad19349448
```

## Reserved keywords

| Keyword       | SQL:2016  |
| --------------- | --------- |
| `ALTER`         | reserved  |
| `AND`           | reserved  |
| `AS`            | reserved  |
| `BETWEEN`       | reserved  |
| `BY`            | reserved  |
| `CASE`          | reserved  |
| `CAST`          | reserved  |
| `CONSTRAINT`    | reserved  |
| `CREATE`        | reserved  |
| `CROSS`         | reserved  |
| `CUBE`          | reserved  |
| `CURRENT_CATALOG` | reserved |
| `CURRENT_DATE`  | reserved  |
| `CURRENT_PATH`  | reserved  |
| `CURRENT_ROLE`  | reserved  |
| `CURRENT_SCHEMA` | reserved |
| `CURRENT_TIME`  | reserved  |
| `CURRENT_TIMESTAMP` | reserved |
| `CURRENT_USER`  | reserved  |
| `DEALLOCATE`    | reserved  |
| `DELETE`        | reserved  |
| `DESCRIBE`      | reserved  |
| `DISTINCT`      | reserved  |
| `DROP`          | reserved  |
| `ELSE`          | reserved  |
| `END`           | reserved  |
| `ESCAPE`        | reserved  |
| `EXCEPT`        | reserved  |
| `EXECUTE`       | reserved  |
| `EXISTS`        | reserved  |
| `EXTRACT`       | reserved  |
| `FALSE`         | reserved  |
| `FOR`           | reserved  |
| `FROM`          | reserved  |
| `FULL`          | reserved  |
| `GROUP`         | reserved  |
| `GROUPING`      | reserved  |
| `HAVING`        | reserved  |
| `IN`            | reserved  |
| `INNER`         | reserved  |
| `INSERT`        | reserved  |
| `INTERSECT`     | reserved  |
| `INTO`          | reserved  |
| `IS`            | reserved  |
| `JOIN`          | reserved  |
| `JSON_ARRAY`    | reserved  |
| `JSON_EXISTS`   | reserved  |
| `JSON_OBJECT`   | reserved  |
| `JSON_QUERY`    | reserved  |
| `JSON_VALUE`    | reserved  |
| `LEFT`          | reserved  |
| `LIKE`          | reserved  |
| `LISTAGG`       | reserved  |
| `LOCALTIME`     | reserved  |
| `LOCALTIMESTAMP` | reserved |
| `NATURAL`       | reserved  |
| `NORMALIZE`     | reserved  |
| `NOT`           | reserved  |
| `NULL`          | reserved  |
| `ON`            | reserved  |
| `OR`            | reserved  |
| `ORDER`         | reserved  |
| `OUTER`         | reserved  |
| `PREPARE`       | reserved  |
| `RECURSIVE`     | reserved  |
| `RIGHT`         | reserved  |
| `ROLLUP`        | reserved  |
| `SELECT`        | reserved  |
| `SKIP`          | reserved  |
| `TABLE`         | reserved  |
| `THEN`          | reserved  |
| `TRIM`          | reserved  |
| `TRUE`          | reserved  |
| `UESCAPE`       | reserved  |
| `UNION`         | reserved  |
| `UNNEST`        | reserved  |
| `USING`         | reserved  |
| `VALUES`        | reserved  |
| `WHEN`          | reserved  |
| `WHERE`         | reserved  |
| `WITH`          | reserved  |                                
