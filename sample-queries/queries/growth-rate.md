# Growth Rate

### Growth rate <a id="Growth-rate"></a>

Assuming you have a query with a count of some event grouped by time \(month for instance\) you can add this snippet to you `select` statement to get growth rate.

```text
(count(distinct event) - lag(count(distinct event), 1)
over (order by date_trunc('month', evt_block_time))) / lag(count(distinct action), 1)
over (order by date_trunc('month', evt_block_time)) as "Growth rate"
```

Multiply the number by 100 to get percentage.

