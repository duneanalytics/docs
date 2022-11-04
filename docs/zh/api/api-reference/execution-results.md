---
title: 执行结果
description: 如果获取执行请求的结果数据。
---

# [GET] 执行结果

如何获取执行请求的结果数据。

## 请求参数

无需参数。

## 返回值

返回执行查询的状态、元数据和查询结果。

## 请求示例

您需要传递您从 [执行查询 ID](execute-query-id.md) 请求中获得的 `execution_id` 参数，用以完成获取执行结果的 API 请求。

```
GET v1/execution/{{execution_id}}/results

https://api.dune.com/api/v1/execution/{{execution_id}}/results
```

### cURL

```
curl -X GET "https://api.dune.com/api/v1/execution/{{execution_id}}/results" -H x-dune-api-key:{{api_key}}
```

## 返回示例

!!! info “Dune API 以 JSON 格式返回响应。”

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_COMPLETED",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "2024-08-28T06:36:41.58847Z",
    "execution_started_at": "2022-08-29T06:33:24.916543Z",
    "execution_ended_at": "2022-08-29T06:36:41.588467Z",
    "result": {
        "rows": [
            {
                "TableName": "eth_blocks",
                "ct": 6296
            },
            {
                "TableName": "eth_traces",
                "ct": 4474223
            },
            {
                "TableName": "eth_creation_traces",
                "ct": 10155
            },
            {
                "TableName": "eth_logs",
                "ct": 2137508
            },
            {
                "TableName": "eth_transactions",
                "ct": 1039890
            },
            {
                "TableName": "sol_transactions",
                "ct": 37185158
            },
            {
                "TableName": "bnb_transactions",
                "ct": 2942005
            },
            {
                "TableName": "optimism_transactions",
                "ct": 120973
            }
        ],
        "metadata": {
            "column_names": [
                "ct",
                "TableName"
            ],
            "result_set_bytes": 194,
            "total_row_count": 8,
            "datapoint_count": 16,
            "pending_time_millis": 8,
            "execution_time_millis": 24
        }
    }
}
```

 - *execution_id* : 当前 API 调用的执行 ID 。
 - *query_id* : 当前请求所对应执行的 Dune 查询 ID 。
 - *state* : 此查询的当前执行状态。查阅 `FAQ` 章节，了解不同状态码所对应 `state` 的具体含义。
 - *submitted_at* : 执行该查询的 API 被调用时的时间戳。
 - *expires_at* : 该查询的执行结果被储存在我们数据库中的过期时间。
 - *execution_started_at* : 该请求在我们的服务器中查询执行开始的时间。
 - *execution_ended_at* : 该请求在我们的服务器中查询执行完成的时间。
 - *result* :
    - *rows* : 该请求返回的实际数据记录。
    - *metadata* : 返回查询数据的一些属性。
        - *column_names* : 返回数据中的列名。
        - *result_set_bytes* : 返回的数据大小。
        - *total_row_count* : 数据中的行数。
        - *datapoint_count* : 该请求返回的数据点（datapoints）总数，等值于（`total_row_count` x 列数）。
        - *pending_time_millis* : 在我们的服务器中为这个请求分配一个插槽所花费的时间（以毫秒计）。
        - *execution_time_millis* : 该请求实际执行查询所花费的时间（以毫秒计）。


## 查询结果读取 FAQ

### 我能否通过直连数据库来提取数据？

目前还不行。在过渡时期，我们建议定期从 "max(latestBlockNumber) - 2" 到 "lastFetchedBlockNumber" 之间获取数据。从最新区块编号往前2位开始获取，可以确保你从每次新请求中获取到完整数据集。

### 查询结果数据是否会被存档以便快速检索？

没错

### 执行的结果数据会被储存多久？

目前是2年，但未来我们可能会降低到接近90天。这个值在 API 响应的执行状态和查询结果的 "expires_at" 字段均可见。

### 在单次 API 结果调用中，我可以获取多少数据？

目前上限为 1GB，但我们可能会在整体上调低此限制，或依据不同的付费计划类型而有所不同。