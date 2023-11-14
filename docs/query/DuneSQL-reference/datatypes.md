# Datatypes

DuneSQL has a set of built-in data types, described below.

Implicit Conversion and Casting to other datatypes is described in [the conversion function documentation](Functions-and-operators/conversion.md).

## Boolean

### `BOOLEAN`

This type captures boolean values `true` and `false`.

## Integer

### `TINYINT`

A 8-bit signed two\'s complement integer with a minimum value of `-2^7`
and a maximum value of `2^7 - 1`.

### `SMALLINT`

A 16-bit signed two\'s complement integer with a minimum value of
`-2^15` and a maximum value of `2^15 - 1`.

### `INTEGER`

A 32-bit signed two\'s complement integer with a minimum value of
`-2^31` and a maximum value of `2^31 - 1`. The name `INT` is also
available for this type.

### `BIGINT`

A 64-bit signed two\'s complement integer with a minimum value of
`-2^63` and a maximum value of `2^63 - 1`.

### `UINT256` (Dune SQL)

A 256-bit unsigned integer with a minimum value of 0 and a maximum value of 2^256 - 1. This data type can represent only non-negative integers, including very large positive integers, as well as zero. Since there is no sign bit, all 256 bits can be used to represent the magnitude of the number. This data type is commonly used in EVM smart contracts to represent balances and other quantities.

### `INT256` (Dune SQL)

A 256-bit signed two's complement integer with a minimum value of -2^255 and a maximum value of 2^255 - 1. This data type can represent a wide range of values, including very large negative and positive integers, as well as zero.

This data type is commonly used in EVM smart contracts to represent balances and other quantities, more specifically when the value can be negative. 





## Floating-point

### `REAL`

A real is a 32-bit inexact, variable-precision implementing the IEEE
Standard 754 for Binary Floating-Point Arithmetic.

Example literals: `REAL '10.3'`, `REAL '10.3e0'`, `REAL '1.03e1'`

### `DOUBLE`

A double is a 64-bit inexact, variable-precision implementing the IEEE
Standard 754 for Binary Floating-Point Arithmetic.

Example literals: `DOUBLE '10.3'`, `DOUBLE '1.03e1'`, `10.3e0`, `1.03e1`

## Fixed-precision

### `DECIMAL`

A fixed precision decimal number. Precision up to 38 digits is supported
but performance is best up to 18 digits.

The decimal type takes two literal parameters:

-   **precision** - total number of digits
-   **scale** - number of digits in fractional part. Scale is optional
    and defaults to 0.

Example type definitions: `DECIMAL(10,3)`, `DECIMAL(20)`

Example literals: `DECIMAL '10.3'`, `DECIMAL '1234567890'`, `1.1`

## String

### `VARCHAR`

Variable length character data with an optional maximum length.

Example type definitions: `varchar`, `varchar(20)`

SQL statements support simple literal, as well as Unicode usage:

-   literal string : `'Hello winter !'`
-   Unicode string with default escape character:
    `U&'Hello winter \2603 !'`
-   Unicode string with custom escape character:
    `U&'Hello winter #2603 !' UESCAPE '#'`

A Unicode string is prefixed with `U&` and requires an escape character
before any Unicode character usage with 4 digits. In the examples above
`\2603` and `#2603` represent a snowman character. Long Unicode codes
with 6 digits require usage of the plus symbol before the code. For
example, you need to use `\+01F600` for a grinning face emoji.

### `CHAR`

Fixed length character data. A `CHAR` type without length specified has
a default length of 1. A `CHAR(x)` value always has `x` characters. For
example, casting `dog` to `CHAR(7)` adds 4 implicit trailing spaces.
Leading and trailing spaces are included in comparisons of `CHAR`
values. As a result, two character values with different lengths
(`CHAR(x)` and `CHAR(y)` where `x != y`) will never be equal.

Example type definitions: `char`, `char(20)`

### `VARBINARY`

Variable length binary data. In Dune, we store addresses, hashes, calldata and logs as `varbinary` data types.


SQL statements support usage of binary data with the prefix `0x`. The
binary data has to use hexadecimal format. For example, the binary form
of `eh?` is `X'65683F'`.

We have built custom functions to make it easier to work with varbinaries in DuneSQL. Check the [varbinary functions](../DuneSQL-reference/Functions-and-operators/varbinary.md) page for more information.

```sql
    Select * from ethereum.transactions where "from" = 0xc8ebccc5f5689fa8659d83713341e5ad19349448
```

### `JSON`

JSON value type, which can be a JSON object, a JSON array, a JSON
number, a JSON string, `true`, `false` or `null`.

## Date and time

See also [`date and time functions`](../DuneSQL-reference/Functions-and-operators/conversion.md).

### `DATE`

Calendar date (year, month, day).

Example: `DATE '2001-08-22'`

### `TIME`

`TIME` is an alias for `TIME(3)` (millisecond precision).

### `TIME(P)`

Time of day (hour, minute, second) without a time zone with `P` digits
of precision for the fraction of seconds. A precision of up to 12
(picoseconds) is supported.

Example: `TIME '01:02:03.456'`

### `TIME WITH TIME ZONE`

Time of day (hour, minute, second, millisecond) with a time zone. Values
of this type are rendered using the time zone from the value. Time zones
are expressed as the numeric UTC offset value:
```sql
    SELECT TIME '01:02:03.456 -08:00';
    -- 1:02:03.456-08:00
```
### `TIMESTAMP`

`TIMESTAMP` is an alias for `TIMESTAMP(3)` (millisecond precision).

### `TIMESTAMP(P)`

Calendar date and time of day without a time zone with `P` digits of
precision for the fraction of seconds. A precision of up to 12
(picoseconds) is supported. This type is effectively a combination of
the `DATE` and `TIME(P)` types.

`TIMESTAMP(P) WITHOUT TIME ZONE` is an equivalent name.

Timestamp values can be constructed with the `TIMESTAMP` literal
expression. Alternatively, language constructs such as
`localtimestamp(p)`, or a number of `date and time functions and
operators </functions/datetime>`{.interpreted-text role="doc"} can
return timestamp values.

Casting to lower precision causes the value to be rounded, and not
truncated. Casting to higher precision appends zeros for the additional
digits.

The following examples illustrate the behavior:

```sql
    SELECT TIMESTAMP '2020-06-10 15:55:23';
    -- 2020-06-10 15:55:23

    SELECT TIMESTAMP '2020-06-10 15:55:23.383345';
    -- 2020-06-10 15:55:23.383345

    SELECT typeof(TIMESTAMP '2020-06-10 15:55:23.383345');
    -- timestamp(6)

    SELECT cast(TIMESTAMP '2020-06-10 15:55:23.383345' as TIMESTAMP(1));
     -- 2020-06-10 15:55:23.4

    SELECT cast(TIMESTAMP '2020-06-10 15:55:23.383345' as TIMESTAMP(12));
    -- 2020-06-10 15:55:23.383345000000
```

### `TIMESTAMP WITH TIME ZONE` {#timestamp-with-time-zone-data-type}

`TIMESTAMP WITH TIME ZONE` is an alias for `TIMESTAMP(3) WITH TIME ZONE`
(millisecond precision).

### `TIMESTAMP(P) WITH TIME ZONE`

Instant in time that includes the date and time of day with `P` digits
of precision for the fraction of seconds and with a time zone. Values of
this type are rendered using the time zone from the value. Time zones
can be expressed in the following ways:

-   `UTC`, with `GMT`, `Z`, or `UT` usable as aliases for UTC.
-   `+hh:mm` or `-hh:mm` with `hh:mm` as an hour and minute offset from
    UTC. Can be written with or without `UTC`, `GMT`, or `UT` as an
    alias for UTC.
-   An [IANA time zone name](https://www.iana.org/time-zones).

The following examples demonstrate some of these syntax options:
```sql
    SELECT TIMESTAMP '2001-08-22 03:04:05.321 UTC';
    -- 2001-08-22 03:04:05.321 UTC

    SELECT TIMESTAMP '2001-08-22 03:04:05.321 -08:30';
    -- 2001-08-22 03:04:05.321 -08:30

    SELECT TIMESTAMP '2001-08-22 03:04:05.321 GMT-08:30';
    -- 2001-08-22 03:04:05.321 -08:30

    SELECT TIMESTAMP '2001-08-22 03:04:05.321 America/New_York';
    -- 2001-08-22 03:04:05.321 America/New_York
```
### `INTERVAL YEAR TO MONTH`

Span of years and months.

Example: `INTERVAL '3' MONTH`

### `INTERVAL DAY TO SECOND`

Span of days, hours, minutes, seconds and milliseconds.

Example: `INTERVAL '2' DAY`

## Structural

### `ARRAY` 

An array of the given component type.

Example: `ARRAY[1, 2, 3]`

### `MAP` 

A map between the given component types.

Example: `MAP(ARRAY['foo', 'bar'], ARRAY[1, 2])`

### `ROW` 

A structure made up of fields that allows mixed types. The fields may be
of any SQL type.

By default, row fields are not named, but names can be assigned.

Example: `CAST(ROW(1, 2e0) AS ROW(x BIGINT, y DOUBLE))`

Named row fields are accessed with field reference operator (`.`).

Example: `CAST(ROW(1, 2.0) AS ROW(x BIGINT, y DOUBLE)).x`

Named or unnamed row fields are accessed by position with the subscript
operator (`[]`). The position starts at `1` and must be a constant.

Example: `ROW(1, 2.0)[1]`

## Network address

### `IPADDRESS` 

An IP address that can represent either an IPv4 or IPv6 address.
Internally, the type is a pure IPv6 address. Support for IPv4 is handled
using the *IPv4-mapped IPv6 address* range
(`4291#section-2.5.5.2`{.interpreted-text role="rfc"}). When creating an
`IPADDRESS`, IPv4 addresses will be mapped into that range. When
formatting an `IPADDRESS`, any address within the mapped range will be
formatted as an IPv4 address. Other addresses will be formatted as IPv6
using the canonical format defined in `5952`{.interpreted-text
role="rfc"}.

Examples: `IPADDRESS '10.0.0.1'`, `IPADDRESS '2001:db8::1'`

## UUID

### `UUID` 

This type represents a UUID (Universally Unique IDentifier), also known
as a GUID (Globally Unique IDentifier), using the format defined in
`4122`{.interpreted-text role="rfc"}.

Example: `UUID '12151fd2-7586-11e9-8f9e-2a86e4085a59'`

## HyperLogLog

Calculating the approximate distinct count can be done much more cheaply
than an exact count using the
[HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog) data sketch.
See `/functions/hyperloglog`{.interpreted-text role="doc"}.

### `HyperLogLog` 

A HyperLogLog sketch allows efficient computation of
`approx_distinct`{.interpreted-text role="func"}. It starts as a sparse
representation, switching to a dense representation when it becomes more
efficient.

### `P4HyperLogLog` 

A P4HyperLogLog sketch is similar to
`hyperloglog_type`{.interpreted-text role="ref"}, but it starts (and
remains) in the dense representation.

## SetDigest

### `SetDigest` 

A SetDigest (setdigest) is a data sketch structure used in calculating
[Jaccard similarity
coefficient](https://en.wikipedia.org/wiki/Jaccard_index) between two
sets.

SetDigest encapsulates the following components:

-   [HyperLogLog](https://en.wikipedia.org/wiki/HyperLogLog)
-   [MinHash with a single hash
    function](http://en.wikipedia.org/wiki/MinHash#Variant_with_a_single_hash_function)

The HyperLogLog structure is used for the approximation of the distinct
elements in the original set.

The MinHash structure is used to store a low memory footprint signature
of the original set. The similarity of any two sets is estimated by
comparing their signatures.

SetDigests are additive, meaning they can be merged together.

## Quantile digest

### `QDigest` 

A quantile digest (qdigest) is a summary structure which captures the
approximate distribution of data for a given input set, and can be
queried to retrieve approximate quantile values from the distribution.
The level of accuracy for a qdigest is tunable, allowing for more
precise results at the expense of space.

A qdigest can be used to give approximate answer to queries asking for
what value belongs at a certain quantile. A useful property of qdigests
is that they are additive, meaning they can be merged together without
losing precision.

A qdigest may be helpful whenever the partial results of
`approx_percentile` can be reused. For example, one may be interested in
a daily reading of the 99th percentile values that are read over the
course of a week. Instead of calculating the past week of data with
`approx_percentile`, `qdigest`s could be stored daily, and quickly
merged to retrieve the 99th percentile value.

## T-Digest

### `TDigest` 

A T-digest (tdigest) is a summary structure which, similarly to qdigest,
captures the approximate distribution of data for a given input set. It
can be queried to retrieve approximate quantile values from the
distribution.

TDigest has the following advantages compared to QDigest:

-   higher performance
-   lower memory usage
-   higher accuracy at high and low percentiles

T-digests are additive, meaning they can be merged together.
