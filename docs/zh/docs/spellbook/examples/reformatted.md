---
title: 重新更改格式的转账
---

我们的基础数据表记录了一个账户的转账进出数额。为了便于对转账数额进行汇总，我们将其合并为发送交易和接收交易的集合。

此外，鉴于存款和提款的额外功能，WETH 需要特殊处理。这意味着我们需要添加 `zeroex_ethereum.weth9_evt_deposit`作为数据源，就像我们在上面为 `erc20_ethereum.evt_transfer` 做的那样。

与源文件类似，模型被定义在 YAML 文件中。这是定义描述、测试和元数据等内容的地方。这也是我们追踪"贡献者"的地方。因此，为了确保您获得应有的影响力，请在编写或编辑魔法时添加您的名缀。然后您的贡献会被记入在[文档](https://spellbook-docs.dune.com/#!/overview)中。

在 JINJA 配置块中，我们定义这个视图的别名是 `erc20`。如果没有这个别名，数据表名称将默认为文件名。这个视图的架构名称在魔法书项目根目录的 [dbt\_project.yml](https://github.com/duneanalytics/spellbook/blob/master/spellbook/dbt\_project.yml) 文件中定义。架构是由目录结构在那里定义的。考虑到当前的结构，这个视图的名称应该是 transfers\_ethereum.erc20。

注意：我们基本上反对使用 SHOUT CASE（大写），那是 IDEs 用的。不许反对。

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
