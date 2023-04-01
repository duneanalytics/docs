[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/tdigest.md)

# T-Digest Functions

This technical guide covers the T-Digest functions in the Dune Docs project. A T-Digest is a data sketch that stores approximate percentile information. The Trino type for this data structure is called `tdigest`. T-Digests can be merged, and for storage and retrieval, they can be cast to and from `VARBINARY`.

## Data Structures

This section explains the T-Digest data structure and its usage in the project. It provides information on how to store and retrieve T-Digests using `VARBINARY`.

## Functions

This section covers the T-Digest functions available in the project. It explains the purpose of each function and how to use it. The functions covered in this guide are:

### merge()

This function aggregates all inputs into a single `tdigest`.

Example: `merge(tdigest)`

### values_at_quantile()

This function returns the approximate percentile value from the T-Digest, given the number `quantile` between 0 and 1.

Example: `value_at_quantile(tdigest, quantile)`

### values_at_quantiles()

This function returns the approximate percentile values as an array, given the input T-Digest and an array of values between 0 and 1, which represent the quantiles to return.

Example: `values_at_quantiles(tdigest, quantiles)`

### tdigest_agg()

This function composes all input values of `x` into a `tdigest`. `x` can be of any numeric type.

Example: `tdigest_agg(x)`

This function also composes all input values of `x` into a `tdigest` using the per-item weight `w`. `w` must be greater or equal to 1. `x` and `w` can be of any numeric type.

Example: `tdigest_agg(x, w)`

Overall, this guide provides a clear understanding of the T-Digest functions available in the Dune Docs project and how to use them.
## Questions: 
 1. What is the purpose of the T-digest data structure and how is it used in this app?
   
   The T-digest data structure is used to store approximate percentile information and can be merged and cast to and from `VARBINARY`. It is used in this app to perform functions such as `merge()`, `value_at_quantile()`, `values_at_quantiles()`, and `tdigest_agg()`.

2. What types of numeric input values are accepted by the `tdigest_agg()` function?
   
   The `tdigest_agg()` function can accept input values of any numeric type.

3. Can the `values_at_quantiles()` function return percentile values outside of the range of 0 to 1?
   
   No, the `values_at_quantiles()` function only returns approximate percentile values as an array, given the input T-digest and an array of values between 0 and 1, which represent the quantiles to return.