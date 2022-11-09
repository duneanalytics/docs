---
title: 执行状态
description: 如何检查执行请求的状态。
---

# [GET] 执行状态

如何检查执行请求的状态。

## 请求参数

无需参数。

## 返回值

如果执行完成，则返回查询的执行状态以及相关的结果元数据。

## 请求示例

您需要传递您从 [执行查询 ID](execute-query-id.md) 请求中获得的 `execution_id` 参数，用以完成获取执行状态的 API 请求。

```
GET v1/execution/{{execution_id}}/status

https://api.dune.com/api/v1/execution/{{execution_id}}/status
```

### cURL

```
curl -X GET "https://api.dune.com/api/v1/execution/{{execution_id}}/status" -H x-dune-api-key:{{api_key}}
```

## 返回示例

!!! info “Dune API 以 JSON 格式返回响应。”

### 查询运行中

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_EXECUTING",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "1970-01-01T00:00:00Z",
    "execution_started_at": "2022-08-29T06:33:24.916543331Z"
}
```

### 执行完成

```json
{
    "execution_id": "01GBM4W2N0NMCGPZYW8AYK4YF1",
    "query_id": 980708,
    "state": "QUERY_STATE_COMPLETED",
    "submitted_at": "2022-08-29T06:33:24.913138Z",
    "expires_at": "2024-08-28T06:36:41.58847Z",
    "execution_started_at": "2022-08-29T06:33:24.916543Z",
    "execution_ended_at": "2022-08-29T06:36:41.588467Z",
    "result_metadata": {
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
```

 - *execution_id* : 当前 API 调用的执行 ID 。
 - *query_id* : 当前请求所对应执行的 Dune 查询 ID 。
 - *state* : 此查询的当前执行状态。查阅 `FAQ` 章节，了解不同状态码所对应 `state` 的具体含义。
 - *submitted_at* : 执行该查询的 API 被调用时的时间戳。
 - *expires_at* : 该查询的执行结果被储存在我们数据库中的过期时间。
 - *execution_started_at* : 该请求在我们的服务器中查询执行开始的时间。
 - *execution_ended_at* : 该请求在我们的服务器中查询执行完成的时间。
 - *result_metadata* : 本次请求返回数据的一些属性。
    - *column_names* : 本次请求返回数据中的列名。
    - *result_set_bytes* : 返回数据的字节大小。
    - *total_row_count* : 返回数据的行数。
    - *datapoint_count* : 该请求返回的数据点（datapoints）总数，等值于（`total_row_count` x 列数）。
    - *pending_time_millis* : 在我们的服务器中为这个请求分配一个插槽所花费的时间（以毫秒计）。
    - *execution_time_millis* : 该请求实际执行查询所花费的时间（以毫秒计）。

## 查询执行状态 FAQ

### “执行中”(Executing)和“待执行”(Pending)这两种状态有什么区别？

待执行(Pending)指的是执行正在等待一个可用的执行连接槽。执行中(Executing)意味着目前正对数据库进行查询。

以下是所有的状态码清单，供参考。

   - QUERY_STATE_PENDING  - 查询执行正在等待执行插槽
   - QUERY_STATE_EXECUTING - 查询正在运行中
   - QUERY_STATE_FAILED - 执行失败
   - QUERY_STATE_COMPLETED - 执行成功完成
   - QUERY_STATE_CANCELLED - 用户取消执行
   - QUERY_STATE_EXPIRED - 查询执行过期，结果不再可用