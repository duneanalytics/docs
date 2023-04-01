[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/conversion.md)

# Conversions

This section of the app technical guide for the Dune Docs project covers how Trino implicitly converts numeric and character values to the correct type if such a conversion is possible. However, Trino will not convert between character and numeric types. For example, a query that expects a varchar will not automatically convert a bigint value to an equivalent varchar. When necessary, values can be explicitly cast to a particular type.

The section also covers conversion functions, which include `cast()` and `try_cast()`. The `cast()` function explicitly casts a value as a type. This can be used to cast a varchar to a numeric value type and vice versa. The `try_cast()` function is like `cast()`, but returns null if the cast fails.

The Formatting section covers the `format()` and `format_number()` functions. The `format()` function returns a formatted string using the specified format string and arguments. The format string follows the syntax specified in the Java documentation. The `format_number()` function returns a formatted string using a unit symbol.

The Miscellaneous section covers the `typeof()` function, which returns the name of the type of the provided expression. Examples of expressions include integers, strings, and doubles.

Overall, this section of the app technical guide provides information on how to convert values between different types and how to format values in a specific way. The guide also provides examples of how to use each function.
## Questions: 
 1. What is the purpose of the Dune Docs project?
- The app technical guide does not provide information on the purpose of the Dune Docs project.

2. Does the app use any blockchain technology?
- The app technical guide does not provide information on whether the app uses any blockchain technology.

3. How does the app handle data storage and retrieval?
- The app technical guide does not provide information on how the app handles data storage and retrieval.