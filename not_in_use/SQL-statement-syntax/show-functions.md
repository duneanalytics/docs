# SHOW FUNCTIONS

## Synopsis

``` text
SHOW FUNCTIONS [ LIKE pattern ]
```

## Description

List all the functions available for use in queries. For each function
returned, the following information is displayed:

-   Function name
-   Return type
-   Argument types
-   Function type
-   Deterministic
-   Description

`Specify a pattern <like_operator>`{.interpreted-text role="ref"} in the
optional `LIKE` clause to filter the results to the desired subset. For
example, the following query allows you to find functions beginning with
`array`:

    SHOW FUNCTIONS LIKE 'array%';

`SHOW FUNCTIONS` works with built-in functions as well as with `custom
functions </develop/functions>`{.interpreted-text role="doc"}. In the
following example, three custom functions beginning with `cf` are
available:

``` text
SHOW FUNCTIONS LIKE 'cf%';

     Function      | Return Type | Argument Types | Function Type | Deterministic |               Description
 ------------------+-------------+----------------+---------------+---------------+-----------------------------------------
 cf_getgroups      | varchar     |                | scalar        | true          | Returns the current session's groups
 cf_getprincipal   | varchar     |                | scalar        | true          | Returns the current session's principal
 cf_getuser        | varchar     |                | scalar        | true          | Returns the current session's user
```
