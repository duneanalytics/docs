# SHOW SESSION

## Synopsis

``` text
SHOW SESSION [ LIKE pattern ]
```

## Description

List the current
`session properties <session-properties-definition>`{.interpreted-text
role="ref"}.

`Specify a pattern <like_operator>`{.interpreted-text role="ref"} in the
optional `LIKE` clause to filter the results to the desired subset. For
example, the following query allows you to find session properties that
begin with `query`:

    SHOW SESSION LIKE 'query%'

## See also

`reset-session`{.interpreted-text role="doc"},
`set-session`{.interpreted-text role="doc"}
