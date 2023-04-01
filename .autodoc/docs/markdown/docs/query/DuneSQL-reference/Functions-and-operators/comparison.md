[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/Functions-and-operators/comparison.md)

# Comparisons

This technical guide covers comparison operators, range operators, null operators, greatest and least functions, quantified comparison predicates, and pattern comparison. It is a part of the Dune Docs project.

## Comparison Operators

This section covers the comparison operators in SQL. The table lists the operators and their descriptions. The operators include `<`, `>`, `<=`, `>=`, `=`, `<>`, and `!=`. 

## Range Operator: BETWEEN

This section covers the `BETWEEN` operator, which tests if a value is within a specified range. The section provides examples of how to use the operator and how to test if a value does not fall within the specified range. The section also covers how `NULL` is evaluated in a `BETWEEN` or `NOT BETWEEN` statement.

## IS NULL and IS NOT NULL

This section covers the `IS NULL` and `IS NOT NULL` operators, which test whether a value is null. The section provides examples of how to use the operators and how `NULL` is evaluated.

## IS DISTINCT FROM and IS NOT DISTINCT FROM

This section covers the `IS DISTINCT FROM` and `IS NOT DISTINCT FROM` operators, which treat `NULL` as a known value and guarantee either a true or false outcome even in the presence of `NULL` input. The section provides examples of how to use the operators and how `NULL` is evaluated.

## GREATEST and LEAST

This section covers the `GREATEST` and `LEAST` functions, which return the largest and smallest of the provided values, respectively. The section provides examples of how to use the functions and how `NULL` is evaluated.

## Quantified Comparison Predicates: ALL, ANY and SOME

This section covers the `ALL`, `ANY`, and `SOME` quantifiers, which can be used together with comparison operators. The section provides examples of how to use the quantifiers and the meanings of some quantifier and comparison operator combinations.

## Pattern Comparison: LIKE

This section covers the `LIKE` operator, which can be used to compare values with a pattern. The section provides examples of how to use the operator and how to match characters using the `_` and `%` symbols. The section also covers how to escape the wildcard characters `_` and `%`.

Overall, this technical guide provides a comprehensive overview of comparison operators, range operators, null operators, greatest and least functions, quantified comparison predicates, and pattern comparison in SQL. It is a useful resource for developers working on the Dune Docs project.
## Questions: 
 1. What comparison operators are supported by this app and what are their descriptions?
- The app supports comparison operators such as `<`, `>`, `<=`, `>=`, `=`, `<>`, and `!=`, and their descriptions are provided in a table format.

2. How does the app handle NULL values in the BETWEEN and NOT BETWEEN operators?
- The app evaluates NULL values in the BETWEEN and NOT BETWEEN operators using standard NULL evaluation rules applied to the equivalent expression.

3. What is the syntax and meaning of the LIKE operator in this app?
- The LIKE operator can be used to compare values with a pattern using symbols such as `_` and `%`, and it is typically used as a condition in WHERE statements. The app also provides examples of how to negate the result and escape wildcard characters.