[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/aggregate.md)

The app technical guide covers aggregate functions, which operate on a set of values to compute a single result. It explains how to order and filter during aggregation, and provides examples for each. The guide also lists general aggregate functions, bitwise aggregate functions, map aggregate functions, approximate aggregate functions, statistical aggregate functions, and lambda aggregate functions.

Ordering during aggregation can be specified using an `order-by-clause` within the aggregate function. Filtering during aggregation can be done using the `FILTER` keyword with a `WHERE` clause. Examples are provided for both ordering and filtering.

The guide then lists various aggregate functions, including:

- General aggregate functions like `arbitrary(x)`, `array_agg(x)`, `avg(x)`, `bool_and(boolean)`, `bool_or(boolean)`, `count(x)`, `max(x)`, `min(x)`, and `sum(x)`.
- Bitwise aggregate functions like `bitwise_and_agg(x)` and `bitwise_or_agg(x)`.
- Map aggregate functions like `histogram(x)`, `map_agg(key, value)`, `map_union(x(K,V))`, `map_union_agg(x(K,V))`, `multimap_agg(key, value)`, and `multimap_union(x(K,V))`.
- Approximate aggregate functions like `approx_distinct(x)`, `approx_most_frequent(x, k)`, `approx_percentile(x, percentage)`, `approx_set(x)`, and `numeric_histogram(buckets, value)`.
- Statistical aggregate functions like `corr(x, y)`, `covar_pop(y, x)`, `covar_samp(y, x)`, `kurtosis(x)`, `regr_intercept(y, x)`, `regr_slope(y, x)`, `skewness(x)`, `stddev(x)`, `variance(x)`, and `var_pop(x)`.
- Lambda aggregate functions like `reduce_agg(inputValue T, initialState S, inputFunction(S, T, S), combineFunction(S, S, S))`.

Each function is accompanied by a brief description and its return type.
## Questions: 
 1. **Question:** What is the behavior of aggregate functions when dealing with null values?

   **Answer:** Except for `count`, `count_if`, `max_by`, `min_by`, and `approx_distinct`, all aggregate functions ignore null values and return null for no input rows or when all values are null. For example, `sum` returns null rather than zero, and `avg` does not include null values in the count. The `coalesce` function can be used to convert null into zero.

2. **Question:** How can I specify the ordering of input values for aggregate functions that produce different results depending on the order?

   **Answer:** You can specify the ordering by writing an `order-by-clause` within the aggregate function. For example: `array_agg(x ORDER BY y DESC)` or `array_agg(x ORDER BY x, y, z)`.

3. **Question:** How can I remove rows from aggregation processing based on a condition?

   **Answer:** You can use the `FILTER` keyword with a condition expressed using a `WHERE` clause. This is evaluated for each row before it is used in the aggregation and is supported for all aggregate functions. For example: `aggregate_function(...) FILTER (WHERE <condition>)`.