---
title: 错误代码
description: 如何处理在使用 Dune API 的过程中可能遇到的错误。
---

好消息：你在非常早期的时候接触到了 Dune API。 🧙‍♂️

坏消息：这意味着我们仍在努力解决一些潜在的小问题。 👹

目前，Dune API 并不总是抛出异常信息。在某些情况下，当事情未按预期进行时，您需要使用我们的响应对象来解析具体信息。

!!! Note
    如果这些东西对您而言，太过于生僻、复杂或困惑，不要太勉强自己。欢迎在 [#dune-api Discord channel](https://discord.com/channels/757637422384283659/1019910980634939433) 联系我们，我们会在您卡住的时候提供帮助。

以下是几种常见的错误情况：

## API Key 无效

### 返回对象

```
 {'error': 'invalid API Key'}
```

#### 核查
 
  - 确保您在 *header* 中将您的 API Key 传给接入点。具体实现方式，请参阅 [鉴权] 章节（.../api-reference/authentication.md），以及我们 [快速入门指南]（.../quick-start/api-py.md）中具体语言的实现案例。
  - 如果您已经在 header 中传递了 API Key，请确保输入正确。


## 发生了内部错误

### 返回对象

```
 {'error': 'An internal error occurred'}
```

#### 核查

  - 如果您正在使用我们的某个 GET 接入地址，请确保您输入的 "query_id" 是正确的。
  - 如果您正在使用我们的某个 POST 接入地址，请确保您从 GET 接入地址获取的 `execution_id` 已经被正确传递到 POST 接入地址。


当前文档并不完善！

我们目前正在努力完善中，但还是那句话，获得任何帮助的最佳途径依旧是我们的 [#dune-api Discord channel](https://discord.com/channels/757637422384283659/1019910980634939433)。