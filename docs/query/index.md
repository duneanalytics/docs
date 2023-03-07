---
title: Query Overview
description: Dune utilizes a fork of TrinoSQL to power DuneSQL. DuneSQL is a custom built query engine that is optimized for blockchain data.   
---

Querying for data on Dune is done using DuneSQL, a custom built query engine that is optimized for blockchain data. DuneSQL is a fork of [TrinoSQL](https://trino.io), an open source distributed SQL query engine for big data, to which we have added blockchain specific optimizations. TrinoSQL utilizes parquet files as its storage format, which is a columnar storage format that is optimized for fast reads. DuneSQL features an ANSI compliant SQL dialect. 
## Querying using DuneSQL
DuneSQL provides a crypto native SQL experience. Since DuneSQL is based on TrinoSQL, much of the same rules and syntax apply. However, there are several differences that are important to note. DuneSQL supports blockchain varbinary data types, which are used to store addresses, hashes, and other encoded data. Additionally, DuneSQL natively supports unint256 and int256 data types, which are used to store large numbers in blockchain data. For both of these data types, DuneSQL provides a set of functions that allow you to easily work with them. 

You can learn about querying using DuneSQL in the [DuneSQL](DuneSQL.md) section.
## Storage
DuneSQL utilizes a columnar storage format, which is a storage format that is optimized for fast reads. In a columnar storage format, data is stored in columns instead of rows. This allows for fast reads of a single column, which is useful for aggregations and filters. To write efficient DuneSQL queries, it is important to understand how data is stored in DuneSQL.  

You can learn more about the database layout and how to query it in the [Storage](storage.md) section.
## Other questions and feedback

Google and ChatAIs are a great friend in answering your SQL questions.

Since DuneSQL is built on Trino googling for e.g. “Trino SQL median” should most likely get you the answer you need. 

Trino also has a great documentation site that is worth checking out:

* [Trino - Functions and Operators](https://trino.io/docs/current/functions.html)

Our [#dune-sql Discord channel](https://discord.gg/dunecom) is the best place to get help from our team and Wizard community when Google fails you.

As you come across issues or identify areas of improvement, please send us an email at [dunesql-feedback@dune.com](mailto:dunesql-feedback@dune.com) and we’ll work with you to update and optimize!
