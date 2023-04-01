# SHOW CATALOGS

## Synopsis

``` text
SHOW CATALOGS [ LIKE pattern ]
```

## Description

List the available catalogs.

`Specify a pattern <like_operator>`{.interpreted-text role="ref"} in the
optional `LIKE` clause to filter the results to the desired subset. For
example, the following query allows you to find catalogs that begin with
`t`:

    SHOW CATALOGS LIKE 't%'
