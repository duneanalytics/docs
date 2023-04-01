[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/insert.md)

## `INSERT` Command

The `INSERT` command is used to add new rows to a table in the Dune Docs project. The syntax for the command is as follows:

``` text
INSERT INTO table_name [ ( column [, ... ] ) ] query
```

The `table_name` parameter specifies the name of the table to insert the new rows into. The optional `column` parameter specifies the columns to insert data into. If the list of column names is specified, they must exactly match the list of columns produced by the query. Each column in the table not present in the column list will be filled with a `null` value. Otherwise, if the list of columns is not specified, the columns produced by the query must exactly match the columns in the table being inserted into.

The `query` parameter specifies the data to insert into the table. This can be a `SELECT` statement or a list of values. 

### Examples

Here are some examples of how to use the `INSERT` command in the Dune Docs project:

- Load additional rows into the `orders` table from the `new_orders` table:

    ``` sql
    INSERT INTO orders
    SELECT * FROM new_orders;
    ```

- Insert a single row into the `cities` table:

    ``` sql
    INSERT INTO cities VALUES (1, 'San Francisco');
    ```

- Insert multiple rows into the `cities` table:

    ``` sql
    INSERT INTO cities VALUES (2, 'San Jose'), (3, 'Oakland');
    ```

- Insert a single row into the `nation` table with the specified column list:

    ``` sql
    INSERT INTO nation (nationkey, name, regionkey, comment)
    VALUES (26, 'POLAND', 3, 'no comment');
    ```

- Insert a row without specifying the `comment` column. That column will be `null`:

    ``` sql
    INSERT INTO nation (nationkey, name, regionkey)
    VALUES (26, 'POLAND', 3);
    ```

### See also

- `values` command: This command is used to insert a single row into a table with a list of values.
## Questions: 
 1. What is the purpose of this app and how does it relate to blockchain technology?
- The app technical guide is for an SQL database tool called dune docs, and there is no explicit mention of blockchain technology. A blockchain SQL analyst might want to know if this tool is specifically designed for use with blockchain databases or if it has any features that are particularly useful for analyzing blockchain data.

2. Are there any security features built into this app to protect against unauthorized access or data breaches?
- The app technical guide does not mention any security features, so a blockchain SQL analyst might want to know if there are any measures in place to ensure the security of sensitive data, especially if the app is being used to analyze blockchain transactions that contain confidential information.

3. Can this app be used to analyze data from multiple blockchain networks or is it limited to a specific blockchain platform?
- The app technical guide does not provide information about which blockchain networks or platforms it is compatible with, so a blockchain SQL analyst might want to know if the app can be used to analyze data from a variety of blockchain networks or if it is limited to a specific platform.