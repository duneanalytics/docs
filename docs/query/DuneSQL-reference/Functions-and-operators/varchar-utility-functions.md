# Varchar Utility Functions

Dune SQL offers a series of functions designed to ease some common tasks when working with varchar data.

#### left()
**``left(varchar, bigint)``** → varchar

This function returns the leftmost `x` characters from a string, if `x` is less than or equal to 0 the result is an empty string. The first argument is the original string, and the second argument is `x`, the length of the resulting string.

```sql
SELECT 
    "left"('123456', 2)
```
will return `12`

#### right()
**``right(varchar, bigint)``** → varchar

This function returns the rightmost `x` characters from a string, if `x` is less than or equal to 0 the result is an empty string. The first argument is the original string, and the second argument is `x`, the length of the resulting string.

```sql
SELECT 
    "right"('123456', 2)
```
will return `56`

#### initcap()
**``initcap(varchar)``** → varchar

This function returns a string with the first letter of each word in uppercase and all other letters in lowercase. Words are delimited by white space or characters that are not alphanumeric. The only argument is the original string.

```sql
SELECT 
    "initcap"('hellO woRld')
```
will return `Hello World`