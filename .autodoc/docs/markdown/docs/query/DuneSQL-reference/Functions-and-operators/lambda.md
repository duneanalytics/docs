[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/lambda.md)

# Lambda Expressions

This guide covers the use of lambda expressions in the Dune Docs project. Lambda expressions are anonymous functions that are passed as arguments to higher-order SQL functions. They are written with `->`. The guide provides examples of lambda expressions and their limitations. Most SQL expressions can be used in a lambda body, with the exception of subqueries and aggregations.

The guide provides examples of how to use lambda expressions in the Dune Docs project. The `transform` function can be used to obtain the squared elements of an array column or to safely cast the elements of an array to strings. Other columns can be captured as well within the lambda expression. The `any_match` function can be used to find the array elements containing at least one value greater than `100`. The `regexp_replace` function can be used to capitalize the first letter of a string.

Lambda expressions can also be applied in aggregation functions. The guide provides an example of the calculation of the sum of all elements of a column by making use of `reduce_agg`.

Overall, this guide provides a comprehensive overview of the use of lambda expressions in the Dune Docs project. It covers the syntax of lambda expressions, their limitations, and provides examples of their use in various functions.
## Questions: 
 1. What are lambda expressions in the context of this app and how are they used with SQL functions?
- Lambda expressions are anonymous functions that are passed as arguments to higher-order SQL functions, and they are written with `->`. They can be used to manipulate array columns, cast elements to strings, and perform various calculations.

2. What are the limitations of using lambda expressions in SQL?
- Subqueries and aggregations are not supported in lambda bodies.

3. Can lambda expressions be used in aggregation functions, and if so, how?
- Yes, lambda expressions can be applied in aggregation functions such as `reduce_agg`, which can be used to calculate the sum of all elements in a column.