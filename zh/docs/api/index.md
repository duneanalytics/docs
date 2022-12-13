---
title: API
description: 欢迎来到 Dune API
---

# 欢迎来到 Dune API

![dune API Cover](images/dune_api_cover.jpg)

所有您能在 Dune 网站上看到的查询和数据，都可以通过 Dune API 完整获取。这也就意味着，任何的公共查询，您都可以执行查询并读取结果，这当然也包括您账户内拥有访问权限的私人查询。

本文档描述了所有可用的 API 调用及返回对象的属性。如果您有任何疑问或反馈意见，请通过 [api-feedback@dune.com](mailto:api-feedback@dune.com) 联系我们，或者来我们的 #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) Discord 频道。

！！！ 注意

截至目前，Dune API 尚处于内测阶段。这意味着它的工作方式和返回数据可能会在提前通知后发生变化。

## API 如何工作？

我们的 API 目前允许用户：

1. 执行查询
2. 检查执行状态
3. 获取执行结果

这些执行结果目前单独存储，与您在 Dune.com 网站上看到的任何内容都不一样。这意味着从 Dune API 获得查询结果的唯一方法是使用 Dune API 执行查询。

同样的，通过 API 执行的结果目前也没有出现在 Dune 的网站上。

## API 入门

### 获取一枚 API 密钥

Dune API 目前尚处于内部测试阶段，有小一批内测用户，但会在11月的时候对外开放！

### 选择一门编程语言

您可以自由选择自己的语言来使用我们的 API - 查阅 [API 参考](api-reference/authentication.md) 区 - 我们目前针对 [Python](quick-start/api-py.md) 和 [Node.js](quick-start/api-js.md) 有快速入门教程。

### 我可以用 Dune API 构建什么？

通过 Dune，您可以访问当下最流行的区块链生态的几乎所有数据。使用这些数据来构建的东西是没有任何限制的！

由于有如此之多的可能性，有时候构思要做什么东西可能相当有挑战，所以这里给一些帮您构思的小提示：

#### 区块链数据的新型接口

我们的社区达人 [@0xBoxer](https://dune.com/0xBoxer) 制作了一个 [教程](https://youtu.be/ez3VfcfNwvc) ，他带我们一起创建一个可以给任何钱包地址自定义个性化指标的 [数据看板](https://dune.com/0xBoxer/gas-tracker-dashboard) 。

有了 Dune API，就可以在您自己超丝滑、超酷的应用 UX 中为这个看板或 Dune 上的任何其他看板搭建一个更漂亮的用户界面。

除此之外，还可以将 API 查询结果用于 Excel、Google 表格、Notion 页面、 Discord 机器人、Telegram 机器人等处，没有任何使用限制。

有了 API，数据可以流向任何地方！

#### 来自 CoW Protocol 的真实案例

我们社区的 [@bh2smith](https://dune.com/bh2smith)  (同时也来自 [Cow Protocol](https://dune.com/cowprotocol)) 周四在 [DuneCon](https://dunecon.com) 发表了一次讲话，向我们展示了 Cow Protocol 使用 API 的真实案例。

[在这里看视频重播](https://youtu.be/VEvk-iqxXIM?t=404)!

## 重要链接

 - API 文档 - 您已经在这儿了，查看侧边栏以了解更多信息！
 - [#dune-api Discord 频道](https://discord.com/channels/757637422384283659/1019910980634939433)
 - [API 客户端 (来自社区构建)](../api/quick-start/community-clients.md)