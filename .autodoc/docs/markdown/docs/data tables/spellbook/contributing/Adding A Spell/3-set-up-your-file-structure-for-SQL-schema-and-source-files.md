[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\contributing\Adding A Spell\3-set-up-your-file-structure-for-SQL-schema-and-source-files.md)

This technical guide provides instructions on how to set up the file structure for SQL, schema, and source files in the Dune Docs project. The guide explains that all Spells are stored in the `/spellbook/models` directory by project name and blockchain network. The folder names are all lowercase, and words are separated by underscores. The guide provides an example of the folder structure for the Keep3r network, where the folder is `/spellbook/models/keep3r_network/ethereum`. 

The guide explains that if the project folder exists but a Spell is being created for a new blockchain, a folder for the new blockchain should be created. The guide then explains that three files need to be created: a `.sql` file for the Spell's logic, a `_schema.yml` file to define the Spell's purpose and add generic tests, descriptions, metadata, etc., and a `_sources.yml` file with any project-specific table dependencies. The guide provides an example of the file structure for a Spell folder. 

The guide also explains the naming convention for Spell files. Schema files are named `[project_name]_[blockchain]_schema.yml`, sources files are named `[project_name]_[blockchain]_sources.yml`, and SQL files for Spells are named `[project_name]_[blockchain]_[spell_name].sql`. 

The guide then provides an example of a specific v1 migration example where three additional `.sql` files are needed for a Spell called `keep3r_network_ethereum_view_job_log.sql`. The guide explains that these files are needed because the original `view_job_log.sql` V1 Abstraction has two `FROM` statements that reference two other files that are also abstractions that need to be converted into Spells. The guide also explains that a recursive check needs to be done to see if those abstractions depend on any other abstractions that have yet to be migrated to Spells. 

Overall, this technical guide provides a clear and detailed explanation of how to set up the file structure for Spells in the Dune Docs project. It provides examples and naming conventions for the different types of files needed for Spells and explains how to handle dependencies between Spells.
## Questions: 
 1. What is the purpose of the app and how does it relate to blockchain technology?
   Answer: The app technical guide is focused on setting up a file structure for SQL, schema, and source files for a project that involves blockchain networks. A blockchain SQL analyst might want to know more about the specific use case of the project and how it utilizes blockchain technology.

2. What are the naming conventions for the files and folders in the app?
   Answer: The app technical guide provides specific naming conventions for the files and folders used in the project. A blockchain SQL analyst might want to know more about these conventions to ensure consistency and organization in their work.

3. How does the app handle dependencies between different files and abstractions?
   Answer: The app technical guide explains how to identify and handle dependencies between different files and abstractions in the project. A blockchain SQL analyst might want to know more about this process to ensure that all necessary files and abstractions are properly migrated to Spells.