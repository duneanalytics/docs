---
title: Tests
---

The Dune community and team are building the world's best blockchain dataset. To ensure our data is reliable for everyone, we're striving for test-driven development.

That means we think about what results we want from our Spell before we write it, then we write tests that will pass if those results match our output. 

Writing [tests](https://docs.getdbt.com/docs/building-a-dbt-project/tests) before I write my spell? What is this software engineering? Is this language even Turing Complete?!

The level of testing a Spell needs depends on quite a few factors so there's no one-rule-fits-all here.

Generally, the more the following are true, the more a Spell will need to be tested:

- The Spell is upstream of a large / heavily used dataset (e.g. [nft.trades](https://dune.com/spellbook#!/model/model.spellbook.nft_trades))
- The underlying contracts are complex or have many edge cases (e.g. [OpenSea v1](https://dune.com/spellbook#!/model/model.spellbook.opensea_trades))
- The logic of the Spell is relatively complex (e.g. [hashflow](https://dune.com/spellbook#!/source/source.spellbook.hashflow_ethereum.pool_evt_trade))
- The Spell is materialized as table / incremental table

Tests can take one of three forms:

## Unit tests

Unit tests are the most basic form of test, made with a simple SQL query that returns results in case of failure.

Notes:

- Tests should be their own sql file under the tests directory
- Naming convention is: `/tests/\<protocol\>/\<blockchain\>/\<test_case\>.sql`

See an example [here!](https://github.com/duneanalytics/spellbook/pull/1767/files#diff-1fcf4cfb32cd74212ac86f8f2b78193d8859710ee160d6cf8dc7554615bce50b)

## Seed tests

Seed tests are perhaps the most powerful and intuitive tests we have, as they can be easily extended to cover edge cases discovered after the Spell is merged.

To use seed tests, you need to:

- Define a generic test ([see example here](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-3f43ced7ce642ed61f0d4b84a578d7e71d0d2ae559b4c8a84c0db582b84c7532)) if it's not defined already
- Generate a seed file with the test cases populated from a block explorer or similar ([example](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-6b4cf60192795ebd65cc95915d76382afe11ffed1507e8e3c13902bb57c19c51))
- Instantiate the test in the schema.yml file with the corresponding inputs ([example](https://github.com/duneanalytics/spellbook/pull/1864/files#diff-d0ac6f4db1670a3760a2895f7e2c5db7d3a4c2c9e1ab3de5391e23bc42721cfaR35))

## Generic tests

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


## How to define a unit test for your Spell

If you are having trouble imagining what the output of your Spell should look like, you might want to go back to data modelling.

Writing a good unit test requires creativity and a little grit. You need to find a way to validate some of your output which might require some manual calculations.

For example, Etherscan [token check](https://etherscan.io/tokencheck-tool) will return a token balance for a given wallet address, contract address, and date. We can manually record results for a handful of tests cases, either in a CSV file to be uploaded as a dbt [seed](https://docs.getdbt.com/docs/building-a-dbt-project/seeds) or as plain values in the unit test itself. Another option could be using your wallet to track function calls and calculating what the output of the Spell would be just for that wallet.

These tests do not need to be particularly comprehensive. They should be added whenever someone is making a substantive change to the model in the future. The main goal here is to first ensure your model is likely correct and prevent regressions in the future.

Tests should return zero rows to pass. You can get creative, there’s no set way to write the test. One way I like to write tests against individual values is to compare values in a `case when` statement. I hard code in values that I compare to my final model.

The “ref” should be the file name for your intended spell, e.g. `{{ ref('balances_ethereum_erc20_day' )}}.` A ref is how we reference other Spells or models in the DBT project.

You don’t need the model written at this point, just decide on the file name. You will run the test after you finish your Spell. Unless you want to try running your test now to confirm it will fail 😉.

```sql
WITH unit_test1
    AS (SELECT CASE
                 WHEN amount == 100 THEN TRUE
                 ELSE FALSE
               END AS test
        FROM   {{ ref('balances_ethereum_erc20_day' )}}
        WHERE  wallet_address = '0x8de61aeacd24d2865a4fb471b8e746b02ef4e346'
               AND contract_address =
                   '0x00000000000045166c45af0fc6e4cf31d9e14b9a'
               AND DATE = '2022-06-27 00:00'),
    unit_test2
    AS (SELECT CASE
                 WHEN token == 'ONT'
                      AND amount == 7 THEN TRUE
                 ELSE FALSE
               END AS test
        FROM   {{ ref('balances_ethereum_erc20_day' )}}
        WHERE  wallet_address = '0x01bcb7117f00c4d3141ccab2432c7ae3bd5b00d3'
               AND contract_address =
                   '0x0000000000004946c0e9f43f4dee607b0ef1fa1c'
               AND DATE = '2022-06-27 00:00')
SELECT *
FROM   (SELECT *
       FROM   unit_test1
       UNION
       SELECT *
       FROM   unit_test2)
WHERE  test = FALSE
```