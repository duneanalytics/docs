---
title: 撤销执行
description: 如何撤销您的 Dune API 执行请求。
---

# [POST] 撤销执行

如何撤销您的 Dune API 执行请求。

## 请求参数

无需参数。

## 返回值

返回一个布尔值，用于表示执行是否被成功撤销。

## 请求示例

您需要传递您从 [执行查询 ID POST](execute-query-id.md) 请求中获得的 `execution_id` 参数，用以完成撤销执行的 API 请求。

```
POST v1/execution/{{execution_id}}/cancel

https://api.dune.com/api/v1/execution/{{execution_id}}/cancel
```

### cURL

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/execution/{{execution_id}}/cancel"
```

## 返回示例

!!! info "Dune API 以 JSON 格式返回响应。"

```json
{
    "success": true
}
```

 - *success* : 一个布尔值，用于表示撤销查询执行的请求是否成功。