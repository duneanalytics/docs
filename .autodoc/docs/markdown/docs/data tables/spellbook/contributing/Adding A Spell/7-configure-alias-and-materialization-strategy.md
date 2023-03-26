[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\contributing\Adding A Spell\7-configure-alias-and-materialization-strategy.md)

This technical guide covers the configuration of aliases and materialization strategies in the dune docs project. The guide explains how to configure aliases for Spells, which are SQL files that contain logic for data transformation, and how to specify the materialization strategy for each Spell. The guide also provides an overview of the four materialization strategies available in dbt, which are table, ephemeral, view, and incremental. 

The `view` materialization strategy is the default in Spellbook, and it is used to store SQL logic without additional data. The `incremental` materialization strategy, on the other hand, allows dbt to insert or update records in a table according to the defined logic. The guide provides an example of how to create an incremental Spell by specifying the partition column, materialization type, and incremental strategy. 

To configure aliases and materialization, the guide explains how to add configuration to the top of each SQL file. The configuration includes an alias for the Spell file that appears in the dune.com UI, as well as how the file is stored and categorized in the UI. The guide provides an example of how to configure aliases for a `view` materialization strategy. 

Finally, the guide explains how to add new models to the `dbt_project.yml` file in the Spellbook root folder. The models section specifies the project name, schema, and materialization strategy for the project as a whole, as well as the specific blockchain(s) that the Spells are created for. 

Overall, this guide provides a comprehensive overview of how to configure aliases and materialization strategies in the dune docs project. It is a useful resource for developers who are working on the app, API, data tables, or query features of the project.
## Questions: 
 1. What are the available materialization strategies in dbt and which ones does Spellbook use?
   
   Answer: There are 4 materialization strategies in dbt: `table`, `ephemeral`, `view`, and `incremental`. Spellbook uses `view` and `incremental`.
   
2. How can an `incremental` Spell be created and what are the benefits of using it?

   Answer: An `incremental` Spell can be created by including specific configuration statements in the Config section of the SQL file. The benefits of using it are faster run times, though the data won't be as fresh as `view` Spells.
   
3. How can aliases and materialization be configured for a Spell and where should this configuration be added?

   Answer: Aliases and materialization can be configured for a Spell by adding configuration statements to the top of each SQL file. This configuration assumes a `view` materialization strategy. It should be added to the top of each SQL file.