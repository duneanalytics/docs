---
标题: 用户自制表
描述: >-
  dune_user_generated架构是是在我们的数据库中构建自己的视图、函数或表的简单方法。
---

!!! note
    V2 现在尚未支持用户自制表。

**请注意，这些表不能保证数据的准确性，如果不是由您自己创建，请谨慎使用。**

**请随时保存视图的构造函数参数。有时我们必须删除视图，以便能够更改某些解码表或代理依赖关系，您可能需要重新部署视图。**

## 使用案例

有几种方法可以利用Dune内部的视图和表，使在Dune上处理数据更加容易。

您自己的表、视图和函数在Dune上创建内容时都起着重要作用，如果正确使用，可以使看板和查询的维护更容易。

如果您不熟悉表、视图、物化视图和函数，请参阅 [pgSQL 文档](https://www.postgresqltutorial.com/postgresql-views) 或查看我们的[入门指南](../../getting-started/index.md).

### 存储信息

有时，数据提取所需的某些信息没有正确存储在可用的表中或存储在许多不同的表中，这将使查询很难处理。在这些情况下，最好将必要的信息存储在视图中并引用该视图。

这方面的一个例子是将某些资金库或借贷代币映射到其各自的基础代币。


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

此表生成一个视图，可用于联接查询。

[请看这个数据表](https://dune.com/queries/41577).

### 整合数据

视图还可以用于将多个智能合约的操作聚合到一个包含所有必要数据的视图中。

如果您需要反复使用同一数据集，并且只更改显示或聚合数据的方式，这一点尤其有用。这样，您就不必一次又一次地查询数据集，只需将其放入一个视图中，然后就可以开始引用该视图。

这将允许您更改构建数据集的基本查询，而无需遍历查询。您可将此想象成，将数据收集和实际工作/显示拆分为两个独立工作的不同部分。

利用这一点将使仪表板的维护变得更加容易，因为您只需更改 **dune\_user\_generated** 视图，而不必逐一查看所有查询。

这方面的一个很好的例子是[这个看板](https://dune.com/keeganead/cryptoart\_1)。创建者在**dune\_user\_generated**模式中创建了一个基本数据集，并使用该数据集作为所有查询的基础。

请注意，虽然这种方法适用于大多数情况，但视图的计算成本可能非常高，您最好在我们的 [Spells](spells.md) 中构造一个具体的视图或数据表。

本例从 Uniswap\_v3 中获取数据，并对索引的数据进行标准化获得 dex.trades table。

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

### 测试抽象表

"create"函数的另一个很好的用途是测试GitHub发出的Pull Request是否对我们的抽象表产生了预期的结果。您只需尝试使用模式**dune\_user\_generated**而需要在GitHub中所需的实际模式运行查询。

如果测试成功，您可以继续进行Pull Request。如果可以，请将“测试表/视图”附加到Pull Request中。

### 视图定义

要了解特定视图是如何创建的，可以对PostgreSQL基表运行查询。

**一个特定的视图**

```sql
select definition from pg_views 
where viewname = 'view_name_here'
```

**所有视图**

```sql
select * from pg_views 
where schemaname = 'dune_user_generated'
```

### 视图依属

如果生成多个相互依赖的视图，有时可能会发生无法更改`view1`的情况，因为`view2`依赖于`view1`。可以通过运行下面的查询来解决任何视图间的依属问题。

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

您需要暂时中断依属关系才能更改`view1`。

您可以在 [这里](https://dune.com/queries/70916)找到该检索。 感谢 [@gosuto](https://dune.com/gosuto) 发现这个问题。
