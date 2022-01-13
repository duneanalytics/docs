# August 2020



#### Price Provider Switch <a href="#price-provider-switch" id="price-provider-switch"></a>

We’ve changed price providers from Coincap to Coinpaprika, and in turn now have prices for 230+ assets in the `prices.usd` and `prices.layer1_usd` tables! A slight caveat is that while previously we had prices for all minutes up to current time, we now have prices up to 5 minutes before current time.

**New table prices.layer1\_usd**

We’ve moved all assets that are not tokens on Ethereum to their own table `prices.layer1_usd`. This table is partitioned on `symbol` and has `(symbol, minute)` as primary key as before.

```
 Column │           Type           
────────┼──────────────────────────
 minute │ timestamp with time zone 
 price  │ double precision         
 symbol │ text                     
```

#### Changes to prices schema <a href="#changes-to-prices-schema" id="changes-to-prices-schema"></a>

**New column decimals on prices.usd**

We’ve added a new column `decimals` to `prices.usd` so that you can avoid the additional join with `erc20.tokens` for calculating correct volumes.

**New primary key for prices.usd**

Previously `prices.usd` was partitioned on the token `symbol`, and it’s primary key was `(symbol, minute)`. In this release we’ve made a change to this scheme to allow for multiple `contract_address`es to map to the same `symbol`. This could happen e.g. in times where a token migration is happening. `prices.usd` is now partitioned on `contract_address` and it’s primary key is `(contract_address, minute)`.

Note that this might yield some weird results for queries that rely on doing `SELECT minute, price FROM prices.usd WHERE symbol='x'` in certain cases where there are two contracts mapped to the symbol `x` in a time window. You may then receive several rows per minute. It is better to then use the primary key `contract_address` for filtering and joining.

```
      Column      │           Type          
──────────────────┼─────────────────────────
 minute           │ timestamp with time zone
 price            │ double precision        
 decimals         │ smallint                
 contract_address │ bytea                   
 symbol           │ text                    
```
