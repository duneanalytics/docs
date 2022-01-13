# raw transactions per wallet

### Total # of Transactions

```sql
with alltransactions
AS (

SELECT 
    block_time, 
    success, 
    gas_price/10^9 AS gas_prices, 
    gas_used,
    (gas_price*gas_used)/10^18 AS eth_paid_for_tx,
    hash
FROM ethereum.transactions
WHERE "from" = CONCAT('\x', substring('{{1. Eth Address}}' from 3))::bytea
AND block_time >= '{{2. Start Date}}'
AND block_time < '{{3. End Date}}')

SELECT
    count(*)
FROM alltransactions

```

### Transaction Success Rate

```sql
with alltransactions
AS (

SELECT 
    block_time, 
    success, 
    gas_price/10^9 AS gas_prices, 
    gas_used,
    (gas_price*gas_used)/10^18 AS eth_paid_for_tx,
    hash
FROM ethereum.transactions
WHERE "from" = CONCAT('\x', substring('{{1. Eth Address}}' from 3))::bytea
AND block_time >= '{{2. Start Date}}'
AND block_time < '{{3. End Date}}')

SELECT
    success, 
    count(success)*100/sum(count(*)) over ()
FROM alltransactions
GROUP by success
ORDER BY success DESC
```

### Running Total of # of Transactions

```sql
with alltransactions
AS (

SELECT 
    block_time, 
    success, 
    gas_price/10^9 AS gas_prices, 
    gas_used,
    (gas_price*gas_used)/10^18 AS eth_paid_for_tx,
    hash
FROM ethereum.transactions
WHERE "from" = CONCAT('\x', substring('{{1. Eth Address}}' from 3))::bytea
AND block_time >= '{{2. Start Date}}'
AND block_time < '{{3. End Date}}')

SELECT
    block_time,
    COUNT(block_time) over (ORDER BY block_time ASC) AS "Total # of Transactions"
FROM alltransactions 
```

