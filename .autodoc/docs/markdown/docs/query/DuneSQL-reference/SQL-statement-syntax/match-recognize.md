[View code on GitHub](https://dune.com/docs/query/DuneSQL-reference/SQL-statement-syntax/match-recognize.md)

The app technical guide covers the `MATCH_RECOGNIZE` clause, which is used to detect patterns in a set of rows using row pattern syntax based on regular expressions. The guide explains various components of the `MATCH_RECOGNIZE` clause, such as partitioning and ordering, row pattern measures, rows per match, after match skip, row pattern syntax, row pattern union variables, row pattern variable definitions, and row pattern recognition expressions.

The guide provides examples to illustrate the usage of the `MATCH_RECOGNIZE` clause, such as detecting a V-shape pattern in the `totalprice` column of orders made by a customer. It also explains the usage of various subclauses, such as `PARTITION BY`, `ORDER BY`, `MEASURES`, `ROWS PER MATCH`, `AFTER MATCH SKIP`, `PATTERN`, `SUBSET`, and `DEFINE`.

Additionally, the guide covers the usage of pattern navigation functions, aggregate functions, and the `RUNNING` and `FINAL` semantics in the context of row pattern recognition. It also discusses the evaluation of expressions in empty matches and unmatched rows.
## Questions: 
 1. **What is the purpose of the `MATCH_RECOGNIZE` clause in the app technical guide?**

   The `MATCH_RECOGNIZE` clause is an optional subclause of the `FROM` clause, used to detect patterns in a set of rows. Patterns of interest are specified using row pattern syntax based on regular expressions. For each detected match, one or more rows are returned, containing requested information about the match.

2. **How can I use the `MEASURES` clause in the app technical guide?**

   The `MEASURES` clause allows you to specify what information is retrieved from a matched sequence of rows. It consists of measure expressions that are scalar expressions whose value is computed based on a match. Each measure defines an output column of the pattern recognition, and the column can be referenced with the `measure_name`.

3. **What is the difference between `ONE ROW PER MATCH` and `ALL ROWS PER MATCH` in the app technical guide?**

   `ONE ROW PER MATCH` is the default option, where for every match, a single row of output is produced, consisting of `PARTITION BY` columns and measures. `ALL ROWS PER MATCH` produces an output row for every row of a match, unless it is excluded from the output by the exclusion syntax. Output consists of `PARTITION BY` columns, `ORDER BY` columns, measures, and remaining columns from the input table.