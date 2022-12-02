# Spellbook Contribution Guidelines

Spellbook is a powerful tool for creating well-organized and accurate data abstractions at scale.

Built using [dbt-core](https://docs.getdbt.com/docs/introduction) (data build tool), Spellbook mixes SQL with JINJA templating to enable us to build as a team and community using data engineering best practices.

To adhere to those best practices, dbt's requirements, and facilitate contribution and collaboration across our community, we have a few requirements we'll ask you to follow.

We've created these docs to help you understand those conventions and structures as well as some of the why behind them in order to help you successfully build Spells and get your PRs approved faster!

Read on to learn about the different types of Spellbook contributions and General Guidelines.

If you're looking for guidelines on a specific type of Spellbook contribution, see these pages:

\<div class="cards grid" markdown\>

- [Adding new Tokens or Price Feeds (Contributing to Static Views)](../spellbook/contribution-guidelines/contributing-static-views.md)

- [Contributing with new Spells](../spellbook/contribution-guidelines/contributing-spells.md)

\</div\>

And as always, if you have questions reach out in the [#spellbook](https://discord.com/channels/757637422384283659/999683200563564655)[Discord](https://discord.com/channels/757637422384283659/999683200563564655)[Channel](https://discord.com/channels/757637422384283659/999683200563564655) - someone from the community or team is always happy to help!

## Types of Spellbook Contributions

Spellbook consists of two primary data structures, each of which has different guidelines for contribution.

### Static Views

Static views are our way of maintaining reference datasets in Spellbook. We currently have two major types.

#### Token Metadata

Token Metadata views store basic metadata such as symbol, decimals, etc.

They have slightly different schemas depending on the token standard (e.g. ERC20, ERC721).

#### Token Prices

Token Prices views are configuration files to our internal pricing jobs that fetch prices for our prices table.

Learn more about the [guidelines for contributing Static Views here](.../spellbook/contribution-guidelines/contributing-static-views.md)!

### Spells

Spells are the abstracted datasets our community and team build on top of raw blockchain data - they're a core part of what makes Dune the best source for blockchain data and tool for analysis!

Each Spell is a dbt model on the Spellbook repository ([browse our list of existing Spells here](https://dune.com/spellbook#!/overview)).

All Spells have the same general structure with slight differences depending on the type of materialization.

In general, every time you build an entirely new spell, it's going to be as a view. In case you are extending an existing sector spell with new projects (e.g. adding a new dex to dex.trades) you'll be following that spell's materialization strategy (usually incremental). If you know what you're doing, you can use the type that best matches your application.

#### Views

Views are the most common and default type of Spell. They're executed every time they're queried.

#### Incremental Tables

Used for large tables like `dex.trades`, Spells materialized as Incremental Tables are stored on disk, records from new blocks are appended regularly every hour.

#### Tables

Tables are relatively rare as the data is stored on disk and the Spell is executed on the whole blockchain - making them computationally intensive and naturally slower to run.

Learn more about the guidelines for contributing Spells here!

## General Spellbook contribution guidelines

In order to best facilitate community contributions while adhering to dbt's requirements and keeping Spellbook manageable for our team, we have a few guidelines that we'll ask you to follow.

### Directory format and naming conventions

Spellbook is a repository where many people contribute and collaborate, so to keep it easily understandable for everyone, we have some rather strict naming and directory organization conventions.

Spells are organized under `models` (all spells are just dbt models) using the following structure:

- Sectors (DEX, NFT, etc.) have their own spells under `/models/\<sector\>`
- Project spells `/models/\<project\>/\<blockchain\>`
- Most spells are built bottom-up, starting from a single project version in a single chain and merging all the way up to a sector, with there being four total levels of the hierarchy
  - Project version on one blockchain
  - Project on one blockchain
  - Project on all blockchains
  - Sector on all blockchains

We have a few special cases for storing static datasets, they are:

- Token metadata views live under `/models/tokens/\<blockchain\>`
  - Files follow the convention `tokens_\<blockchain\>_\<subset\>.sql` and contain metadata for tokens of a subset of tokens (e.g. erc20, NFTs, Rebasing tokens)
- Price feeds metadata live on `/models/prices/prices_tokens.sql`

## Anatomy of a spell

Spells are dbt models and as such are ultimately `select` queries. Each Spell's SQL file has to contain a select statement and follow a few additional rules:

Querying data from other parts of Dune is must be done using [Jinja syntax](https://docs.getdbt.com/docs/build/jinja-macros):

- **sources** are decoded and raw tables on Dune, they should be addressed with `{{ source('ethereum', 'transactions' }}` and, in case of decoded tables, should be referenced on the `sources.yml` file (see details [here](#_ht3y58fudwir))
- **refs** are all the other spells created in spellbook, should be addressed with the `ref` function e.g. `{{ ref('uniswap_ethreum_trades') }}`

At the top of each Spell's SQL file you'll find a config block. Its contents will vary depending on the type of materialization but at the very least:

- The config block should assign an alias to the view.
- If the view should be available on the Dune Data Explorer, a post\_hook must be added.

- There will be additional requirements depending on the type of materialization you use (see details for [incremental](#_526g7qsxh9q)[table](#_526g7qsxh9q) and [table](#_9gqiuknnb44))

### Metadata Files

The power of dbt lies in automatically performing many of the tasks our Wizard ancestors had to code by hand in ETL software.

To use this power, though, dbt needs to know (or be able to infer) details about our spells that is not contained in the SQL itself. That's where the yml metadata files come in.

dbt starts working based on the parent config file `dbt_project.yml`. Any new spell we add has to be reflected in [project.yml](https://github.com/duneanalytics/spellbook/blob/main/dbt_project.yml) under `models \> spellbook`.

In every Spell you will find two very important .yml files:

- \*\_sources.yml contains metadata about the sources required by the Spell. This includes any Raw or Decoded Table that you call using `source()` Jinja function.
- \*\_schema.yml contains metadata about the models included in the Spell. As long as the schema file is referenced by dbt\_project.yml, you can consolidate multiple models into a single schema file.

The content of these files is usually fairly simple, although the options are endless. If you want to understand what to use for your case, it may be best to refer to examples of similar Spells. Explore all our existing Spells in the [Spellbook Model docs](https://spellbook-docs.dune.com/#!/overview).

### Testing

The Dune community and team are building the world's best blockchain dataset. To ensure our data is reliable for everyone, all Spellbook contributions need to undergo a certain level of testing.

The level of testing a Spell needs depends on quite a few factors so there's no one-rule-fits-all here.

Generally, the more the following are true, the more a Spell will need to be tested:

- The Spell is upstream of a large / heavily used dataset (e.g. [nft.trades](https://dune.com/spellbook#!/model/model.spellbook.nft_trades))
- The underlying contracts are complex or have many edge cases (e.g. [OpenSea v1](https://dune.com/spellbook#!/model/model.spellbook.opensea_trades))
- The logic of the Spell is relatively complex (e.g. [hashflow](https://dune.com/spellbook#!/source/source.spellbook.hashflow_ethereum.pool_evt_trade))
- The Spell is materialized as table / incremental table

Tests can take one of three forms:

#### Unit tests

Unit tests are the most basic form of test, made with a simple SQL query that returns results in case of failure.

Notes:

- Tests should be their own sql file under the tests directory
- Naming convention is: `/tests/\<protocol\>/\<blockchain\>/\<test_case\>.sql`

See an example [here!](https://github.com/duneanalytics/spellbook/pull/1767/files#diff-1fcf4cfb32cd74212ac86f8f2b78193d8859710ee160d6cf8dc7554615bce50b)

#### Seed tests

Seed tests are perhaps the most powerful and intuitive tests we have, as they can be easily extended to cover edge cases discovered after the Spell is merged.

To use seed tests, you need to:

- Define a generic test ([see example here](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-3f43ced7ce642ed61f0d4b84a578d7e71d0d2ae559b4c8a84c0db582b84c7532)) if it's not defined already
- Generate a seed file with the test cases populated from a block explorer or similar ([example](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-6b4cf60192795ebd65cc95915d76382afe11ffed1507e8e3c13902bb57c19c51))
- Instantiate the test in the schema.yml file with the corresponding inputs ([example](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-d0ac6f4db1670a3760a2895f7e2c5db7d3a4c2c9e1ab3de5391e23bc42721cfaR35))

#### Generic tests

Spellbook has a series of generic tests that can be applied at the column level or at the table level.

Some of the more common examples:

- Column tests
  - _unique\*_
  - _not\_null\*_
  - _accepted\_values\*_
  - [is\_unique\_filtered](https://github.com/duneanalytics/spellbook/blob/main/tests/generic/is_unique_filtered.sql)
- Table tests
  - [dbt\_utils.unique\_combination\_of\_columns](https://github.com/dbt-labs/dbt-utils/blob/main/macros/generic_tests/unique_combination_of_columns.sql)
- Many other generic tests can be found under:
  - [dbt-utils generic tests package](https://github.com/dbt-labs/dbt-utils/tree/main/macros/generic_tests)
  - [spellbook generic tests](https://github.com/duneanalytics/spellbook/tree/main/tests/generic)

(\*) Included with dbt core

# Contributing Static Views

## Token metadata

If you're adding new token metadata to existing blockchains, you can follow this pattern.

Before submitting your PR, please make sure that:

- Contract addresses are lowercase, or that `lower(contract_address)` is applied at the last select statement
- Ensure no commas at the end of the view (if using right commas like a sociopath) or at the beginning (if using left commas like a well adapted member of society)
- Ensure the schema.yml file for this metadata list contains the right tests:
  - Contract address field is tested for uniqueness
  - Fields with a subset of accepted values have a test to that end (e.g. token standard for NFTs)

???? If you need to create a new model

In case you need a new model to host token metadata (e.g. for a new blockchain), you should ensure that:

  - New directory created in models/tokens/\<blockchain\>
  - Add directory to `dbt_project.yml` file
    - Ensure default schema & materialization applied following the naming standards
  - Follow model naming standard `tokens_\<blockchain\>_\<sector\>`
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

# Contributing Spells

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

As you will notice below, these can get quite complex. While understanding the basics of incremental materialization is not rocket science, the details below can get daunting. We recommend building spells as views first, and turning them into incremental tables when they gather traction or as a second step (unless this is a required practice for the sector like in the case of dex.trades)

- **Basics**
  - Use Jinja syntax for 'is\_incremental' and 'not is\_incremental' logic
  - Leverage jinja variables for reusable hardcoded values throughout the model
    - Common use case is "project start date" to filter base tables from that date forward on initial build / any future rebuilds
    - [https://github.com/duneanalytics/spellbook/pull/1472/files#diff-8be4351b64f13bdb3ced1d5365aa0de0fb03ecafcbeb1540561d00998748a1cbR16](https://github.com/duneanalytics/spellbook/pull/1472/files#diff-8be4351b64f13bdb3ced1d5365aa0de0fb03ecafcbeb1540561d00998748a1cbR16)
  - Model config block setup
    - Partition by column which makes most sense to downstream table usage in filters & joins – e.g. block\_date in dex trades to filter certain timeframes, similar to base tables partition strategy
    - Unique key supplied as an array to handle multiple columns
      - _ **Note** _: sector-level spells should be able to apply the same values across all spells – i.e. all dex trades models thus far use the same unique keys

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
