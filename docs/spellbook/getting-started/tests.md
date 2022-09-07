---
title: Tests
---

How to define a unit test for your spell.

Writing a [test](https://docs.getdbt.com/docs/building-a-dbt-project/tests) before I write my spell? What is this software engineering? Is this language even Turing Complete?!

We are striving for test-driven development. That means, we think about what results we want from our spell before we write it. Then, we write a test that will pass if those results match our output. If you are having trouble imagining what the output of your spell should look like, you might want to go back to data modelling.

Writing a good unit test requires creativity and a little grit. You need to find a way to validate some of your output which might require some manual calculations.

For example, Etherscan [token check](https://etherscan.io/tokencheck-tool) will return a token balance for a given wallet address, contract address, and date. We can manually record results for a handful of tests cases, either in a CSV file to be uploaded as a dbt [seed](https://docs.getdbt.com/docs/building-a-dbt-project/seeds) or as plain values in the unit test itself. Another option could be using your wallet to track function calls and calculating what the output of the spell would be just for that wallet.

![Etherscan token balance check](https://lh4.googleusercontent.com/EFymwYMt60l6zdbQHhmxV7c3FZ2RHSPjT0SIux1pdk0maghfXn1AyzfIT0b260VU-Hmol5Phm6QSWEROVP74fRqbcFYf2hZPjBDneyISwmjkpYF\_-DPYjAZXfKKQ2iVENYhJq3A6iGegSuggMf8)

These tests do not need to be particularly comprehensive. They should be added whenever someone is making a substantive change to the model in the future. The main goal here is to first ensure your model is likely correct and prevent regressions in the future.

Tests should return zero rows to pass. You can get creative, there’s no set way to write the test. One way I like to write tests against individual values is to compare values in a `case when` statement. I hard code in values that I compare to my final model.

The “ref” should be the file name for your intended spell, e.g. `{{ ref('balances_ethereum_erc20_day' )}}.` A ref is how we reference other spells or models in the DBT project.

You don’t need the model written at this point, just decide on the file name. You will run the test after you finish your spell. Unless you want to try running your test now to confirm it will fail 😉.

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
