---
title: Conversions
---

## Implicit Conversions

DuneSQL will implicitly convert numeric and character values to the correct type if such a conversion is possible.  
DuneSQL will not convert implicitly between character and numeric types.  
For example, a query that expects a `VARCHAR` will not automatically convert a `BIGINT` value to an equivalent `VARCHAR`.

When necessary, values can be explicitly cast to a particular type using the [cast function](#cast).

### Implicit Casting with numeric types

DuneSQL has added support for implicit casts when performing operations with `INT256` and `UINT256` and other numeric types like `INTEGER`, `BIGINTEGER`, `DECIMAL`, or `DOUBLE`.
This allows you to use `INT256` and `UINT256` without adding casts explicitly.

Whenever DuneSQL needs to find a common type for `INT256` or `UINT256` and another numeric type, it will generally go towards the bigger type.  
We consider `INT256` to be bigger than `UINT256`. In some cases, this might lead to an overflow error when trying to include `UINT256` and `INT256` values into the same expression. 

`TINYINT`, `SMALLINT`, `INTEGER`, `BIGINT`, and `DECIMAL` type with zero scale, like `DECIMAL(2,0)` will be converted to `INT256` or `UINT256`.
Please note that some conversions to `UINT256` will fail, since this type cannot hold negative values.

For operations involving `INT256` or `UINT256` and `DECIMAL` type with non-zero scale, like `DECIMAL(2,1)`,
the result type is `DOUBLE`. Also, for operations involving `INT256` or `UINT256` and `REAL` or `DOUBLE` types, the result type is `DOUBLE`.
Please note that `DOUBLE` is an approximate numeric type and hence the conversion might lose some precision.
You can use explicit cast to override DuneSQL conversion rules.

With implicit conversion, this arithmetic expression:

```sql
SELECT 2 * UINT256 '1';
```

will be equivalent to:

```sql
SELECT CAST(2 AS UINT256) * UINT256 '1';
```

Similarly, this comparison:

```sql
SELECT INT256 '1' > 0;
```

will be equivalent to:

```sql
SELECT INT256 '1' > CAST(0 AS INT256);
```

DuneSQL uses implicit conversions in many other contexts. Here are some examples:

```sql
SELECT COALESCE(1, INT256 '2');
-- will resolve to INT256
```

```sql
SELECT CASE 
    WHEN false THEN BIGINT '0' 
    WHEN false THEN INT256 '1' 
    WHEN true THEN UINT256 '2' 
END;
-- will resolve to INT256
```

```sql
SELECT * FROM (
    (VALUES TINYINT '0') 
    UNION 
    (VALUES INT256 '1') 
    UNION 
    (VALUES DOUBLE '2'));
-- will resolve to DOUBLE
```

### Conversion functions


#### cast() 
**``cast(value AS type)``** → type

Explicitly cast a value as a type. This can be used to cast a varchar to
a numeric value type and vice versa.


#### try_cast()
**``try_cast(value AS type)``** → type

Like `cast`, but returns `null` if the cast
fails.

### Formatting

#### format()
**``format(format, args\...)``** → varchar

Returns a formatted string using the specified [format
string](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Formatter.html#syntax)
and arguments:
```sql
    SELECT format('%s%%', 123);
    -- '123%'

    SELECT format('%.5f', pi());
    -- '3.14159'

    SELECT format('%03d', 8);
    -- '008'

    SELECT format('%,.2f', 1234567.89);
    -- '1,234,567.89'

    SELECT format('%-7s,%7s', 'hello', 'world');
    -- 'hello  ,  world'

    SELECT format('%2$s %3$s %1$s', 'a', 'b', 'c');
    -- 'b c a'

    SELECT format('%1$tA, %1$tB %1$te, %1$tY', date '2006-07-04');
    -- 'Tuesday, July 4, 2006'
```

#### format_number()
**``format_number(number)``** → varchar
Returns a formatted string using a unit symbol:

    SELECT format_number(123456); -- '123K'
    SELECT format_number(1000000); -- '1M'



### Miscellaneous

#### typeof()
**``typeof(expr)``** → varchar

Returns the name of the type of the provided expression:
```sql
    SELECT typeof(123); -- integer
    SELECT typeof('cat'); -- varchar(3)
    SELECT typeof(cos(2) + 1.5); -- double
```

