[View code on GitHub](https://dune.com/blob/master/query\index.md)

# Query Overview

This technical guide covers the querying process for data on Dune using DuneSQL, a custom-built query engine optimized for blockchain data. DuneSQL is a fork of TrinoSQL, an open-source distributed SQL query engine for big data, with added blockchain-specific optimizations. The guide explains how DuneSQL utilizes parquet files as its storage format, which is a columnar storage format optimized for fast reads. 

The guide provides an overview of how to query using DuneSQL, highlighting the differences between DuneSQL and TrinoSQL. DuneSQL supports blockchain varbinary data types, which are used to store addresses, hashes, and other encoded data. Additionally, DuneSQL natively supports unint256 and int256 data types, which are used to store large numbers in blockchain data. The guide provides a set of functions that allow users to easily work with these data types. 

The guide also covers the storage format used by DuneSQL, which is important to understand when writing efficient queries. Data is stored in columns instead of rows, allowing for fast reads of a single column, which is useful for aggregations and filters. 

The guide provides resources for users to get help with SQL questions, including Google, ChatAIs, and the Trino documentation site. The #dune-sql Discord channel is also available for users to get help from the Dune team and Wizard community. Finally, the guide encourages users to send feedback to dunesql-feedback@dune.com to help improve and optimize the platform. 

Overall, this technical guide provides a comprehensive overview of querying on Dune using DuneSQL, including the data types and storage format used, as well as resources for users to get help and provide feedback.
## Questions: 
 1. What optimizations has DuneSQL added to TrinoSQL specifically for blockchain data?
   
   Answer: The app technical guide mentions that DuneSQL has added blockchain specific optimizations to TrinoSQL, but it does not provide specific details on what those optimizations are. A blockchain SQL analyst might want to know more about these optimizations and how they improve query performance for blockchain data.

2. How does DuneSQL handle large numbers in blockchain data?
   
   Answer: The app technical guide mentions that DuneSQL natively supports unint256 and int256 data types for storing large numbers in blockchain data, but it does not provide specific details on how these data types are handled. A blockchain SQL analyst might want to know more about how DuneSQL handles these data types and what functions are available for working with them.

3. How does the columnar storage format used by DuneSQL compare to other storage formats commonly used in blockchain data analysis?
   
   Answer: The app technical guide mentions that DuneSQL utilizes a columnar storage format that is optimized for fast reads, but it does not provide a comparison to other storage formats commonly used in blockchain data analysis. A blockchain SQL analyst might want to know more about the advantages and disadvantages of using a columnar storage format for blockchain data analysis compared to other storage formats such as row-based or document-based storage.