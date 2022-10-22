---
title: 鉴权
description: 如何认证您的API请求。
---

Dune API 使用 API 密钥（API Keys）来认证请求。您的 API 密钥被用来确定您可以调用的私人查询权限，以及哪个账户为此请求付费，所以请务必保证密钥安全! 

**请不要在GitHub、客户端代码等可公开访问的地方分享你的 API 密钥。**

API 鉴权通过在请求头中添加 "x-de-api-key" 属性来实现。所有类型的请求中都需要这么做！

下面是一个用于执行 POST 请求的 API 调用案例：

```
curl -X POST -H x-dune-api-key:{{api_key}} "https://api.dune.com/api/v1/query/{{query_id}}/execute"
```