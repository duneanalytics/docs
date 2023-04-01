[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/conditional.md)

The app technical guide covers the conditional expressions in SQL. The guide explains the standard SQL `CASE` expression, which has two forms: the "simple" form and the "searched" form. The "simple" form searches each `value` expression from left to right until it finds one that equals `expression`. The `result` for the matching `value` is returned. If no match is found, the `result` from the `ELSE` clause is returned if it exists, otherwise null is returned. The "searched" form evaluates each boolean `condition` from left to right until one is true and returns the matching `result`. If no conditions are true, the `result` from the `ELSE` clause is returned if it exists, otherwise null is returned.

The `IF` expression has two forms, one supplying only a `true_value` and the other supplying both a `true_value` and a `false_value`. The `IF` expression evaluates and returns `true_value` if `condition` is true, otherwise null is returned and `true_value` is not evaluated. The `IF` expression evaluates and returns `true_value` if `condition` is true, otherwise evaluates and returns `false_value`.

The `COALESCE` function returns the first non-null `value` in the argument list. Like a `CASE` expression, arguments are only evaluated if necessary.

The `NULLIF` function returns null if `value1` equals `value2`, otherwise returns `value1`.

The `TRY` function evaluates an expression and handles certain types of errors by returning `NULL`. In cases where it is preferable that queries produce `NULL` or default values instead of failing when corrupt or invalid data is encountered, the `TRY` function may be useful. To specify default values, the `TRY` function can be used in conjunction with the `COALESCE` function. The following errors are handled by `TRY`: Division by zero, Invalid cast or function argument, and Numeric value out of range.

The guide provides examples of each of the conditional expressions and how they can be used in SQL queries.
## Questions: 
 1. What is the purpose of the `TRY` function and how is it used in SQL queries?
    
    The `TRY` function is used to evaluate an expression and handle certain types of errors by returning `NULL`. It can be used in conjunction with the `COALESCE` function to specify default values in cases where queries produce `NULL` or default values instead of failing when corrupt or invalid data is encountered.
    
2. How does the `CASE` expression work in SQL and what are its two forms?
    
    The `CASE` expression in SQL has two forms: the "simple" form and the "searched" form. The "simple" form searches each `value` expression from left to right until it finds one that equals `expression`, while the "searched" form evaluates each boolean `condition` from left to right until one is true and returns the matching `result`.
    
3. What is the purpose of the `COALESCE` function in SQL and how is it used?
    
    The `COALESCE` function in SQL returns the first non-null `value` in the argument list. It is used like a `CASE` expression, where arguments are only evaluated if necessary.