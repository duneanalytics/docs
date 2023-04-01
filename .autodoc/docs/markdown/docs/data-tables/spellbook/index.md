[View code on GitHub](https://dune.com/docs/data-tables/spellbook/index.md)

The app technical guide covers the topic of Spells, which are custom tables constructed and maintained by Dune and the community. The guide explains that Spells are available on Dune V2 and can be queried from both Spark SQL and Dune SQL V2 Query Engines. The guide also provides a link to the Spellbook GitHub repository, where all the Spellbook Spell tables can be found. 

The guide then introduces the new Spellbook, which is a retooling of the existing abstractions repository and a first-in-class open-source analytics engineering tool called dbt. The guide explains that dbt allows for the writing and management of unit tests to spot and prevent any issues in abstractions. It also allows for data integrity tests to be added with a single line in a YAML file. The guide highlights that dbt natively understands the dependencies between all models, which makes deploying and maintaining them easier. 

The guide then goes on to explain Sector Spells, which are tables that take in data from multiple contracts and projects, standardize the data across them, and make it easy to query for this data and compare the metrics of different projects with each other. The guide notes that most of the sector dashboards depend on sector spells and that projects can easily get their data into these dashboards by making a pull request to the public GitHub repo. 

The guide also explains Project Spells, which allow projects to assemble their data into one neat table that has all the data they need in one place. The main advantage of using Spells over just constructing a view is that Spells can deal with bigger amounts of data since they can run automatically in the background every few hours. 

Finally, the guide provides information on how to contribute to Spellbook and how to view available Spells. It notes that Spells are managed via the public Spellbook GitHub repository and that pull requests are welcome. The guide also provides a warning that the abstractions for V1 are no longer open for contributions and will be sunsetted with the V1 engine soon. 

Overall, the app technical guide provides a comprehensive overview of Spells, the Spellbook, and how to contribute to Spellbook. It is a useful resource for anyone looking to understand how to use Spells and how to contribute to the Spellbook project.
## Questions: 
 1. What is the purpose of Spells in Dune and how are they maintained?
- Spells are custom tables that cover a type of activity on the blockchain and are built and maintained by Dune and their community.

2. What is the difference between Sector Spells and Project Spells?
- Sector Spells standardize data from multiple contracts and projects, making it easy to query and compare metrics, while Project Spells allow projects to assemble their data into one table and deal with larger amounts of data automatically.

3. What is dbt and how does it improve the process of creating Spells?
- dbt is an open-source analytics engineering tool that injects classical software engineering practices into writing SQL, allowing for the creation and management of unit tests and easy addition of data integrity tests. It also understands the dependencies between all models, making deploying and maintaining Spells more efficient.