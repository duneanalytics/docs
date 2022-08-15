# March 2020



Big release on the data front this month.

#### Denormalization of `block_time` and `block_number` <a href="#denormalization-of-block_time-and-block_number" id="denormalization-of-block_time-and-block_number"></a>

We’ve added `block_time` and `block_number` to all decoded events and calls, with names `evt_block_time`, `evt_block_number` and `call_block_time`, `call_block_number` respectively. This will eliminate the most painful joins on the platform, joining with `ethereum.transactions` in order to get a time dimension into your queries.

Where previously would need to do

```
SELECT date_trunc('day', tx.block_time), count(*)
FROM uniswap."Exchange_ev t_TokenPurchase" tp
INNER JOIN ethereum.transactions tx ON tp.evt_tx_hash = tx.hash
GROUP BY 1;
```

in order to get the number of daily `TokenPurchase`-events on Uniswap, you can now simply do

```
SELECT date_trunc('day', evt_block_time), count(*)
FROM uniswap."Exchange_evt_TokenPurchase"
GROUP BY 1;
```

eliminating a painful and costly join. Joining across two decoded tables can also be done without involving any of the `ethereum`-tables by using `evt_block_number` or `call_block_number`.

#### Decoding events without parameters <a href="#decoding-events-without-parameters" id="decoding-events-without-parameters"></a>

We’re also “decoding” events that are emitted without parameters. These events have their own tables, but only include Dune-added fields i.e.:

| Column             | Type          |
| ------------------ | ------------- |
| `contract_address` | `bytea`       |
| `evt_tx_hash`      | `bytea`       |
| `evt_index`        | `bigint`      |
| `evt_block_time`   | `timestamptz` |
| `evt_block_number` | `bigint`      |

#### Decoding call outputs <a href="#decoding-call-outputs" id="decoding-call-outputs"></a>

We’ve added function return values to decoded `call` tables. Whenever a function has a named return value it will be decoded into `output_{{name}}`, and when it is not named it will be decoded into `output_{{i}}` where `i` is a counter that starts at 0. Consider the following case, counting success and error codes for calls to the Compound CERC20 `mint` function:

```
SELECT output_0, count(*) 
FROM compound_v2."cErc20_call_mint" 
WHERE call_success 
GROUP BY 1;
```

#### traces.success <a href="#tracessuccess" id="tracessuccess"></a>

**TLDR**: we’ve added a `success` field to `ethereum.traces` that you can use to figure out if an exact call was successful. Useful for e.g. calculating balances. Here’s an example:

```
SELECT sum(amount)                                                         
FROM (                                                                     
    SELECT address, sum(amount) / 1e18 as amount                           
    FROM (                                                                 
        SELECT "from" AS address, -value AS amount                         
         FROM ethereum.traces                                              
         WHERE "from" = '\x390435245F2f95f7443eBb045357DA743E9A65a4'       
         and success = true                                                
    UNION ALL                                                              
        SELECT "to" AS address, value AS amount                            
         FROM ethereum.traces                                              
         WHERE "to" = '\x390435245F2f95f7443eBb045357DA743E9A65a4'         
         AND success = true                                                
    UNION ALL                                                              
        SELECT "from" AS address, -gas_used * gas_price as amount          
        FROM ethereum.transactions                                         
        WHERE "from" = '\x390435245F2f95f7443eBb045357DA743E9A65a4'        
    ) t                                                                    
    group by 1                                                             
) a                                                                        
;
```

**Longer Story**: Dune ingests transaction traces from Parity OpenEthereum. OpenEthereum returns a tree-like datastructure of function call traces, where some can have a non-null `error` field. Where previously we ingested the traces more or less _as is_, today we’ve added a `success` field to `ethereum.traces`. This `success` field is `true` for a given trace if no trace above it in the trace hierarchy has a non-null `error` field.

It came to our attention that if a _parent_ trace-entry has a non-null `error` field, the _child_ call is considered failed in the EVM as well. Previously in Dune, in order to correctly assess whether or not a given function call’s state change was included in the blockchain you would’ve needed to write a slightly complex query to check if any traces in the same branch of the trace tree had an error. With the addition of the `success` field today, this has become much easier.

Note that the field `tx_success` field denotes the success of the transaction as a whole, and that a `true` `tx_success`-field, does not necessarily mean that every function call in the transaction has a `true` `success` field. Here are the potential combinations

| tx\_success | sucess  |
| ----------- | ------- |
| `true`      | `true`  |
| `true`      | `false` |
| `false`     | `false` |

As you can see a call can be _not successful_ in a _successful_ transaction, but can not be _successful_ in a _not successful_ transaction…

Also note that where previously the field `call_success` on decoded tables where calculated as `traces.tx_success && !traces.error`, it is now directly copied from `traces.success`.

#### Postgresql 12.2 <a href="#postgresql-122" id="postgresql-122"></a>

Upgraded the databases to postgresql 12.2. Changelog [here](https://www.postgresql.org/docs/current/release-12-2.html).

#### Misc <a href="#misc" id="misc"></a>

Renamed some curvefi-contracts:

| schema  | name         | Address                                    |
| ------- | ------------ | ------------------------------------------ |
| curvefi | compound     | 0xe5fdbab9ad428bbb469dee4cb6608c0a8895cba5 |
| curvefi | usdt         | 0x52ea46506b9cc5ef470c5bf89f17dc28bb35d85c |
| curvefi | y            | 0x45f783cce6b7ff23b2ab2d70e416cdb7d6055f51 |
| curvefi | compound\_v2 | 0x2e60cf74d81ac34eb21eeff58db4d385920ef419 |
| curvefi | busd         | 0x79a8c46dea5ada233abaffd40f3a0a2b1e5a4f27 |
| curvefi | compound\_v3 | 0xa2b47e3d5c44877cca798226b7b8118f9bfb7a56 |

Moved onesplit contracts to their own schema.

| schema   | name     | address                                                |
| -------- | -------- | ------------------------------------------------------ |
| onesplit | OneSplit | 0x2ad672fda8a042c4c78c411bf9d4f1b320aa915a             |
| onesplit | OneSplit | 0xdff2aa5689fcbc7f479d8c84ac857563798436dd             |
| onesplit | OneSplit | 0x0a236b41add0073df05eac5fc8505ad745c\*\*\*\*\*\*7859d |
