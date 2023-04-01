[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/string.md)

# String Functions and Operators

This technical guide covers the string operators and functions available in the Dune Docs project. The guide is divided into two sections: string operators and string functions. 

The string operators section describes the `||` operator, which performs concatenation, and the `LIKE` statement, which can be used for pattern matching. 

The string functions section contains a list of functions that can be used to manipulate strings. The functions are divided into two categories: Unicode functions and string functions. 

The Unicode functions include the `normalize()` function, which transforms a string with the specified normalization form, and the `to_utf8()` function, which encodes a string into a UTF-8 varbinary representation. The `from_utf8()` function decodes a UTF-8 encoded string from binary. 

The string functions include the `concat()` function, which returns the concatenation of two or more strings, and the `lower()` function, which converts a string to lowercase. The `replace()` function removes or replaces all instances of a substring in a string. The `trim()` function removes leading and trailing whitespace from a string. 

The guide also includes examples of how to use each function. For example, the `luhn_check()` function tests whether a string of digits is valid according to the Luhn algorithm. 

Note that some functions assume that the input strings contain valid UTF-8 encoded Unicode code points. There are no explicit checks for valid UTF-8, and the functions may return incorrect results on invalid UTF-8. Invalid UTF-8 data can be corrected with `from_utf8()`. Additionally, the functions operate on Unicode code points and not user-visible characters (or grapheme clusters). Some languages combine multiple code points into a single user-perceived character, the basic unit of a writing system for a language, but the functions will treat each code point as a separate unit. 

The guide also notes that the `lower()` and `upper()` functions do not perform locale-sensitive, context-sensitive, or one-to-many mappings required for some languages. Specifically, this will return incorrect results for Lithuanian, Turkish, and Azeri. 

Overall, this guide provides a comprehensive overview of the string operators and functions available in the Dune Docs project, along with examples of how to use each function.
## Questions: 
 1. What is the purpose of the dune docs app?
    
    Answer: The app technical guide does not provide information about the purpose of the dune docs app. 

2. What are the potential issues with using the lower and upper functions for some languages?
    
    Answer: The lower and upper functions do not perform locale-sensitive, context-sensitive, or one-to-many mappings required for some languages. Specifically, this will return incorrect results for Lithuanian, Turkish, and Azeri.

3. What is the purpose of the `luhn_check` function?
    
    Answer: The `luhn_check` function tests whether a `string` of digits is valid according to the Luhn algorithm. This checksum function, also known as `modulo 10` or `mod 10`, is widely applied on credit card numbers and government identification numbers to distinguish valid numbers from mistyped, incorrect numbers.