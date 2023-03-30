---
title: Overview
description: Dune utilizes a fork of TrinoSQL to power DuneSQL. DuneSQL is a custom built query engine that is optimized for blockchain data.   
---

!!!note 
    Not quite sure what I am going to do with this whole section as we are mostly using very basic Select statements.
    I think I can split this up into other higher level bound documents and not hide the content as much that way.


DuneSQL is an ANSI SQL compliant query engine. It is a fork of [TrinoSQL](https://trino.io).
This standard compliance allows Trino users to integrate their favorite data tools, including BI
and ETL tools with any underlying data source.

DuneSQL validates and translates the received SQL statements into the
necessary operations on the connected data source.

This chapter provides a reference to the supported SQL data types and
other general characteristics of the SQL support of DuneSQL.

A [full SQL statement and syntax reference](../SQL-statement-syntax/index.md) is available.

Trino also provides [numerous SQL functions and operators](../Functions-and-operators/index.md).
