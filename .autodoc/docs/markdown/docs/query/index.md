[View code on GitHub](https://dune.com/docs/query/index.md)

# DuneSQL: Query Engine for Blockchain Data

The DuneSQL app technical guide provides an overview of the custom-built query engine designed for efficient analysis of blockchain data. DuneSQL is a fork of TrinoSQL, an open-source, distributed SQL query engine for running interactive analytic queries against data sources of all sizes ranging from gigabytes to petabytes. The guide highlights the additional optimizations incorporated into DuneSQL to handle blockchain-specific requirements.

The guide outlines the features of DuneSQL, including blockchain varbinary data types, native support for uint256 and int256 data types, columnar storage format, and querying a query. The blockchain varbinary data types are designed for storing addresses, hashes, and other encoded data. The native support for uint256 and int256 data types is ideal for handling large numbers commonly found in blockchain data, with built-in functions for ease of use. The columnar storage format is optimized for fast reads, organizing data in columns rather than rows, enabling quick access to single columns for aggregation or filtering. Querying a query allows users to create reusable queries, build up complex queries, and reuse queries as views.

The guide provides extensive documentation for DuneSQL, which can be found in the DuneSQL Reference section of the documentation. The DuneSQL Reference section includes SQL statement reference, SQL language reference, and functions and operators. The guide also highlights the importance of understanding DuneSQL storage for an efficient query-writing process. The Storage section of the documentation provides details on the database layout and querying techniques.

The guide provides resources and support for assistance with DuneSQL, including a Google search for TrinoSQL-related queries, talking to an AI assistant about TrinoSQL-related questions, and the official Trino docs - Functions and Operators. Users can also join the #dune-sql Discord channel to connect with the team and the community for help and support.

Finally, the guide encourages feedback and suggestions for improvement. Users can email dunesql-feedback@dune.com with any concerns or ideas for optimization.

Overall, the DuneSQL app technical guide provides a comprehensive overview of the custom-built query engine designed for efficient analysis of blockchain data. The guide highlights the features of DuneSQL, provides extensive documentation, and offers resources and support for assistance with DuneSQL.
## Questions: 
 1. What optimizations does DuneSQL incorporate to handle blockchain-specific requirements?
- DuneSQL incorporates additional optimizations to handle blockchain-specific requirements, but the specific details are not provided in the app technical guide.

2. What blockchain data types does DuneSQL support?
- DuneSQL supports blockchain varbinary data types for storing addresses, hashes, and other encoded data, as well as native support for uint256 and int256 data types for handling large numbers commonly found in blockchain data.

3. What resources are available for assistance with DuneSQL?
- Resources for assistance with DuneSQL include a Google search for TrinoSQL-related queries, talking to an AI assistant about TrinoSQL-related questions, joining the #dune-sql Discord channel, and referring to the official Trino docs for functions and operators.