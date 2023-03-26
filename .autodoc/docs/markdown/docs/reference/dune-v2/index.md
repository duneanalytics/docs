[View code on GitHub](https://dune.com/blob/master/reference\dune-v2\index.md)

The Dune V2 technical guide provides an overview of the new features and updates to the Dune Engine V2, which is a query engine and database that enables users to query, extract, and visualize blockchain data. The guide explains that Dune V2 brings a new level of performance, scalability, and functionality to the core tools that let Wizards query, extract, and visualize the vast amounts of blockchain data available. 

The guide highlights two significant updates to the Dune V2: a scalable column-oriented database and two new query engines, Dune SQL and Spark SQL. The new database architecture is transitioning away from a PostgreSQL database to a scalable columnar database. The difference between the two systems is that V2 uses a columnar storage format in contrast to PostgreSQL’s row-oriented approach. Traditional indexes are replaced by block range indexes, which are chunk level min/max values. 

The guide also explains that DuneV2 leverages two different query engines as it transitions away from a PostgreSQL database to a data lake house. Spark SQL was the initial choice for a V2 Query engine, but after gathering data and feedback from the Beta release, the team realized it won’t allow them to continue to have the best blockchain data querying experience as they scale. The solution is Dune SQL powered by Trino, and it is live in alpha. 

The guide also explains that abstractions in DuneV2 run on dbt (data build tool), which enables analytics engineers to transform data in their warehouses by simply writing select statements, then dbt handles turning these select statements into tables and views. Spells currently run on Spark SQL in Dune v2 but can also be queried on Dune SQL. 

The guide provides links to resources where users can find more information about the new query engines and built-in functions. The guide also encourages users to reach out to the Dune team for help and feedback. 

Overall, the Dune V2 technical guide provides a comprehensive overview of the new features and updates to the Dune Engine V2, which is a query engine and database that enables users to query, extract, and visualize blockchain data. The guide is useful for developers and data analysts who want to learn more about the new features and updates to the Dune Engine V2.
## Questions: 
 1. What is the difference between Dune V2's column oriented database and PostgreSQL's row oriented approach?
- Dune V2's database uses a columnar storage format, while PostgreSQL uses a row oriented approach.
2. Why did the Dune team decide to transition from Spark SQL to Dune SQL?
- After gathering data and feedback from their Beta release, the Dune team realized that Dune SQL powered by Trino would provide a better blockchain data querying experience as they scale.
3. What is the best way to get help from the Dune team and Wizard community when encountering issues with Dune V2?
- The best place to get help is the #dune-sql Discord channel, and users can also send an email to dunesql-feedback@dune.com for assistance with updating and optimizing the app.