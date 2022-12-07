---
title: Dune API 计费与定价
description: Dune API 计费与定价的相关信息。
---
# FAQ: 计费与定价

## API 免费吗？
    
我们正为特定用户提供有限时长的免费试用服务。在任何试用期过后，都需要付费使用 API。
    
## API 计费将如何与新的团队套餐（Team plans）配合？

We'll be supporting API keys on a team level. So any usage associated with those keys will be billed to their respective team.

## 什么是数据点（datapoint）？

通常情况下，一个数据点可以被认为是 行*列 的结果。在一组结果中每个单元格平均有 50 字节的额外限制。可以表示为：

Datapoints = max(rows*columns, ceil(totalbytes/50))

## 每次执行都要收取数据点费用吗？

对于每个不同的查询执行，我们对第1次读取结果和随后的第 100 次读取结果中的数据点进行收费。
