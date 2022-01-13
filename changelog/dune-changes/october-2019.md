# October 2019

#### New data structure <a href="#new-data-structure" id="new-data-structure"></a>

If you are forking old queries you need to be aware of these changes to you can replace old table and column names with new ones.

#### USD price tables <a href="#usd-price-tables" id="usd-price-tables"></a>

Previously the usd price table was named `coincap."tokens/usd"` this is now changed to `prices.usd` with the fields

```
symbol -- unchanged
contract_address -- previously "asset"
price -- previously "average"
minute -- previously "time"
```

#### Dune generated columns <a href="#dune-generated-columns" id="dune-generated-columns"></a>

We add some data fields to all decoded tables for `calls` and `events`. These are now named `evt_index, evt_tx_hash, contract_address`. Previously these were simplt named `index, tx_hash, address` but we wanted to make it clear that these are added by Dune and not extracted directly from the blockchain.
