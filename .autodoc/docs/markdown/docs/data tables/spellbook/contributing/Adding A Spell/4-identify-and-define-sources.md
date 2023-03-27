[View code on GitHub](https://dune.com/blob/master/data tables\spellbook\contributing\Adding A Spell\4-identify-and-define-sources.md)

This app technical guide covers the process of identifying and defining sources in the Dune Docs project. The guide provides instructions on how to complete the `_sources.yml` file, which is used to specify the sources of data for the project. The file is formatted using YAML syntax, and it contains information about the version of the engine used, the name and description of the source, and the tables associated with the source.

The guide explains how to identify the sources that need to be named by searching for `FROM` statements in the V1 abstractions that are being migrated. The tables mentioned in these statements that are not abstractions are the ones that need to be included in the `_sources.yml` file. The guide provides an example of how to create a `keep3r_network_ethereum_sources.yml` file, which includes a description of the Keep3r Network, a marketplace for posting and accepting jobs to help run decentralized infrastructure. The file lists the tables associated with the source, such as `Keep3r_evt_LiquidityAddition` and `Keep3r_evt_KeeperWork`.

Overall, this guide is essential for developers working on the Dune Docs project, as it provides clear instructions on how to identify and define sources of data. By following the steps outlined in the guide, developers can ensure that the project is properly structured and that the data is accurately represented.
## Questions: 
 1. What is the purpose of the `_sources.yml` file in the Dune Docs project?
    
    The `_sources.yml` file in the Dune Docs project is used to identify and define sources for the project's data.

2. How are the sources formatted in the `_sources.yml` file?
    
    The sources in the `_sources.yml` file are formatted with a name, a one-line description, and a list of tables.

3. How can a blockchain SQL analyst determine which sources to name in the `_sources.yml` file?
    
    A blockchain SQL analyst can determine which sources to name in the `_sources.yml` file by searching for `FROM` statements in the V1 abstractions being migrated and looking for all tables mentioned that are not abstractions.