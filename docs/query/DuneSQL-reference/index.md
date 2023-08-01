---
title: DuneSQL Overview
description: Dune utilizes a fork of TrinoSQL to power DuneSQL. DuneSQL is a custom built query engine that is optimized for blockchain data.
---

**DuneSQL is a custom-built query engine designed for efficient analysis of blockchain data. Based on the open-source TrinoSQL engine, it incorporates additional optimizations to handle blockchain-specific requirements.**

## [Functions and Operators](Functions-and-operators/index.md)

DuneSQL provides a wide array of functions and operators that enable you to perform various operations on your data. These include arithmetic, string manipulation, date and time calculations, and much more.

## [Data Types](datatypes.md)

DuneSQL supports a variety of data types, including numeric, string, date, time, and boolean. Additionally, DuneSQL introduces custom data types and functions to better handle unique aspects of blockchain data, such as varbinary data types for addresses and hashes, as well as int256 and uint256 data types for large numeric values.

## SQL Statement Syntax 

DuneSQL follows the standard SQL syntax, which consists of a series of clauses that define how data should be retrieved, manipulated, or stored. Commonly used clauses include SELECT, FROM, WHERE, GROUP BY, ORDER BY, and LIMIT. Each clause serves a specific purpose and can be combined to create complex queries that meet your data analysis needs.

Since DuneSQL is administrated by Dune, all `create`, `update`, `delete`, `drop` and other administrative statements are disabled. This is to ensure that the data in the database is not modified in any way.  
However, you can [query queries](../query-a-query.md) in DuneSQL to replace the ability to create views and tables.
