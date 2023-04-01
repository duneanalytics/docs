[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/qdigest.md)

# Quantile Digest Functions

This technical guide covers the implementation of quantile digest functions in the Dune Docs project. A quantile digest is a data sketch that stores approximate percentile information. The Trino type for this data structure is called `qdigest`. The guide explains the data structures and functions used in the implementation of quantile digest functions.

## Data Structures

The `qdigest` data structure takes a parameter that must be one of `bigint`, `double`, or `real`, which represent the set of numbers that may be ingested by the `qdigest`. They may be merged without losing precision, and for storage and retrieval, they may be cast to/from `VARBINARY`.

## Functions

The guide explains the following functions used in the implementation of quantile digest functions:

### merge()

**``merge(qdigest)``** → qdigest

Merges all input `qdigest`s into a single `qdigest`.

### values_at_quantile()

**``value_at_quantile(qdigest(T), quantile)``** → T

Returns the approximate percentile value from the quantile digest given the number `quantile` between 0 and 1.

### values_at_quantiles()

**``values_at_quantiles(qdigest(T), quantiles)``** → array(T)

Returns the approximate percentile values as an array given the input quantile digest and array of values between 0 and 1 which represent the quantiles to return.

### qdigest_agg()

**``qdigest_agg(x)``** → qdigest(same as x)

Returns the `qdigest` which is composed of all input values of `x`.

**``qdigest_agg(x, w)``** → qdigest(same as x)**

Returns the `qdigest` which is composed of all input values of `x` using the per-item weight `w`.

**``qdigest_agg(x, w, accuracy)``** → qdigest(same as x)**

Returns the `qdigest` which is composed of all input values of `x` using the per-item weight `w` and maximum error of `accuracy`. `accuracy` must be a value greater than zero and less than one, and it must be constant for all input rows.

In summary, this guide provides an overview of the data structures and functions used in the implementation of quantile digest functions in the Dune Docs project. It explains the purpose of each function and how it applies to the project app. The guide also provides examples of the usage of each function.
## Questions: 
 1. What is the purpose of the dune docs app and how does it relate to blockchain technology?
- The app technical guide does not provide information on the purpose of the dune docs app or its relation to blockchain technology, so a blockchain SQL analyst may need to seek additional information from other sources.

2. Can the `qdigest` data structure be used to store and retrieve data from a blockchain database?
- The app technical guide does not provide information on whether the `qdigest` data structure can be used with a blockchain database, so a blockchain SQL analyst may need to experiment with the data structure or consult with other experts in the field.

3. What is the maximum error of `accuracy` in the `qdigest_agg()` function and how does it affect the precision of the results?
- The app technical guide states that `accuracy` must be a value greater than zero and less than one, but it does not provide information on how this value affects the precision of the results, so a blockchain SQL analyst may need to conduct further research or experimentation to determine the optimal value for their use case.