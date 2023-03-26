[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\index.md)

The app technical guide covers the Spells feature of the Dune project. Spells are custom tables that are built and maintained by Dune and the community. The guide explains that Spells are available on Dune V2 and can be queried from both Spark SQL and Dune SQL V2 Query Engines. The guide also provides a link to the Spellbook GitHub repository where the Spells can be found. 

The guide explains that the Spellbook is a retooling of the existing abstractions repository and a first-in-class open-source analytics engineering tool called dbt. Abstractions are some of the most queried tables on Dune, and the Spellbook aims to make the experience of creating them better. The guide explains that dbt allows for the writing and management of unit tests to spot and prevent any issues in the abstractions. 

The guide also explains that there are two types of Spells: Sector Spells and Project Spells. Sector Spells are tables that take in data from multiple contracts and projects, standardize the data across them, and make it easy to query for this data and compare the metrics of different projects with each other. Project Spells allow projects to assemble their data into one neat table that has all the data they need in one place. 

The guide provides information on how to contribute to the Spellbook and how to view available Spells. It also warns that the abstractions for V1 are no longer open for contributions and will be sunsetted with the V1 engine soon. 

Overall, the app technical guide provides a detailed explanation of the Spells feature of the Dune project, including how to use it, how to contribute to it, and how it can benefit users.
## Questions: 
 1. What is the purpose of Spells in Dune and how are they maintained?
- Spells are custom tables that cover a type of activity on the blockchain and are built and maintained by Dune and their community.

2. What is the difference between Abstractions and Spells in Dune?
- Abstractions are snippets of SQL executed on the data platform for the V1 engine, while Spells are models or tables that can be materialized into views and tables using dbt for the V2 engine.

3. How can a blockchain SQL analyst contribute to Spellbook and what are some benefits of using dbt?
- A blockchain SQL analyst can contribute to Spellbook by creating new Spells and submitting pull requests to the public GitHub repository. Using dbt allows for classical software engineering practices to be injected into writing SQL, including managing dependencies, writing and managing unit tests, and adding data integrity tests with minimal effort.