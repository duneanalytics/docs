---
title: 执行查询 ID
description: 如何执行（运行）一个带或不带参数的查询来检索数据。
---
# [POST] 执行查询 ID

如何执行（运行）一个带或不带参数的查询来检索数据。

## 请求参数

无需参数。你也可以选择添加查询参数（[参见此案例](#curl-with-parameters)）。

## 返回值

返回指定请求的 `execution_id` 。

## 请求示例

```
POST v1/query/{{query_id}}/execute

https://api.dune.com/api/v1/query/{{query_id}}/execute
```

### cURL

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```

### cURL with Parameters

```
curl -X POST -d '{"query_parameters": { "param1":24}}' -H x-dune-api-key:{{api_key}}  "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```

## 返回示例

!!! info "Dune API 以 JSON 格式返回响应。"

```json
{
    "execution_id": "01GB1Y2MRA4C9PNQ0EQYVT4K6R",
    "state": "QUERY_STATE_PENDING"
}
```

 - *execution_id* : 每次调用此 API 时都会生成的一个唯一 ID。你可能想要保存这个值，用以稍后传递给其他 API 接入点。
 - *state* : 查询的当前执行状态。查阅 "FAQ" 章节，了解不同状态码的具体含义。