---
title: Javascript 示例
description: 如何通过 JavaScript 调用 Dune API。
---

!!! Warning
    本指南尚不完善。如果您遇到其他问题，请通过 Discord 的 #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) 频道联系我们的团队。

让我们通过 JavaScript 调用 Dune API！

我们将向您展示几种通过 JavaScript 调用 API 的方式，本例中会使用 `node-fetch` 包。

!!! example "前提条件"
    本快速入门指南假定您对 Node.js（Node）、Node包管理器（NPM）和 Node版本管理器（NVM）较为熟悉。

首先，确保您使用的是 Node.js 的 LTS 版本（Node 16）和 NPM 的最新版：

## 着手准备

```
nvm use lts
npm install latest
```

然后安装 node-fetch 包：

```
npm install node-fetch
```

接下来，创建一个项目目录并初始化一个 ESM 兼容的 Node 项目：

```
mkdir dune_api_js
cd dune_api_js
npm init esm --yes
```

这将为您初始化一个项目，其中包括一个 `package.json` 文件。打开这个文件并添加下面这行内容：

``` json
"type": "module"
```

## Dune API 代码案例

将以下代码中的 `#！YOUR_API_KEY` 替换为您自己的 Dune API 密钥，然后将其添加到您项目的 `main.js` 文件中：

``` js
import { Headers } from 'node-fetch';
import fetch from 'node-fetch';

// Add the API key to an header object
const meta = {
    "x-dune-api-key": "YOUR_API_KEY"
};
const header = new Headers(meta);

//  Call the Dune API
const response = await fetch('https://api.dune.com/api/v1/query/1258228/execute', {
    method: 'POST',
    headers: header
});
const body = await response.text();

// Log the returned response
console.log(body);

```

直接运行这个脚本从 Dune API 中获得响应：

```
node main.js
```

您应该在命令行上看到一个返回的响应。

本例中，我们使用了一个简单的查询，该查询获取了一小部分数据集：`query_id: 1258228`
您也可以编辑 Query URL，即可从任何其他查询中获取您想要的数据！ 🪄

这里的代码仅调用了开启执行查询的 API 访问域名。如要获取该查询所返回的数据，您需要调用其他 API 访问域名。请参阅 [API参考](../api-reference/authentication.md) 部分的内容，以了解更多有关 Dune API 访问域名的信息。

!!! 完整代码
    本教程的完整代码可在 [这个链接](https://github.com/SusmeetJain/dune_api_js) 查阅。
