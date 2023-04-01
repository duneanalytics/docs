---
title: Conversions
---

Trino will implicitly convert numeric and character values to the
correct type if such a conversion is possible. Trino will not convert
between character and numeric types. For example, a query that expects a
varchar will not automatically convert a bigint value to an equivalent
varchar.

When necessary, values can be explicitly cast to a particular type.

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
**``format_number(number, decimal_places)``** → varchar
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

