[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/merge.md)

# MERGE

The `MERGE` statement is used to conditionally update and/or delete rows of a table and/or insert new rows into a table. This section of the app technical guide provides a detailed explanation of the `MERGE` statement, including its syntax, description, examples, and limitations.

The `MERGE` statement has the following syntax:

``` text
MERGE INTO target_table [ [ AS ]  target_alias ]
USING { source_table | query } [ [ AS ] source_alias ]
ON search_condition
when_clause [...]
```

where `when_clause` is one of:

``` text
WHEN MATCHED [ AND condition ]
    THEN DELETE
```

``` text
WHEN MATCHED [ AND condition ]
    THEN UPDATE SET ( column = expression [, ...] )
```

``` text
WHEN NOT MATCHED [ AND condition ]
    THEN INSERT [ column_list ] VALUES (expression, ...)
```

The `MERGE` statement supports an arbitrary number of `WHEN` clauses with different `MATCHED` conditions, executing the `DELETE`, `UPDATE`, or `INSERT` operation in the first `WHEN` clause selected by the `MATCHED` state and the match condition.

For each source row, the `WHEN` clauses are processed in order. Only the first matching `WHEN` clause is executed, and subsequent clauses are ignored. A `MERGE_TARGET_ROW_MULTIPLE_MATCHES` exception is raised when a single target table row matches more than one source row.

If a source row is not matched by any `WHEN` clause and there is no `WHEN NOT MATCHED` clause, the source row is ignored.

In `WHEN` clauses with `UPDATE` operations, the column value expressions can depend on any field of the target or the source. In the `NOT MATCHED` case, the `INSERT` expressions can depend on any field of the source.

The examples provided in this section illustrate how to use the `MERGE` statement to delete customers, update purchases, and insert new rows into a table. The examples show how to use the `MERGE` statement with different `WHEN` clauses and match conditions.

The `MERGE` statement has some limitations. Any connector can be used as a source table for a `MERGE` statement. However, only connectors that support the `MERGE` statement can be the target of a merge operation. Refer to the connector documentation for more information.

In summary, the `MERGE` statement is a powerful SQL statement that allows you to conditionally update and/or delete rows of a table and/or insert new rows into a table. The `MERGE` statement supports an arbitrary number of `WHEN` clauses with different `MATCHED` conditions, executing the `DELETE`, `UPDATE`, or `INSERT` operation in the first `WHEN` clause selected by the `MATCHED` state and the match condition. The examples provided in this section illustrate how to use the `MERGE` statement with different `WHEN` clauses and match conditions.
## Questions: 
 1. What is the purpose of the `MERGE` statement in the context of a blockchain SQL database?
- Answer: A blockchain SQL analyst might want to know how the `MERGE` statement can be used to conditionally update, delete, and insert rows in a table, and whether it can be used to modify blockchain data.

2. Are there any limitations to using the `MERGE` statement with blockchain data?
- Answer: A blockchain SQL analyst might want to know if there are any limitations to using the `MERGE` statement with blockchain data, and whether any specific connectors are required.

3. Can the `MERGE` statement be used to modify data in a blockchain network?
- Answer: A blockchain SQL analyst might want to know if the `MERGE` statement can be used to modify data in a blockchain network, and if so, what implications this might have for the integrity and security of the network.