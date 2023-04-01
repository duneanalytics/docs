[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/alter-table.md)

# ALTER TABLE

## Synopsis

The `ALTER TABLE` statement is used to change the definition of an existing table. The statement can be used to rename a table, add or drop a column, rename a column, change the data type of a column, set authorization, set properties, and execute a command. 

## Description

The `ALTER TABLE` statement has several clauses that can be used to modify a table. The `IF EXISTS` clause can be used before the table name or column name to suppress errors if the table or column does not exist. The `IF NOT EXISTS` clause can be used before the column name to suppress errors if the column already exists. 

The `SET PROPERTIES` clause can be used to apply specified properties and values to a table. The statement can be used to set a property to `DEFAULT`, which reverts its value back to the default in that table. However, support for `ALTER TABLE SET PROPERTIES` varies between connectors, as not all connectors support modifying table properties.

The `EXECUTE` clause can be used to modify the table according to the specified command and parameters. The `=>` operator can be used for passing named parameter values. The left side is the name of the parameter, the right side is the value being passed.

## Examples

The following are examples of how to use the `ALTER TABLE` statement:

- Rename table `users` to `people`: `ALTER TABLE users RENAME TO people;`
- Rename table `users` to `people` if table `users` exists: `ALTER TABLE IF EXISTS users RENAME TO people;`
- Add column `zip` to the `users` table: `ALTER TABLE users ADD COLUMN zip varchar;`
- Add column `zip` to the `users` table if table `users` exists and column `zip` not already exists: `ALTER TABLE IF EXISTS users ADD COLUMN IF NOT EXISTS zip varchar;`
- Drop column `zip` from the `users` table: `ALTER TABLE users DROP COLUMN zip;`
- Drop column `zip` from the `users` table if table `users` and column `zip` exists: `ALTER TABLE IF EXISTS users DROP COLUMN IF EXISTS zip;`
- Rename column `id` to `user_id` in the `users` table: `ALTER TABLE users RENAME COLUMN id TO user_id;`
- Rename column `id` to `user_id` in the `users` table if table `users` and column `id` exists: `ALTER TABLE IF EXISTS users RENAME column IF EXISTS id to user_id;`
- Change type of column `id` to `bigint` in the `users` table: `ALTER TABLE users ALTER COLUMN id SET DATA TYPE bigint;`
- Change owner of table `people` to user `alice`: `ALTER TABLE people SET AUTHORIZATION alice`
- Allow everyone with role public to drop and alter table `people`: `ALTER TABLE people SET AUTHORIZATION ROLE PUBLIC`
- Set table properties (`x = y`) in table `people`: `ALTER TABLE people SET PROPERTIES x = 'y';`
- Set multiple table properties (`foo = 123` and `foo bar = 456`) in table `people`: `ALTER TABLE people SET PROPERTIES foo = 123, "foo bar" = 456;`
- Set table property `x` to its default value in table`people`: `ALTER TABLE people SET PROPERTIES x = DEFAULT;`
- Collapse files in a table that are over 10 megabytes in size, as supported by the Hive connector: `ALTER TABLE hive.schema.test_table EXECUTE optimize(file_size_threshold => '10MB')`

## See also

`create-table`
## Questions: 
 1. What is the purpose of the `SET PROPERTIES` statement in the `ALTER TABLE` command?
   
   The `SET PROPERTIES` statement in the `ALTER TABLE` command is used to apply specified properties and values to a table. It can be used to change the default value of a property back to the default in that table.

2. What is the purpose of the `EXECUTE` statement in the `ALTER TABLE` command?
   
   The `EXECUTE` statement in the `ALTER TABLE` command is used to modify the table according to the specified command and parameters. It supports different commands on a per-connector basis.

3. Which connectors support the `ALTER TABLE SET PROPERTIES` statement?
   
   Support for `ALTER TABLE SET PROPERTIES` varies between connectors, as not all connectors support modifying table properties.