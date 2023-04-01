[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/teradata.md)

# Teradata Functions

This technical guide provides compatibility with Teradata SQL. It is divided into two sections: String functions and Date functions.

## String Functions

This section contains two functions:

### char2()

**``char2hexint(string)``** → varchar

This function returns the hexadecimal representation of the UTF-16BE encoding of the string.

### index()

**``index(string, substring)``** → bigint

This function is an alias for the `strpos` function.

## Date Functions

This section contains three functions that use a format string that is compatible with the Teradata datetime functions. The following table describes the supported format specifiers:

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

### to_char()

**``to_char(timestamp, format)``** → varchar

This function formats `timestamp` as a string using `format`.

### to_timestamp()

**``to_timestamp(string, format)``** → timestamp

This function parses `string` into a `TIMESTAMP` using `format`.

### to_date()

**``to_date(string, format)``** → date

This function parses `string` into a `DATE` using `format`.

The purpose of this guide is to provide a reference for developers who need to use Teradata functions in their SQL queries. The guide explains the syntax and usage of each function, and provides examples of how to use them. The guide is organized into two sections: String functions and Date functions. The String functions section contains two functions: `char2()` and `index()`. The Date functions section contains three functions: `to_char()`, `to_timestamp()`, and `to_date()`. Each function is described in detail, including its input parameters and return type. The guide also provides a table of format specifiers that are used by the Date functions.
## Questions: 
 1. What is the purpose of the app "dune docs" and how does it relate to blockchain technology?
    
    The app technical guide does not provide information on the purpose of "dune docs" or its relation to blockchain technology.

2. Are there any specific date or time functions that are relevant for blockchain data analysis?
    
    The app technical guide provides date and time functions that are compatible with Teradata SQL, but it does not specify if any of these functions are relevant for blockchain data analysis.

3. Does the app support any functions for working with JSON data?
    
    The app technical guide does not provide information on whether or not the app supports functions for working with JSON data.