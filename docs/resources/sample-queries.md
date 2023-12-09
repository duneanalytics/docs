---
title: Sample Queries
description: Learn how to make use of popular tables and spells on Dune
---

# Sample Queries  
   
Dune is a platform that provides tools for querying, visualizing, and analyzing data from various chains. However, this can be difficult for new users that are not familiar with SQL/on chain data! Hence this guide will help you on your journey becoming a Dune wizard.

Refer to [this dashboard](https://dune.com/resident_wizards/sample-queries){:target="_blank"}, which is a collection of commonly requested queries over time, and this list will continue to grow! Don't find the query that you need? Check out the [Dune AI](https://dune.com/ai){:target="_blank"} or head down to our [Discord](https://discord.gg/dunecom).



### Getting Total Supply Of ERC20 Token 

[Getting Total Supply of ERC20 Token Query](https://dune.com/queries/3265730){:target="_blank"}

To get the total supply of ERC20 token, we can make use of the erc20's Transfer event that is emitted on every transfers. 

For every token that are minted, there will be an event emitted from these transfers from the blackhole address(`0x0000000000000000000000000000000000000000`), and when tokens are burned, they will usually get sent to the similar address as well.

```
SELECT SUM(case when "from" = 0x0000000000000000000000000000000000000000 THEN (value/1e18) ELSE -(value/1e18) END) as lp_supply
from erc20_ethereum.evt_transfer
where contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- erc20 token address
and ("from" = 0x0000000000000000000000000000000000000000 or "to" = 0x0000000000000000000000000000000000000000)
-- to filter transfers that are sent from or receiving from the blackhole address
```

From the query above, we can make use of the `erc20_ethereum.evt_transfer` table, to get the total supply. As the `erc20_ethereum.evt_transfer` table contains all erc20 tokens' transfer, you have to filter by `contract_address`,sender(`from`) and recipient(`to`).


Next, you'll need to sum up all the transfer events, adding when token is minted `"from" = 0x0000000000000000000000000000000000000000` and subtracting when token is burned(sent to blackhole address(`to = 0x0000000000000000000000000000000000000000`))

This is done here, using `CASE` function to get the aggregated amount.

```
SELECT SUM(case when "from" = 0x0000000000000000000000000000000000000000 THEN (value/1e18) ELSE -(value/1e18) END)
```

You can then verify the token supply on blockchain explorer!

### Getting All Token Holders Of ERC20 Token

[Getting All ERC20 Token Holders' Balance](https://dune.com/queries/2753189){:target="_blank"}

Similarly to getting total supply of ERC20 token, we will make use of the erc20's Transfer event table to achieve this.

For every erc20 transfers that each wallet received / sent out, we can just aggregate them up and grouping by the wallet address.

```
SELECT address,
       symbol,
       SUM(amount) as balance
FROM (
-- transactions that address having token outflows
SELECT tr."from" AS address,
       symbol,
       contract_address,
       -(tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
WHERE "from" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token 
UNION ALL
-- transactions that address having token inflows
SELECT tr."to" AS address,
       symbol,
       contract_address,
       (tr.value/POW(10,decimals)) AS amount
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
 WHERE "to" != 0x0000000000000000000000000000000000000000 -- exclude mint/burn addresses
 AND contract_address = 0x046eee2cc3188071c02bfc1745a6b17c656e3f3d -- contract_address of the erc20 token
 ) x
 GROUP BY address,symbol
 HAVING SUM(amount) > 0.1 --  having more than 0.1 balance
 ORDER BY 3 DESC
```

```
FROM erc20_ethereum.evt_transfer tr JOIN tokens.erc20 USING (contract_address)
```

As token decimals varies, we can make use of the `tokens.erc20` table, which contains the token mapping to get the `symbol` and `decimals`.
We then divide the value by the token decimals(`tr.value/POW(10,decimals)`) to get the amount.

To get the balance of each user, you'll need to get to sum up inflows(`"to"`) and subtracting outflows(`"from"`) to get the current balance.
We then aggregate all the values from the events,to get the current balance of each holder(`GROUP BY address,symbol`).

- You can also add in a filter to remove holders that are holding dust amount (` HAVING SUM(amount) > 0.1`)
- You can also add in a filter to get the top X holders (`LIMIT 100`) at the end of query

























