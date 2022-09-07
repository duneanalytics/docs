---
title: Reformatted Transfers
---

Our base table records the transfer amount to and from an account. To make it easier to sum of transfers, we munge this into a union of sent txns and received txns.

Additionally, WETH requires special handling given the additional functions of deposit and withdrawal. This means we need to add `zeroex_ethereum.weth9_evt_deposit` as a source like we did for `erc20_ethereum.evt_transfer` above.

Similar to a source, the model is defined in a YAML file. This is where things like the description, tests, and metadata are defined. This is also where we track “contributors”. So make sure you get your clout and add your handle when writing or editing a spell. Then you’ll be credited for your contribution in the [documentation](https://spellbook-docs.dune.com/#!/overview).

In the JINJA config block, we define that the alias for this view is `erc20`. Without this alias, the table name would default to the file name. The schema name for this view is defined in the [dbt\_project.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/dbt\_project.yml) file in the root of the Spellbook project. Schema’s are defined there by the directory structure. The name of this view would be transfers\_ethereum.erc20 given the current structure.

Note: we're generally against using SHOUT CASE, that’s what IDEs are for. Sue us.

[transfers\_ethereum\_erc20.sql](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/erc20/transfers\_ethereum\_erc20.sql)

```sql
{{ config(materialized='view', alias='erc20') }}

with
    sent_transfers as (
        select
            'send' || '-' || evt_tx_hash || '-' || evt_index || '-' || `to` as unique_tx_id,
            `to` as wallet_address,
            contract_address as token_address,
            evt_block_time,
            value as amount_raw
        from
            {{ source('erc20_ethereum', 'evt_transfer') }}
    )

    ,
    received_transfers as (
        select
        'receive' || '-' || evt_tx_hash || '-' || evt_index || '-' || `from` as unique_tx_id,
        `from` as wallet_address,
        contract_address as token_address,
        evt_block_time,
        - value as amount_raw
        from
            {{ source('erc20_ethereum', 'evt_transfer') }}
    )

    ,
    deposited_weth as (
        select
            'deposit' || '-' || evt_tx_hash || '-' || evt_index || '-' || dst as unique_tx_id,
            dst as wallet_address,
            contract_address as token_address,
            evt_block_time,
            wad as amount_raw
        from
            {{ source('zeroex_ethereum', 'weth9_evt_deposit') }}
    )

    ,
    withdrawn_weth as (
        select
            'withdrawn' || '-' || evt_tx_hash || '-' || evt_index || '-' || src as unique_tx_id,
            src as wallet_address,
            contract_address as token_address,
            evt_block_time,
            - wad as amount_raw
        from
            {{ source('zeroex_ethereum', 'weth9_evt_withdrawal') }}
    )
    
select unique_tx_id, 'ethereum' as blockchain, wallet_address, token_address, evt_block_time, amount_raw
from sent_transfers
union
select unique_tx_id, 'ethereum' as blockchain, wallet_address, token_address, evt_block_time, amount_raw
from received_transfers
union
select unique_tx_id, 'ethereum' as blockchain, wallet_address, token_address, evt_block_time, amount_raw
from deposited_weth
union
select unique_tx_id, 'ethereum' as blockchain, wallet_address, token_address, evt_block_time, amount_raw
from withdrawn_weth
```

[transfers\_ethereum\_schema.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/models/transfers/ethereum/transfers\_ethereum\_schema.yml)

```yaml
models:
 - name: transfers_ethereum_erc20
   meta:
     blockchain: ethereum
     sector: transfers
     project: erc20
     contibutors: soispoke, dot2dotseurat
   config:
     tags: ['transfers', 'ethereum', 'erc20', 'soispoke', 'dot2dotseurat']
   description: "ERC20 Token Transfers on Ethereum. This table is updated every 15 minutes."
   columns:
     - name: unique_transfer_id
       description: "Unique transfer ID (used for testing for duplicates)"
       tests:
         - unique
     - &blockchain
       name: blockchain
       description: "Blockchain"
     - &wallet_address
       name: wallet_address
       description: "Wallet address of sender or receiver. If amount is negative, wallet address is the sender's."
     - &token_address
       name: token_address
       description: "Contract address for token"
     - &evt_block_time
       name: evt_block_time
       description: "Timestamp for block event time in UTC"
     - &amount_raw
       name: amount_raw
       description: "Raw amount of ERC20 token held *before* taking into account token decimals"

```

[dbt\_project.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/dbt\_project.yml)

```yaml
transfers:
 +schema: transfers
 +materialized: view
 ethereum:
   +schema: transfers_ethereum
   +materialized: view
```
