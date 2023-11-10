---
title: Conversions
---

## Implicit Conversions

DuneSQL will implicitly convert numeric and character values to the correct type if such a conversion is possible.  
DuneSQL will not convert implicitly between character and numeric types.  
For example, a query that expects a varchar will not automatically convert a bigint value to an equivalent varchar.

When necessary, values can be explicitly cast to a particular type.

### Implicit Casting with numeric types

DuneSQL has added support for implicit casts when performing arithmetic with `INT256` and `UINT256` and smaller types like `INTEGER`, `BIGINTEGER`, and `DECIMAL(38,0)`. This allows you to write expressions like `2 * UINT256 '1'` instead of `CAST(2 AS UINT256) * UINT256 '1'`, and similarly for other arithmetic operations.


Whenever DuneSQL needs to find a common type for `INT256` or `UINT256` and another numeric type, it will generally go towards the bigger type.

`TINYINT`, `SMALLINT`, `INTEGER`, `BIGINT`, and `DECIMAL` types will be converted to `INT256` or `UINT256`.

Please note that `UINT256` cannot hold negative values, so conversions from `TINYINT`, `SMALLINT`, `INTEGER`, and `BIGINT` types with negative values will fail. You will need to use explicit cast to override DuneSQL conversion rules. Please be aware that a conversion from `UINT256` to either `INT256` or `DOUBLE` will result in a precision loss.  

Also, conversions from `DECIMAL` type with non-zero scale, like `DECIMAL(2,1)`, will fail. The commonly used `DECIMAL` type with zero scale, like `DECIMAL(38,0)`, will be converted to `INT256` or `UINT256` without any issues.

For `REAL` and `DOUBLE` types, the conversion goes from `INT256` or `UINT256` to `REAL` or `DOUBLE`.
Please note that `REAL` and `DOUBLE` are approximate numeric types and hence the conversion might lose some precision.
You can use explicit cast to override DuneSQL conversion rules.

With implicit conversion, this arithmetic expression:


```sql
SELECT 2 * UINT256 '1';
```

Will be equivalent to:

```sql
SELECT CAST(2 AS UINT256) * UINT256 '1';
```

!!! warning 
    Please note that implicit casting has not been added for arithmetic with DOUBLE to make precision issues more apparent.

```sql
SELECT COALESCE(1, INT256 '2');
--resolves to INT256 '1'
```

```sql
SELECT CASE 
    WHEN false THEN BIGINT '0' 
    WHEN false THEN INT256 '1' 
    WHEN true THEN UINT256 '2' 
END;
--will resolve to UNIT256 type, since it is the biggest type
```


```sql
SELECT * FROM (
    (VALUES TINYINT '0') 
    UNION 
    (VALUES INT256 '1') 
    UNION 
    (VALUES DOUBLE '2'));
--  resolves to DOUBLE '0', DOUBLE '1', DOUBLE '2'
```


### Conversion functions


#### cast() 
**``cast(value AS type)``** → type

Explicitly cast a value as a type. This can be used to cast a varchar to
a numeric value type and vice versa.


#### try_cast()
**``try_cast(value AS type)``** → type

Like `cast`{.interpreted-text role="func"}, but returns null if the cast
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

