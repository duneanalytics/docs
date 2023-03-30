---
title: T-Digest functions
---

## Data structures

A T-digest is a data sketch which stores approximate percentile
information. The Trino type for this data structure is called `tdigest`.
T-digests can be merged, and for storage and retrieval they can be cast
to and from `VARBINARY`.

## Functions

#### merge()
**``merge(tdigest)``** → tdigest

Aggregates all inputs into a single `tdigest`.

#### values_at_quantile()
**``value_at_quantile(tdigest, quantile)``** → double

Returns the approximate percentile value from the T-digest, given the number `quantile` between 0 and 1.

#### values_at_quantiles()
**``values_at_quantiles(tdigest, quantiles)``** → array(double)

Returns the approximate percentile values as an array, given the input T-digest and an array of values between 0 and 1, which represent the quantiles to return.

#### tdigest_agg()
**``tdigest_agg(x)``** → tdigest

Composes all input values of `x` into a `tdigest`. `x` can be of any numeric type.


**``tdigest_agg(x, w)``** → tdigest

Composes all input values of `x` into a `tdigest` using the per-item weight `w`. `w` must be greater or equal than 1. `x` and `w` can be of any numeric type.
