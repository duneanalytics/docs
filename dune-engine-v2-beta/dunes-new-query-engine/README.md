# Dune's New Query Engine

**Dune Engine V2** is Dune's new query engine that brings a new level of performance, scalability and functionality to Dune's core set of tools that enables wizards to query, extract, and visualize the vast amounts of data on the blockchain.

It leverages **Apache Spark** to enable increased performance of complex queries, handle data scale, and enable cross-chain queries all within the same UI.

All of the data sources contained in this section are available for querying with the new query engine today. Currently we have the following data available to query:

* ****[**Ethereum raw tables**](../../data-tables/data-tables/raw-data/ethereum-data.md)****
  * Example: [https://dune.com/hildobby/Ethereum-Overview](https://dune.com/hildobby/Ethereum-Overview)
* ****[**Solana**](solana-data/) ****&#x20;
  * Example: [https://dune.com/danning.sui/Solana-User-Base](https://dune.com/danning.sui/Solana-User-Base)
* ****[**Flashbots**](community-data/flashbots.md)****
  * Example: [https://dune.com/niftytable/MEV](https://dune.com/niftytable/MEV)
* ****[**Prices**](../../data-tables/data-tables/prices.md) (including Solana)

Keep in mind that due to the change from Postgres to Spark there will be a slight change in how queries are written in the application. A reference document to use as you start to query the new query engine is available below but if you run into challenges building your queries, come join us on Discord and ask the community!

{% embed url="https://spark.apache.org/docs/latest/sql-ref-ansi-compliance.html" %}

One final note, as the query engine is still in in **beta** you may run into bugs or have feedback on how it can be improved, feel free to share it with us on [Discord](https://discord.com/invite/ErrzwBz) and [Canny](https://dune.canny.io).
