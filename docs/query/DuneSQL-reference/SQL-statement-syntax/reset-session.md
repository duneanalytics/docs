# RESET SESSION

## Synopsis

``` text
RESET SESSION name
RESET SESSION catalog.name
```

## Description

Reset a
`session property <session-properties-definition>`{.interpreted-text
role="ref"} value to the default value.

## Examples

``` sql
RESET SESSION optimize_hash_generation;
RESET SESSION hive.optimized_reader_enabled;
```

## See also

`set-session`{.interpreted-text role="doc"},
`show-session`{.interpreted-text role="doc"}
