---
title: Dune API 功能
description: Dune API 如何工作。
---
# FAQ: 功能

## 通用

### 我每分钟能发出多少次请求？

基于过载保护，API 暂时被限制在每分钟 12 次请求。如果您需要更高的吞吐量，请联系我们。

### 是否有具体的服务水平协议（SLAs）？

SLA将在未来的企业定价计划中提供。

## 执行查询

### 如何找到查询 ID（Query ID）？

当定位到某个查询时，"/queries/" 之后的第一个数字便是 Query ID。

![query-id-example](../images/query-id-example.jpg)

### API 是否支持查询参数？

API 确实支持查询参数!

对于包含参数的 Dune 查询，你可以将参数作为 Dune 查询的一部分来传递 [执行查询ID的接入点](../../api/api-reference/execute-query-id.md)!

更多内容请见 [创建带参数的 Dune 查询](../../getting-started/queries/parameters.md).

了解如何使用 [cURL](../../api/api-reference/execute-query-id.md#curl-with-parameters) 传递参数，以及 [Python](../../api/quick-start/api-py.md#parameterized-queries)。

### Dune API 和 Dune Web 应用之间有何性能及整体上的差异？我可以查询的内容有何不同？

两者之间没有太大的性能差异或可读取的内容差异。

Dune API 只是让你以编程方式读取已经可以从 Dune Web 应用访问的功能和数据集。

### 执行超时的限制是多久，我能否要求延长？

上线之初，查询执行的超时限制将与 Dune Web 应用相同：30分钟。

随后，我们计划允许修改时长，但我们也需要调整我们的查询执行收费来匹配。

### 你们打算什么时候支持使用直接从服务器发送原始SQL？

我们还没有一个确切的时间表，但此功能暂定于仅限企业计划。

### 我可以同时使用 Dune v2 引擎和原始的 v1 数据库进行查询吗？

当前没问题。但我们正在逐步废除对旧引擎的使用和支持，所以我们建议尽可能地使用新的 Dune v2 引擎。