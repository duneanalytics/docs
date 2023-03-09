---
title: Contributing Static Views
description: Here are the guidelines for adding new tokens or price feeds using Spellbook Static Views!
---

Here are the guidelines for adding new tokens or price feeds using Spellbook Static Views!

## Token metadata

If you're adding new token metadata to existing blockchains, you can follow this pattern.

Before submitting your PR, please make sure that:

- Contract addresses are lowercase, or that `lower(contract_address)` is applied at the last select statement
- Ensure no commas at the end of the view (if using right commas like a sociopath) or at the beginning (if using left commas like a well adapted member of society)
- Ensure the schema.yml file for this metadata list contains the right tests:
  - Contract address field is tested for uniqueness
  - Fields with a subset of accepted values have a test to that end (e.g. token standard for NFTs)

In case you need a new model to host token metadata (e.g. for a new blockchain), you should ensure that:

  - New directory created in models/tokens/[blockchain]
  - Add directory to `dbt_project.yml` file
    - Ensure default schema & materialization applied following the naming standards
  - Follow model naming standard `tokens_[blockchain]_[sector]`
  - Config block provides
    - alias name for view, to avoid model name being used
    - post-hook to ensure visibility in Dune UI table explorer
  - Schema YAML file created to contain new views
  - Columns match existing blockchain views

## Token prices

If you need a new price feed added to Dune, you can follow this guide. An example of a PR of this type can be found [here](https://github.com/duneanalytics/spellbook/pull/1874/files).

Before sending your PR, make sure that:

- Contract address is lowercase, or view has lower() function applied to the contract address column
- ID is valid and active on coinpaprika
  - You can find it by searching for the symbol on coinpaprika and extracting it from the URL, e.g. https://coinpaprika.com/coin **/wbtc-wrapped-bitcoin/**
  - Ensure the feed is active, this is easiest done by checking the is\_active field on the api response api.coinpaprika.com/v1/coins/ **wbtc-wrapped-bitcoin**
- Ensure that the contract address is the correct one for the
- Validate decimal value & symbol are correct (you can use the coinpaprika API or a block explorer)