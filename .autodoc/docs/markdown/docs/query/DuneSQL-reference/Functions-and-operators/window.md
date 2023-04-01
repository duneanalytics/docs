[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/window.md)

# Window Functions

This section of the app technical guide covers window functions in the Dune Docs project. Window functions are used to perform calculations across rows of the query result. They run after the `HAVING` clause but before the `ORDER BY` clause. Invoking a window function requires special syntax using the `OVER` clause to specify the window. 

The `Window functions` header explains how to specify the window in two ways: by a reference to a named window specification defined in the `WINDOW` clause, or by an in-line window specification which allows defining window components as well as referring to the window components pre-defined in the `WINDOW` clause. 

The `Aggregate functions` header explains that all `aggregate` functions can be used as window functions by adding the `OVER` clause. The aggregate function is computed for each row over the rows within the current row's window frame. 

The `Ranking functions` header explains the different ranking functions available in Dune Docs. These functions include `cume_dist()`, `dense_rank()`, `ntile()`, `percent_rank()`, `rank()`, and `row_number()`. Each function is explained in detail, including its syntax and what it returns. 

The `Value functions` header explains the different value functions available in Dune Docs. These functions include `f_value()`, `last_value()`, `nth_value()`, `lead()`, and `lag()`. Each function is explained in detail, including its syntax and what it returns. 

The guide provides examples for each function to help users understand how to use them in their queries. 

Overall, this guide provides a comprehensive overview of window functions in Dune Docs, including how to specify windows, aggregate functions, ranking functions, and value functions.
## Questions: 
 1. What is the purpose of the `OVER` clause in the window functions?
- The `OVER` clause is used to specify the window for the window functions, which perform calculations across rows of the query result.

2. Can all aggregate functions be used as window functions?
- Yes, all aggregate functions can be used as window functions by adding the `OVER` clause.

3. What is the difference between `rank()` and `dense_rank()`?
- `rank()` produces gaps in the sequence for tie values in the ordering, while `dense_rank()` does not produce gaps for tie values.