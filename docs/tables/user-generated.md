---
title: User Generated Tables
description: >-
  The Schema dune_user_generated is an easy way to construct your own view,
  function or table inside of our database.
---

!!! note
    User generated tables are not yet available on V2.

**Note that these tables are not guaranteed to contain correct data, please use these with caution if you haven't created them yourself.**

**Always save the constructor arguments for your views. Sometimes we have to drop views in order to be able to change some decoding tables or proxy dependencies and you might have to redeploy your view.**

## Use Cases

There is several ways in which you can utilize your own views and tables inside of Dune to make working with your data on Dune even easier.

Your own tables, views and function all have an important part to play in creating content on Dune and make maintenance of your dashboards and queries easier if used correctly.

If you are unfamiliar with tables, views, materialized views and functions please consult the [pgSQL documentation](https://www.postgresqltutorial.com/postgresql-views) or check out our [getting started guide](../getting-started/index.md).

### Storing Information

Sometimes certain references or information that you do need for your data extraction are not properly stored in available tables or stored in many different tables, which would makes the query quite hard to work with. In these cases, you are best off storing the necessary information in a view and referencing that view.

An example of this would be the mapping of certain vault or lending tokens to their respective underlying tokens.

```sql
CREATE OR REPLACE VIEW dune_user_generated.view_test (symbol, contract_address, decimals, underlying_token_address) AS VALUES
('iETH'::text, '\x9Dde7cdd09dbed542fC422d18d89A589fA9fD4C0'::bytea, 18::numeric, '\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2'::bytea),
('yDAI'::text, '\x9D25057e62939D3408406975aD75Ffe834DA4cDd'::bytea, 18::numeric, '\x6B175474E89094C44Da98b954EedeAC495271d0F'::bytea),
('yUSDC'::text, '\xa2609b2b43ac0f5ebe27deb944d2a399c201e3da'::bytea, 6::numeric, '\xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48'::bytea),
('ySUSD'::text, '\x36324b8168f960A12a8fD01406C9C78143d41380'::bytea, 18::numeric, '\x57Ab1ec28D129707052df4dF418D58a2D46d5f51'::bytea),
('yUSDT'::text,'\xa1787206d5b1bE0f432C4c4f96Dc4D1257A1Dd14'::bytea, 6::numeric, '\xdAC17F958D2ee523a2206206994597C13D831ec7'::bytea),
('yCRV'::text,'\x9Ce551A9D2B1A4Ec0cc6eB0E0CC12977F6ED306C'::bytea, 18::numeric, '\x6B175474E89094C44Da98b954EedeAC495271d0F'::bytea),
('yBTC'::text, '\x04EF8121aD039ff41d10029c91EA1694432514e9'::bytea, 8::numeric, '\x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599'::bytea)
```

This table generates a view that you can use to join on your query.

[Look at the table](https://dune.com/queries/41577).

### Aggregating Data

Views can also be used to aggregate the actions of multiple smart contracts into one view that contains all the necessary data.

This is especially useful if you are working with the same dataset over and over and only change the way you display or aggregate the data. That way, instead of having to query for your dataset again and again, you just put it into a view once and then can start referencing that view.

This will allow you to change the base query that constructs your dataset without having to go through multiple different instances of your query. Think about it like splitting your data collection and the actual work/display you do with that data into two different parts that function independently of each other.

Utilizing this will make the maintenance of your dashboards much easier since you can just change the **dune\_user\_generated** view instead of having to go through all queries individually.

A great example of this in action is almost all queries on [this dashboard](https://dune.com/keeganead/cryptoart\_1). The Creator made one base dataset in the **dune\_user\_generated** schema and uses that to base all of his queries on.

Please do note that while this approach works for most cases, views can get very computationally expensive and you might be better off constructing a materialized view or table in our [abstractions](abstractions.md).

This example takes the data from Uniswap\_v3 and standardizes the data for the dex.trades table.

```sql
CREATE OR REPLACE view dune_user_generated.uniswap_v3 as 

    SELECT
        dexs.block_time,
        erc20a.symbol AS token_a_symbol,
        erc20b.symbol AS token_b_symbol,
        token_a_amount_raw / 10 ^ erc20a.decimals AS token_a_amount,
        token_b_amount_raw / 10 ^ erc20b.decimals AS token_b_amount,
        project,
        version,
        category,
        coalesce(trader_a, tx."from") as trader_a, -- subqueries rely on this COALESCE to avoid redundant joins with the transactions table
        trader_b,
        token_a_amount_raw,
        token_b_amount_raw,
        coalesce(
            usd_amount,
            token_a_amount_raw / 10 ^ erc20a.decimals * pa.price,
            token_b_amount_raw / 10 ^ erc20b.decimals * pb.price
        ) as usd_amount,
        token_a_address,
        token_b_address,
        exchange_contract_address,
        tx_hash,
        tx."from" as tx_from,
        tx."to" as tx_to,
        trace_address,
        evt_index,
        row_number() OVER (PARTITION BY tx_hash, evt_index, trace_address) AS trade_id
    FROM (

        --Uniswap v3
        SELECT
            t.evt_block_time AS block_time,
            'Uniswap' AS project,
            '3' AS version,
            'DEX' AS category,
            t."recipient" AS trader_a,
            NULL::bytea AS trader_b,
            abs(amount0) AS token_a_amount_raw,
            abs(amount1) AS token_b_amount_raw,
            NULL::numeric AS usd_amount,
            f.token0 AS token_a_address,
            f.token1 AS token_b_address,
            t.contract_address as exchange_contract_address,
            t.evt_tx_hash AS tx_hash,
            NULL::integer[] AS trace_address,
            t.evt_index
        FROM
            uniswap_v3."Pair_evt_Swap" t
        INNER JOIN uniswap_v3."Factory_evt_PoolCreated" f ON f.pool = t.contract_address

        ) dexs
    INNER JOIN ethereum.transactions tx
        ON dexs.tx_hash = tx.hash
    LEFT JOIN erc20.tokens erc20a ON erc20a.contract_address = dexs.token_a_address
    LEFT JOIN erc20.tokens erc20b ON erc20b.contract_address = dexs.token_b_address
    LEFT JOIN prices.usd pa ON pa.minute = date_trunc('minute', dexs.block_time)
        AND pa.contract_address = dexs.token_a_address
    LEFT JOIN prices.usd pb ON pb.minute = date_trunc('minute', dexs.block_time)
        AND pb.contract_address = dexs.token_b_address
```

[https://dune.com/queries/42779](https://dune.com/queries/42779)

### Testing Abstractions

Another great use case of utilizing the "create" function is to test out if the Pull Request you are making to our abstractions GitHub actually produce the intended results. Simply try running the query with the schema **dune\_user\_generated** instead of the actual schema that you want in GitHub.

If the test succeeds, you can proceed in making the Pull Request. If you can please attach the "Test Table/View" into the Pull Request.

### View Definition

To find out how a particular view got created you can run queries against PostgreSQL base tables.

**A particular view**

```sql
select definition from pg_views 
where viewname = 'view_name_here'
```

**All views**

```sql
select * from pg_views 
where schemaname = 'dune_user_generated'
```

### View dependencies

If you build multiple views that are dependent on each other it might sometimes happen that you can't change `view1` because `view2` depends on `view1` . This can be remedied by running the query below to fix any dependency issues.

```sql
-- source: https://stackoverflow.com/a/48770535/1838257

--CREATE OR REPLACE VIEW dune_user_generated.gosuto_view_dependencies AS
SELECT DISTINCT srcobj.oid AS src_oid,
    srcnsp.nspname AS src_schemaname,
    srcobj.relname AS src_objectname,
    tgtobj.oid AS dependent_viewoid,
    tgtnsp.nspname AS dependant_schemaname,
    tgtobj.relname AS dependant_objectname
FROM pg_class srcobj
  JOIN pg_depend srcdep ON srcobj.oid = srcdep.refobjid
  JOIN pg_depend tgtdep ON srcdep.objid = tgtdep.objid
  JOIN pg_class tgtobj ON tgtdep.refobjid = tgtobj.oid AND srcobj.oid <> tgtobj.oid
  LEFT JOIN pg_namespace srcnsp ON srcobj.relnamespace = srcnsp.oid
  LEFT JOIN pg_namespace tgtnsp ON tgtobj.relnamespace = tgtnsp.oid
WHERE tgtdep.deptype = 'i'::"char" AND tgtobj.relkind = 'v'::"char"

-- filter like so:
-- SELECT * FROM dune_user_generated.gosuto_view_dependencies
-- WHERE src_objectname LIKE '%filter_word%'
```

You need to temporarily break the dependencies in order to be able to change `view1`.

Find the query [here](https://dune.com/queries/70916). Big thanks to [@gosuto](https://dune.com/gosuto) for uncovering this.
