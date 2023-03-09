---
title: Aggregate functions
---

Aggregate functions operate on a set of values to compute a single
result.

Except for `count`{.interpreted-text role="func"},
`count_if`{.interpreted-text role="func"}, `max_by`{.interpreted-text
role="func"}, `min_by`{.interpreted-text role="func"} and
`approx_distinct`{.interpreted-text role="func"}, all of these aggregate
functions ignore null values and return null for no input rows or when
all values are null. For example, `sum`{.interpreted-text role="func"}
returns null rather than zero and `avg`{.interpreted-text role="func"}
does not include null values in the count. The `coalesce` function can
be used to convert null into zero.

# Ordering during aggregation {#aggregate-function-ordering-during-aggregation}

Some aggregate functions such as `array_agg`{.interpreted-text
role="func"} produce different results depending on the order of input
values. This ordering can be specified by writing an
`order-by-clause`{.interpreted-text role="ref"} within the aggregate
function:

    array_agg(x ORDER BY y DESC)
    array_agg(x ORDER BY x, y, z)

# Filtering during aggregation {#aggregate-function-filtering-during-aggregation}

The `FILTER` keyword can be used to remove rows from aggregation
processing with a condition expressed using a `WHERE` clause. This is
evaluated for each row before it is used in the aggregation and is
supported for all aggregate functions.

``` text
aggregate_function(...) FILTER (WHERE <condition>)
```

A common and very useful example is to use `FILTER` to remove nulls from
consideration when using `array_agg`:

    SELECT array_agg(name) FILTER (WHERE name IS NOT NULL)
    FROM region;

As another example, imagine you want to add a condition on the count for
Iris flowers, modifying the following query:

    SELECT species,
           count(*) AS count
    FROM iris
    GROUP BY species;

``` text
species    | count
-----------+-------
setosa     |   50
virginica  |   50
versicolor |   50
```

If you just use a normal `WHERE` statement you lose information:

    SELECT species,
        count(*) AS count
    FROM iris
    WHERE petal_length_cm > 4
    GROUP BY species;

``` text
species    | count
-----------+-------
virginica  |   50
versicolor |   34
```

Using a filter you retain all information:

    SELECT species,
           count(*) FILTER (where petal_length_cm > 4) AS count
    FROM iris
    GROUP BY species;

``` text
species    | count
-----------+-------
virginica  |   50
setosa     |    0
versicolor |   34
```

# General aggregate functions

**arbitrary(x)** &#8594 [same as input]

Returns an arbitrary non-null value of `x`, if one exists.

**array_agg(x)** &#8594 [same as input]

Returns an array created from the input `x` elements.

**avg(x)** &#8594 double

Returns the average (arithmetic mean) of all input values.

**avg(time interval type)** &#8594 time interval type

Returns the average interval length of all input values.

**bool_and(boolean)** &#8594 boolean

Returns `TRUE` if every input value is `TRUE`, otherwise `FALSE`.

**bool_or(boolean)** &#8594 boolean

Returns `TRUE` if any input value is `TRUE`, otherwise `FALSE`.

**checksum(x)** &#8594 varbinary

Returns an order-insensitive checksum of the given values.

**count(\*)** &#8594 bigint

Returns the number of input rows.

**count(x)** &#8594 bigint

Returns the number of non-null input values.

**count_if(x)** &#8594 bigint

Returns the number of `TRUE` input values. This function is equivalent
to `count(CASE WHEN x THEN 1 END)`.

**every(boolean)** &#8594 boolean

This is an alias for `bool_and`{.interpreted-text role="func"}.

**geometric_mean(x)** &#8594 double

Returns the geometric mean of all input values.

**listagg(x, separator)** &#8594 varchar

Returns the concatenated input values, separated by the `separator`
string.

Synopsis:

    LISTAGG( expression [, separator] [ON OVERFLOW overflow_behaviour])
        WITHIN GROUP (ORDER BY sort_item, [...])

If `separator` is not specified, the empty string will be used as
`separator`.

In its simplest form the function looks like:

    SELECT listagg(value, ',') WITHIN GROUP (ORDER BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);

and results in:

    csv_value
    -----------
    'a,b,c'

The overflow behaviour is by default to throw an error in case that the
length of the output of the function exceeds `1048576` bytes:

    SELECT listagg(value, ',' ON OVERFLOW ERROR) WITHIN GROUP (ORDER
    BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);

and results in:

    csv_value
    -----------
    'a,c,b'

The overflow behaviour can also be to truncate the output:

    SELECT listagg(value, ',' ON OVERFLOW TRUNCATE) WITHIN GROUP (ORDER
    BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);

and results in:

    csv_value
    -----------
    'a,b'

The overflow behaviour can also be to skip the overflowed values:

    SELECT listagg(value, ',' ON OVERFLOW SKIP) WITHIN GROUP (ORDER
    BY value) csv_value



The current implementation of `LISTAGG` function does not support window
frames.

**max(x)** &#8594 [same as input]

Returns the maximum value of all input values.

**max(x, n)** &#8594 array<[same as x]>

Returns `n` largest values of all input values of `x`.

**max_by(x, y)** &#8594 [same as x]

Returns the value of `x` associated with the maximum value of `y` over
all input values.

**max_by(x, y, n)** &#8594 array<[same as x]>

Returns `n` values of `x` associated with the `n` largest of all input
values of `y` in descending order of `y`.

**min(x)** &#8594 [same as input]

Returns the minimum value of all input values.

**min(x, n)** &#8594 array<[same as x]>

Returns `n` smallest values of all input values of `x`.

**min_by(x, y)** &#8594 [same as x]

Returns the value of `x` associated with the minimum value of `y` over
all input values.

**min_by(x, y, n)** &#8594 array<[same as x]>

Returns `n` values of `x` associated with the `n` smallest of all input
values of `y` in ascending order of `y`.

**sum(x)** &#8594 [same as input]

Returns the sum of all input values.

# Bitwise aggregate functions

**bitwise_and_agg(x)** &#8594 bigint

Returns the bitwise AND of all input values in 2\'s complement representation.

**bitwise_or_agg(x)** &#8594 bigint

Returns the bitwise OR of all input values in 2\'s complement representation.

# Map aggregate functions

**histogram(x)** &#8594 map\<K,bigint\>

Returns a map containing the count of the number of times each input value occurs.

**map_agg(key, value)** &#8594 map\<K,V\>

Returns a map created from the input `key` / `value` pairs.

**map_union(x(K,V))** &#8594 map\<K,V\>

Returns the union of all the input maps. If a key is found in multiple input maps, that key\'s value in the resulting map comes from an arbitrary input map.

**map_union_agg(x(K,V))** &#8594 map\<K,V\>

Returns the union of all the input maps. If a key is found in multiple input maps, that key\'s value in the resulting map comes from the last input map.

**multimap_agg(key, value)** &#8594 multimap\<K,V\>

Returns a multimap created from the input `key` / `value` pairs.

**multimap_union(x(K,V))** &#8594 multimap\<K,V\>

Returns the union of all the input multimaps. If a key is found in multiple input multimaps, that key\'s values in the resulting multimap are the union of all the values from the input multimaps.


# Approximate aggregate functions

**approx_distinct(x)** &#8594 bigint

Returns the approximate number of distinct input values. This function provides an approximation of `count(DISTINCT x)`. Zero is returned if all input values are null.

This function should produce a standard error of 2.3%, which is the standard deviation of the (approximately normal) error distribution over all possible sets. It does not guarantee an upper bound on the error for any specific input set.

**approx_distinct(x, e)** &#8594 bigint

Returns the approximate number of distinct input values. This function provides an approximation of `count(DISTINCT x)`. Zero is returned if all input values are null.

This function should produce a standard error of no more than `e`, which is the standard deviation of the (approximately normal) error distribution over all possible sets. It does not guarantee an upper bound on the error for any specific input set. The current implementation of this function requires that `e` be in the range of 0.0040625 to 0.26000.


**approx_most_frequent(x, k)** &#8594 map\<[same as x], bigint\>

Computes the top frequent values up to `buckets` elements approximately.
Approximate estimation of the function enables us to pick up the
frequent values with less memory. Larger `capacity` improves the
accuracy of underlying algorithm with sacrificing the memory capacity.
The returned value is a map containing the top elements with
corresponding estimated frequency.

The error of the function depends on the permutation of the values and
its cardinality. We can set the capacity same as the cardinality of the
underlying data to achieve the least error.

`buckets` and `capacity` must be `bigint`. `value` can be numeric or
string type.

The function uses the stream summary data structure proposed in the
paper [Efficient Computation of Frequent and Top-k Elements in Data
Streams](https://www.cse.ust.hk/~raywong/comp5331/References/EfficientComputationOfFrequentAndTop-kElementsInDataStreams.pdf)
by A. Metwalley, D. Agrawl and A. Abbadi.
:::

**approx_percentile(x, percentage)** &#8594 [same as x]

Returns the approximate percentile for all input values of `x` at the
given `percentage`. The value of `percentage` must be between zero and
one and must be constant for all input rows.

**approx_percentile(x, percentages)** &#8594 array\<\[same as x\]\>

Returns the approximate percentile for all input values of `x` at each
of the specified percentages. Each element of the `percentages` array
must be between zero and one, and the array must be constant for all
input rows.


**approx_percentile(x, w, percentage)** &#8594 [same as x]

Returns the approximate weighed percentile for all input values of `x`
using the per-item weight `w` at the percentage `percentage`. Weights
must be greater or equal to 1. Integer-value weights can be thought of
as a replication count for the value `x` in the percentile set. The
value of `percentage` must be between zero and one and must be constant
for all input rows.


**approx_percentile(x, w, percentages)** &#8594 array\<\[same as x\]\>

Returns the approximate weighed percentile for all input values of `x`
using the per-item weight `w` at each of the given percentages specified
in the array. Weights must be greater or equal to 1. Integer-value
weights can be thought of as a replication count for the value `x` in
the percentile set. Each element of the `percentages` array must be
between zero and one, and the array must be constant for all input rows.
:::

**approx_set(x)** &#8594 HyperLogLog

See `hyperloglog`
! TO DO LINKS

**merge(x)** &#8594 HyperLogLog

See `hyperloglog`{.interpreted-text role="doc"}.
! TO DO LINKS

**merge(qdigest(T))** &#8594 qdigest(T)

See `qdigest`{.interpreted-text role="doc"}.
! TO DO LINKS

**merge(tdigest)** &#8594 tdigest

See `tdigest`{.interpreted-text role="doc"}.


**numeric_histogram(buckets, value)** &#8594 map\<double, double\>

Computes an approximate histogram with up to `buckets` number of buckets for all `value`s. This function is equivalent to the variant of `numeric_histogram`{.interpreted-text role="func"} that takes a `weight`, with a per-item weight of `1`.



**numeric_histogram(buckets, value, weight)** &#8594 map\<double, double\>

Computes an approximate histogram with up to `buckets` number of buckets for all `value`s with a per-item weight of `weight`. The algorithm is based loosely on:

``` text
Yael Ben-Haim and Elad Tom-Tov, "A streaming parallel decision tree algorithm",
J. Machine Learning Research 11 (2010), pp. 849--872.
```

`buckets` must be a `bigint`. `value` and `weight` must be numeric.


**qdigest_agg(x)** &#8594 qdigest(\[same as x\])

See `qdigest`{.interpreted-text role="doc"}.

**qdigest_agg(x, w)** &#8594 qdigest(\[same as x\])

See `qdigest`{.interpreted-text role="doc"}.

**tdigest_agg(x)** &#8594 tdigest

See `tdigest`{.interpreted-text role="doc"}.

**tdigest_agg(x, w)** &#8594 tdigest

See `tdigest`{.interpreted-text role="doc"}.

# Statistical aggregate functions

**corr(x, y)** &#8594 double

Returns correlation coefficient of input values.

**covar_pop(y, x)** &#8594 double

Returns the population covariance of input values.

**covar_samp(y, x)** &#8594 double

Returns the sample covariance of input values.

**kurtosis(x)** &#8594 double

Returns the excess kurtosis of all input values. Unbiased estimate using the following expression:

``` text
kurtosis(x) = n(n+1)/((n-1)(n-2)(n-3))sum[(x_i-mean)^4]/stddev(x)^4-3(n-1)^2/((n-2)(n-3))
```

**regr_intercept(y, x)** &#8594 double

Returns linear regression intercept of input values. `y` is the dependent value and `x` is the independent value.

**regr_slope(y, x)** &#8594 double

Returns linear regression slope of input values. `y` is the dependent value and `x` is the independent value.

**skewness(x)** &#8594 double

Returns the skewness of all input values. Unbiased estimate using the following expression:

``` text

skewness(x) = n/((n-1)(n-2))sum[(x_i-mean)^3]/stddev(x)^3

```

**stddev(x)** &#8594 double

Returns the standard deviation of all input values.

**stddev_pop(x)** &#8594 double

Returns the population standard deviation of all input values.

**stddev_samp(x)** &#8594 double

Returns the sample standard deviation of all input values.

**variance(x)** &#8594 double

Returns the variance of all input values.

**var_pop(x)** &#8594 double

Returns the population variance of all input values.

**var_samp(x)** &#8594 double

Returns the sample variance of all input values.

# Lambda aggregate functions

**reduce_agg(inputValue T, initialState S, inputFunction(S, T, S), combineFunction(S, S, S))** &#8594 S

reduce_agg(inputValue T, initialState S, inputFunction(S, T, S),
combineFunction(S, S, S)) -\> S

Reduces all input values into a single value. `inputFunction` will be
invoked for each non-null input value. In addition to taking the input
value, `inputFunction` takes the current state, initially
`initialState`, and returns the new state. `combineFunction` will be
invoked to combine two states into a new state. The final state is
returned:

    SELECT id, reduce_agg(value, 0, (a, b) -> a + b, (a, b) -> a + b)
    FROM (
        VALUES
            (1, 3),
            (1, 4),
            (1, 5),
            (2, 6),
            (2, 7)
    ) AS t(id, value)
    GROUP BY id;
    -- (1, 12)
    -- (2, 13)

    SELECT id, reduce_agg(value, 1, (a, b) -> a * b, (a, b) -> a * b)
    FROM (
        VALUES
            (1, 3),
            (1, 4),
            (1, 5),
            (2, 6),
            (2, 7)
    ) AS t(id, value)
    GROUP BY id;
    -- (1, 60)
    -- (2, 42)

The state type must be a boolean, integer, floating-point, or
date/time/interval.

