[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/reset-session.md)

# RESET SESSION

## Synopsis

The `RESET SESSION` command is used to reset a session property value to its default value. This command can be used to reset a specific session property or a property within a specific catalog.

## Description

The `RESET SESSION` command is used to reset a session property value to its default value. This command can be used to reset a specific session property or a property within a specific catalog. The syntax for resetting a session property is as follows:

``` text
RESET SESSION name
RESET SESSION catalog.name
```

The first syntax resets a session property to its default value. The second syntax resets a property within a specific catalog to its default value.

## Examples

Here are some examples of how to use the `RESET SESSION` command:

``` sql
RESET SESSION optimize_hash_generation;
RESET SESSION hive.optimized_reader_enabled;
```

The first example resets the `optimize_hash_generation` session property to its default value. The second example resets the `optimized_reader_enabled` property within the `hive` catalog to its default value.

## See also

- `set-session`: This command is used to set the value of a session property.
- `show-session`: This command is used to display the current value of a session property.
## Questions: 
 1. What is the purpose of the `RESET SESSION` command in the context of a blockchain SQL database?
- Answer: A blockchain SQL analyst might want to know how the `RESET SESSION` command can be used to manage session properties in the context of a blockchain database.

2. How does the `RESET SESSION` command interact with other SQL commands commonly used in blockchain databases?
- Answer: A blockchain SQL analyst might want to know how the `RESET SESSION` command can be used in conjunction with other SQL commands to optimize performance or manage data consistency.

3. Are there any security implications to using the `RESET SESSION` command in a blockchain database?
- Answer: A blockchain SQL analyst might want to know if there are any security risks associated with using the `RESET SESSION` command, and if so, how to mitigate them.