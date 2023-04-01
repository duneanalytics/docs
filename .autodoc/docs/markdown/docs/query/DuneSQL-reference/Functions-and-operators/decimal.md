[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/decimal.md)

# Decimal Functions and Operators

This technical guide provides information on how to use decimal literals, binary arithmetic decimal operators, comparison operators, and unary decimal operators in the Dune Docs project.

## Decimal Literals

To define a decimal literal, use the `DECIMAL 'xxxxxxx.yyyyyyy'` syntax. The precision of a decimal type for a literal will be equal to the number of digits in the literal (including trailing and leading zeros). The scale will be equal to the number of digits in the fractional part (including trailing zeros). The table below shows examples of decimal literals and their corresponding data types:

| Example literal                     | Data type     |
| ----------------------------------- | -------------|
| `DECIMAL '0'`                       | `DECIMAL(1)` |
| `DECIMAL '12345'`                   | `DECIMAL(5)` |
| `DECIMAL '0000012345.1234500000'`   | `DECIMAL(20, 10)` |

## Binary Arithmetic Decimal Operators

Standard mathematical operators are supported for decimal types. The table below explains precision and scale calculation rules for the result. Assuming `x` is of type `DECIMAL(xp, xs)` and `y` is of type `DECIMAL(yp, ys)`:

| Operation          | Result type precision                            | Result type scale |
|--------------------|--------------------------------------------------|-------------------|
| `x + y` and `x -y` | `min(38,1 +max(xs, ys) + max(xp - xs, yp - ys))` | `max(xs, ys)`     |
| `x * y`            | `min(38, xp + yp)`                               | `xs + ys`         |
| `x / y`            | `min(38, xp + ys + max(0, ys-xs))`               | `max(xs, ys)`     |
| `x % y`            | `min(xp - xs, yp - ys) + max(xs, bs)`            | `max(xs, ys)`     |

If the mathematical result of the operation is not exactly representable with the precision and scale of the result data type, then an exception condition is raised: `Value is out of range`. When operating on decimal types with different scale and precision, the values are first coerced to a common super type. For types near the largest representable precision (38), this can result in "Value is out of range" errors when one of the operands doesn't fit in the common super type. For example, the common super type of decimal(38, 0) and decimal(38, 1) is decimal(38, 1), but certain values that fit in decimal(38, 0) cannot be represented as a decimal(38, 1).

## Comparison Operators

All standard comparison operators work for the decimal type.

## Unary Decimal Operators

The `-` operator performs negation. The type of result is the same as the type of the argument.

This guide provides a clear understanding of how to use decimal literals, binary arithmetic decimal operators, comparison operators, and unary decimal operators in the Dune Docs project. The examples provided in the guide help to illustrate how to use these features in practice.
## Questions: 
 1. What is the purpose of the Dune Docs project and how does it relate to blockchain technology?
- The app technical guide does not provide information on the purpose of the Dune Docs project or its relation to blockchain technology.

2. Can the Decimal functions and operators be used with SQL databases commonly used in blockchain technology such as MySQL or PostgreSQL?
- The app technical guide does not specify which SQL databases are compatible with the Decimal functions and operators.

3. Are there any limitations or performance considerations when using the Decimal functions and operators with large datasets or complex calculations in a blockchain application?
- The app technical guide does not provide information on limitations or performance considerations when using the Decimal functions and operators in a blockchain application.