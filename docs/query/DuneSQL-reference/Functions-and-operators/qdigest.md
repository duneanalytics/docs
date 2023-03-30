---
title: Quantile digest functions
---

# Data structures

A quantile digest is a data sketch which stores approximate percentile
information. The Trino type for this data structure is called `qdigest`,
and it takes a parameter which must be one of `bigint`, `double` or
`real` which represent the set of numbers that may be ingested by the
`qdigest`. They may be merged without losing precision, and for storage
and retrieval they may be cast to/from `VARBINARY`.

## Functions

#### merge()
**``merge(qdigest)``** → qdigest

Merges all input `qdigest`s into a single `qdigest`.

#### values_at_quantile()
**``value_at_quantile(qdigest(T), quantile)``** → T

Returns the approximate percentile value from the quantile digest given
the number `quantile` between 0 and 1.

#### values_at_quantiles()
**``values_at_quantiles(qdigest(T), quantiles)``** → array(T)

Returns the approximate percentile values as an array given the input
quantile digest and array of values between 0 and 1 which represent the
quantiles to return.

#### qdigest_agg()
**``qdigest_agg(x)``** → qdigest(same as x)

Returns the `qdigest` which is composed of all input values of `x`.

#### qdigest_agg()
**``qdigest_agg(x, w)``** → qdigest(same as x)

Returns the `qdigest` which is composed of all input values of `x` using
the per-item weight `w`.

#### qdigest_agg()
**``qdigest_agg(x, w, accuracy)``** → qdigest(same as x)

Returns the `qdigest` which is composed of all input values of `x` using
the per-item weight `w` and maximum error of `accuracy`. `accuracy` must
be a value greater than zero and less than one, and it must be constant
for all input rows.
