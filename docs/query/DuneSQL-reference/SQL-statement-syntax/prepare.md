# PREPARE

## Synopsis

``` text
PREPARE statement_name FROM statement
```

## Description

Prepares a statement for execution at a later time. Prepared statements
are queries that are saved in a session with a given name. The statement
can include parameters in place of literals to be replaced at execution
time. Parameters are represented by question marks.

## Examples

Prepare a select query:

    PREPARE my_select1 FROM
    SELECT * FROM nation;

Prepare a select query that includes parameters. The values to compare
with `regionkey` and `nationkey` will be filled in with the
`execute`{.interpreted-text role="doc"} statement:

    PREPARE my_select2 FROM
    SELECT name FROM nation WHERE regionkey = ? AND nationkey < ?;

Prepare an insert query:

    PREPARE my_insert FROM
    INSERT INTO cities VALUES (1, 'San Francisco');

## See also

`execute`{.interpreted-text role="doc"},
`deallocate-prepare`{.interpreted-text role="doc"},
`describe-input`{.interpreted-text role="doc"},
`describe-output`{.interpreted-text role="doc"}
