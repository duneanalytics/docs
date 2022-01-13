# January 2020

## Postgres 12.1 <a href="#postgres-121" id="postgres-121"></a>

We’ve upgraded the database from postgres 11 to postgres 12.1. This should result in performance improvements across the board.

## ERC20 Transfer and Approval tables <a href="#erc20-transfer-and-approval-tables" id="erc20-transfer-and-approval-tables"></a>

You can now query the `erc20."ERC20_evt_Transfer"` and `erc20."ERC20_evt_Approval"` tables to get decoded token transfers and approvals. These tables should include all events that could be decoded using the ABI of the ERC20 standard. This means that all transfers from all tokens can be queried through this table. The table is large (240M rows at time of writing), so please let us know your experience of the query performance.

`erc20."ERC20_evt_Transfer"` schema:

| Column             | Type      |
| ------------------ | --------- |
| `"from"`           | `bytea`   |
| `"to"`             | `bytea`   |
| `value`            | `numeric` |
| `contract_address` | `bytea`   |
| `evt_tx_hash`      | `bytea`   |
| `evt_index`        | `bigint`  |

`erc20."ERC20_evt_Approval"` schema:

| Column             | Type      |
| ------------------ | --------- |
| `owner`            | `bytea`   |
| `spender`          | `bytea`   |
| `value`            | `numeric` |
| `contract_address` | `bytea`   |
| `evt_tx_hash`      | `bytea`   |
| `evt_index`        | `bigint`  |

Here `contract_address` refers to the contract emmitting the event, i.e. the token address, while `evt_tx_hash` and `evt_index` conveniently lets you join with `ethereum.logs` using a query like

```
SELECT *
FROM erc20."ERC20_evt_Approval" apps
INNER JOIN ethereum.logs 
ON apps.evt_tx_hash = logs.tx_hash AND apps.evt_index = logs.index
LIMIT 100;
```

Also note that you can join these tables with `erc20.tokens` to get human readable token symbols and the number of decimals like

```
SELECT value/10^decimals, tr.*
FROM erc20."ERC20_evt_Transfer" tr 
LEFT JOIN erc20.tokens t
ON t.contract_address = tr.contract_address
WHERE symbol = 'MKR'
LIMIT 10
```

Note though that

**Examples**

**Top token holders**

```
WITH transfers AS (
    SELECT
    evt_tx_hash AS tx_hash,
    tr."from" AS address,
    -tr.value AS amount
     FROM erc20."ERC20_evt_Transfer" tr
     WHERE contract_address = '\x6810e776880c02933d47db1b9fc05908e5386b96' --GNO
UNION ALL
    SELECT
    evt_tx_hash AS tx_hash,
    tr."to" AS address,
    tr.value AS amount
     FROM erc20."ERC20_evt_Transfer" tr 
     WHERE contract_address = '\x6810e776880c02933d47db1b9fc05908e5386b96' --GNO
)
SELECT address, sum(amount/1e18) as balance
FROM transfers
GROUP BY 1
ORDER BY 2 desc
LIMIT 10
```

**Token Balances**

```
WITH transfers AS (
    SELECT
    evt_tx_hash AS tx_hash,
    contract_address AS token_address,
    -tr.value AS amount
     FROM erc20."ERC20_evt_Transfer" tr
     WHERE tr."from" = '\xdeadbeef' -- insert real address here
UNION ALL
    SELECT
    evt_tx_hash AS tx_hash,
    contract_address AS token_address,
    tr.value AS amount
     FROM erc20."ERC20_evt_Transfer" tr 
     WHERE tr."to" = '\xdeadbeef' -- insert real address here
)
SELECT token_address, sum(amount/1e18) as balance
FROM transfers
GROUP BY 1
ORDER BY 2 desc;
```

## Fallback decoding <a href="#fallback-decoding" id="fallback-decoding"></a>

The above tables are generated with a new feature we call “fallback decoding”. Essentially it breaks down to being able to decode logs regardless of the events contract address or contract bytecode. If you know other cases where this decoding can be useful feel free to let us know at [hello@dune.xyz](mailto:hello@dune.xyz)

## Misc <a href="#misc1" id="misc1"></a>

* Data for Gnosis sight, safe and dfusion can now be found in `gnosis_sight`, `gnosis_safe` and `gnosis_dfusion` schemas respectively.
* Synthetix token-contracts now have the correct name `Synthetix` and are found in the `synthetix` schema
* `prices.usd_dai` have been renamed to `prices.usd_sai`, and the symbol changed to `SAI` - we still don’t have `DAI` prices unfortunately, as our price provider has not listed it.
* `prices.usd_rep` now has the correct token address for `REP` for entries after the migration. Previsouly all entries had the old address.
