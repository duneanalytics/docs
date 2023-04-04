[View code on GitHub](https://dune.com/docs/data-tables/spellbook/contributing/Adding A Spell/7-configure-alias-and-materialization-strategy.md)

This app technical guide covers the configuration of aliases and materialization strategies in the Spellbook project. The guide explains that materialization strategies are used to persist data in the data lake house and there are four materialization strategies in dbt: table, ephemeral, view, and incremental. Spellbook uses view and incremental strategies. 

The guide explains that view Spells are rebuilt each time they are run, meaning every time someone queries a view Spell, the SQL is run, and fresh data is gathered according to the Spell’s SQL logic. On the other hand, incremental Spells allow dbt to insert or update records in a table according to the logic defined. The guide provides an example of how to create an incremental Spell by including a statement of which column to join new data to the existing data each time the Spell is incremented.

The guide also explains how to configure aliases and materialization. To configure a Spell’s alias and materialization, the configuration is added to the top of each SQL file. The configuration includes creating an alias for the Spell file that will appear in the dune.com UI, defining how the file is stored and categorized in the UI, and naming the contributors. The guide provides an example of how to configure a Spell’s alias and materialization using a view materialization strategy.

Finally, the guide explains how to add new models to the dbt_project.yml file in the Spellbook root folder. The guide provides an example of how to specify the project name, schema, and materialization strategy for the project as a whole as well as the specific blockchain(s) that Spells have been created for. 

Overall, this guide provides a detailed explanation of how to configure aliases and materialization strategies in the Spellbook project. It is a useful resource for developers working on the project who need to configure aliases and materialization strategies for their Spells.
## Questions: 
 1. What are the available materialization strategies in dbt and which ones does Spellbook use?
- The available materialization strategies in dbt are `table`, `ephemeral`, `view`, and `incremental`. Spellbook uses `view` and `incremental`.

2. How does the `incremental` materialization strategy work and what configuration is needed to implement it?
- The `incremental` materialization strategy allows dbt to insert or update records in a table according to the logic defined. To implement it, the configuration section of the file needs to include a statement of which column to join new data to existing data, specify that it is an incremental Spell, and provide an instruction for how dbt should combine new/old data using `merge`. Additionally, `if` statements need to be added to any `FROM` for which data needs to be incremented.

3. How do you configure a Spell's alias and materialization and where is this configuration added?
- To configure a Spell's alias and materialization, the configuration is added to the top of each SQL file. The configuration includes creating an alias for the Spell file that will appear in the UI, defining how the file is stored and categorized in the UI, and specifying whether it is a Spell for a specific project or a whole sector. This configuration assumes the use of a `view` materialization strategy.