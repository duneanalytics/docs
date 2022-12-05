---
title: Contributing Spells
description: Here are the guidelines for adding new Spells to Spellbook!
---

Here are the guidelines for adding new Spells to Spellbook!

Remember there are 3 types of materialization for Spells:

- **Views** are the most common and default type of Spell; their SQL is executed every time they're queried.
- **Incremental Tables** are used for large tables like `dex.trades`; they're stored on disk with records from new blocks appended every hour.
- **Tables** are relatively rare as the data is stored on disk and the Spell is executed on the whole blockchain, making them computationally intensive and naturally slower to run.

Below you'll find the specific guidelines for each materialization type.

## Views

- Add a new directory following the pattern: `models/\<project\>/\<blockchain\>` (e.g. `uniswap/ethereum`)
  - Follow the pattern '\<project\>\_\<blockchain\>\_\<alias\>' for naming the model
- Add the model to dbt\_project.yml file
  - Replicate the same defaults used on all other models (see [example](https://github.com/duneanalytics/spellbook/blob/f9387abb67e70d6fbc51b8843046732ee55fad0c/dbt_project.yml#L31))
- Ensure you have a config block at the beginning of the file, with, at minimum:

```python
{{ config( 
  schema = 'uniswap\_v2\_ethereum', # ONLY WHEN CONTRACT HAS MULTIPLE VERSIONS, override the schema name from dbt\_project yaml file with contract version included (otherwise remove this property)
  alias = 'trades', # Always apply an alias to the table
  post\_hook='{{ expose\_spells(\'["ethereum"]\',
    "project",
    "uniswap\_v2",
    \'["jeff-dude", "markusbkoch", "masquot", "milkyklim", "0xBoxer", "mewwts", "hagaetc"]\') }}'# Post hook to display the model in Dune UI
  ) 
}}
```

- Make sure all of your references to sources / tables is either:
  - `source()` jinja function for raw and decoded tables
  - `ref()` jinja function for any model within spellbook
  - nly use plain references for CTEs defined within the same sql file
- Make sure you create all the metadata files needed:
  - Ensure your schema file contains all views added by your spell
  - Ensure all columns are referenced and have a name and, if the content is not obvious from the name, a description
  - In case you have many instances of the same column, you can use the **&\*** pattern to [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (see example here: [definition](https://github.com/duneanalytics/spellbook/blob/f9387abb67e70d6fbc51b8843046732ee55fad0c/models/uniswap/ethereum/uniswap_ethereum_schema.yml#L25) and [reuse](https://github.com/duneanalytics/spellbook/blob/f9387abb67e70d6fbc51b8843046732ee55fad0c/models/uniswap/ethereum/uniswap_ethereum_schema.yml#L119))
- Sources YAML file created to contain source decoded tables/views used in model(s)
- Ensure jinja refs/sources don't contain extra parentheses (messes with sql parsers downstream)
  - [https://github.com/duneanalytics/spellbook/pull/1599](https://github.com/duneanalytics/spellbook/pull/1599)
- While unit tests are less necessary on views – as they are easier to patch bugs and rebuild – users should be encouraged to add up-front to ensure data quality downstream

## Incremental Table

As you will notice below, these can get quite complex. While understanding the basics of incremental materialization is not rocket science, the details below can get daunting. We recommend building Spells as views first, and turning them into incremental tables when they gather traction or as a second step (unless this is a required practice for the sector like in the case of dex.trades)

- **Basics**
  - Use Jinja syntax for 'is\_incremental' and 'not is\_incremental' logic
  - Leverage jinja variables for reusable hardcoded values throughout the model
    - Common use case is "project start date" to filter base tables from that date forward on initial build / any future rebuilds
    - [https://github.com/duneanalytics/spellbook/pull/1472/files#diff-8be4351b64f13bdb3ced1d5365aa0de0fb03ecafcbeb1540561d00998748a1cbR16](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-8be4351b64f13bdb3ced1d5365aa0de0fb03ecafcbeb1540561d00998748a1cbR16)
  - Model config block setup
    - Partition by column which makes most sense to downstream table usage in filters & joins – e.g. block\_date in dex trades to filter certain timeframes, similar to base tables partition strategy
    - Unique key supplied as an array to handle multiple columns
      - _ **Note** _: sector-level Spells should be able to apply the same values across all Spells – i.e. all dex trades models thus far use the same unique keys

```python
{{ config(
  schema = 'uniswap\_v2\_ethereum', # If contract has multiple versions, override the schema name from dbt\_project yaml file with contract version included
  alias = 'trades', # Always apply an alias to the table
  partition\_by = ['block\_date'], # Partition by the column that makes the most sense
  materialized = 'incremental',
  file\_format = 'delta',
  incremental\_strategy = 'merge',
  unique\_key = ['block\_date', 'blockchain', 'project', 'version', 'tx\_hash', 'evt\_index', 'trace\_address'], # Unique key supplied as an array to handle multiple columns
  post\_hook='{{ expose\_spells(\'["ethereum"]\',
    "project",
    "uniswap\_v2",
    \'["jeff-dude", "markusbkoch", "masquot", "milkyklim", "0xBoxer", "mewwts", "hagaetc"]\') }}'# Post hook to display the model in Dune UI
  )
}}
```

- **Performance & Joins**
  - Prefer Inner join to base tables rather than left join
  - Add condition in inner join to base tables on:
```sql
INNER JOIN {{ source('ethereum', 'transactions') }} tx
  ON tx.hash = dexs.tx\_hash

  {% if not is\_incremental() %}
  AND tx.block\_time \>= '{{project\_start\_date}}' # Define this variable at the top of the file
  {% endif %}

  {% if is\_incremental() %}
  AND tx.block\_time \>= date\_trunc("day", now() - interval '1 week')
  {% endif %}
```
  - If you're joining to prices or token views:
    - Use left join and handle null values in your logic
    - Join on blockchain, as the same contract\_id may repeat across chains

 LEFT JOIN {{ source('prices', 'usd') }} p\_bought # Use left join for prices 
 ON p\_bought.minute = date\_trunc('minute', dexs.block\_time) 
 AND p\_bought.contract\_address = dexs.token\_bought\_address 
 AND p\_bought.blockchain = 'ethereum' # Make sure you join on blockchain 
 {% if not is\_incremental() %} |
 AND p\_bought.minute \>= '{{project\_start\_date}}' |

 {% endif %} |

{% if is\_incremental() %} |
AND p\_bought.minute \>= date\_trunc("day", now() - interval '1 week') |
 {% endif %}
  - Avoid using CTE's whose only role is to filter down a base or decoded table

- **Testing** : When it comes to incremental models, tests are far more necessary. Models are likely to see heavier usage, and correcting errors once the model is merged is an operationally intensive task.

  - Always test uniqueness of the columns used as unique key in the config (example [here](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-7da167e3f4a73d5c5c2e3d245dc8c73c88619f49d08d0fea792a4bd8c54382aeR14))
  - Create (or add to existing) seed file which contains data related to certain use case – i.e. dex trades token bought generic test
    - PR using existing seed ([test declared](https://github.com/duneanalytics/spellbook/pull/1866/files#diff-8ba1908b2679efbd3dc591b730739b0c156cd7fe53a264c85c172ef2762d3205R67), [seed data added](https://github.com/duneanalytics/spellbook/pull/1866/files#diff-09c1b2e11432d6907b7f05a0e73f46488de55e9f905df8d54602cb7173fdba5f))
    - PR creating a new generic seed test ([test created](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-80ca697c58133df93c9963c7a7b1a6f7a97e8c0fbc49c1a71aa7b2011dc7fdc6), [seed created](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-79f59a3f48fe5beee6c8eefd3240ed473ddc5ab5dca950b260abf0fcc6898899), [test declared](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-db47c009edc360c46e6bb2e80efc53cfaa4356bc4fb01d4afb802f46b22e630fR44))
  - Try to think of which cases are likely to break your code (e.g. joining on Token ID for erc721 but creates duplication on erc1155) - **you can send a draft PR and summon other wizards to your aid!**

## Tables

These are going to be relatively rare, since rebuilding them usually requires rerunning them in their entirety, but if you find this is the best implementation for what you're building, follow the guidelines below.

- **Basics**
  - Same checks as [views](#_5gai56xqstcs)
  - Leverage jinja variables for reusable hardcoded values throughout the model
    - Common use case could be address values repeated throughout or a project start date used to filter base tables throughout
  - Model config block setup
    - If contract has multiple versions, override the schema name from dbt\_project yaml file with contract version included
    - Partition by column which makes most sense to downstream table usage in filters & joins – i.e. block\_date in dex trades to filter certain timeframes, similar to base tables partition strategy
    - At minimum, the config should contain the following:
```python
{{ config(
  alias = 'all', # Provide an alias |
  materialized = 'table', # Define materialization
  file\_format = 'delta', # File format is delta
  ...
}}
```

- **Performance & Joins**
  - Inner join to base tables rather than left join
  - Add condition in inner join to base tables on block\_time \>= project\_start\_date variable
    - _ **Note** _: it's important to have a static value for performance gains
  - Add condition in left join to prices or token views on
    - block\_time \>= project\_start\_date variable (use a static value defined at the top of the file)
    - blockchain = '\<blockchain\>' as addresses can be duplicated across blockchains
- **Testing** : When it comes to incremental models, tests are far more necessary. Models are likely to see heavier usage, and correcting errors once the model is merged is an operationally intensive task.

  - Always test uniqueness of the columns used as unique key in the config (example [here](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-7da167e3f4a73d5c5c2e3d245dc8c73c88619f49d08d0fea792a4bd8c54382aeR14))
  - Create (or add to existing) seed file which contains data related to certain use case – i.e. dex trades token bought generic test
    - PR using existing seed ([test declared](https://github.com/duneanalytics/spellbook/pull/1866/files#diff-8ba1908b2679efbd3dc591b730739b0c156cd7fe53a264c85c172ef2762d3205R67), [seed data added](https://github.com/duneanalytics/spellbook/pull/1866/files#diff-09c1b2e11432d6907b7f05a0e73f46488de55e9f905df8d54602cb7173fdba5f))
    - PR creating a new generic seed test ([test created](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-80ca697c58133df93c9963c7a7b1a6f7a97e8c0fbc49c1a71aa7b2011dc7fdc6), [seed created](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-79f59a3f48fe5beee6c8eefd3240ed473ddc5ab5dca950b260abf0fcc6898899), [test declared](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-db47c009edc360c46e6bb2e80efc53cfaa4356bc4fb01d4afb802f46b22e630fR44))
  - Try to think of which cases are likely to break your code (e.g. joining on Token ID for erc721 but creates duplication on erc1155) - **you can send a draft PR and summon other wizards to your aid!**
