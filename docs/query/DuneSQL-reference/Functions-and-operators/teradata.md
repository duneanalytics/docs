---
title: Teradata functions
---

These functions provide compatibility with Teradata SQL.

## String functions

#### char2()
**``char2hexint(string)``** → varchar

Returns the hexadecimal representation of the UTF-16BE encoding of the string.

#### index()
**``index(string, substring)``** → bigint

Alias for `strpos` function.

## Date functions

The functions in this section use a format string that is compatible
with the Teradata datetime functions. The following table, based on the
Teradata reference manual, describes the supported format specifiers:

  | Specifier | Description                   |
|-----------|-------------------------------|
| - / , . ; : | Punctuation characters are ignored |
| dd        | Day of month (1-31)           |
| hh        | Hour of day (1-12)            |
| hh24      | Hour of the day (0-23)        |
| mi        | Minute (0-59)                 |
| mm        | Month (01-12)                 |
| ss        | Second (0-59)                 |
| yyyy      | 4-digit year                  |
| yy        | 2-digit year                  |

!!!warning
    Case insensitivity is not currently supported. All specifiers must be
    lowercase.


#### to_char()
**``to_char(timestamp, format)``** → varchar

Formats `timestamp` as a string using `format`.

#### to_timestamp()
**``to_timestamp(string, format)``** → timestamp

Parses `string` into a `TIMESTAMP` using `format`.

#### to_date()
**``to_date(string, format)``** → date

Parses `string` into a `DATE` using `format`.

