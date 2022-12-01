---
title: Python 示例
description: 如何通过 Python 调用 Dune API。
---

让我们通过 Python 调用 Dune API！

本例中，我们将使用 Python3。我们建议使用虚拟环境和`pip`包管理器。

!!! example "前提条件"
    本快速入门指南假定您之前有过一些 Python 的开发经验，尽管我们的目的是使这些代码易于理解。如果您有其他问题，请通过 Discord 的 #[dune-api](https://discord.com/channels/757637422384283659/973606737393352745) 频道与我们的团队联系。

## 着手准备

我们将主要使用 `requests` 库来访问 API，所以先安装它：

``` bash
pip install requests
```

我们还将使用 `pandas` 将从 API 返回的数据加载到一个整洁的 DataFrame（表格）中，并使用 `jupyter notebooks` 创建一个高颜值的交互界面来完成所有这些工作。

所以，我们一并安装这些库：

``` bash
pip install pandas
pip install jupyter notebook
```

我们建议在 jupyter 界面演示后续的快速入门指南。您可以用这条简单的命令来启动界面：

``` bash
jupyter notebook
```

### 导入必要的库

``` py
from requests import get, post
import pandas as pd
```

### API Keys

您对 Dune API 的任何调用都需要在调用头中传递 API 密钥：

``` py
API_KEY = "YOUR_API_KEY"
HEADER = {"x-dune-api-key" : API_KEY}
```

### 简化URL生成

虽然并非必要，但使用此函数可以更容易为不同的 API 访问域名（endpoints）生成 URL：

``` py
BASE_URL = "https://api.dune.com/api/v1/"

def make_api_url(module, action, ID):
    """
    We shall use this function to generate a URL to call the API.
    """
    
	url = BASE_URL + module + "/" + ID + "/" + action
	
    return url
```

## 用函数包裹API访问域名（endpoints）

Dune API 目前有四个主要的访问域名，在 [API参考](.../api-reference/authentication.md) 部分有详细介绍。我们这里用一些函数进行包装，从而使得调用 Dune API 像挥动魔法棒 🪄 一样简单：

``` py
def execute_query(query_id):
    """
    Takes in the query ID.
    Calls the API to execute the query.
    Returns the execution ID of the instance which is executing the query.
    """
    
    url = make_api_url("query", "execute", query_id)
    response = post(url, headers=HEADER)
    execution_id = response.json()['execution_id']
    
    return execution_id


def get_query_status(execution_id):
    """
    Takes in an execution ID.
    Fetches the status of query execution using the API
    Returns the status response object
    """
    
    url = make_api_url("execution", "status", execution_id)
    response = get(url, headers=HEADER)
    
    return response


def get_query_results(execution_id):
    """
    Takes in an execution ID.
    Fetches the results returned from the query using the API
    Returns the results response object
    """
    
    url = make_api_url("execution", "results", execution_id)
    response = get(url, headers=HEADER)
    
    return response


def cancel_query_execution(execution_id):
    """
    Takes in an execution ID.
    Cancels the ongoing execution of the query.
    Returns the response object.
    """
    
    url = make_api_url("execution", "cancel", execution_id)
    response = get(url, headers=HEADER)
    
    return response
```

## 使用 Dune API

### 执行查询

为了 [执行查询](../api-reference/execute-query-id.md)，您可以传递任何您想要从 Dune 获取数据的 `query_id`，然后把它传递给`execute_query` 函数：

#### 函数调用

``` py
execution_id = execute_query("1258228")
```

#### 返回结果

此函数会返回一个 `execution_id`，输出结果显示类似下面这样：

``` py
'01GCQKPC4QZ6Q8645C3JC4WBT1'
```

这个 execution ID 是其他 API 函数所需的输入项。

### 获取查询的执行状态

要获取 [查询执行状态](.../api-reference/execution-status.md)，从前面 `execute_query` 函数提取返回的 `execution_id`，然后将其传递给`get_query_status` 函数，如下所示：

#### 函数调用

``` py
response = get_query_status(execution_id)
```

#### 返回结果

此函数返回的`response`对象，输出结果显示类似下面这样：

``` json
{'execution_id': '01GCQKPC4QZ6Q8645C3JC4WBT1',
 'query_id': 1258228,
 'state': 'QUERY_STATE_COMPLETED',
 'submitted_at': '2022-09-12T01:05:51.781328Z',
 'expires_at': '2024-09-11T01:05:51.82013Z',
 'execution_started_at': '2022-09-12T01:05:51.806752Z',
 'execution_ended_at': '2022-09-12T01:05:51.820127Z',
 'result_metadata': {'column_names': ['block_time',
   'token_a_symbol',
   'token_b_symbol',
   'token_a_amount',
   'token_b_amount',
   'project',
   'version',
   'category',
   'trader_a',
   'trader_b',
   'token_a_amount_raw',
   'token_b_amount_raw',
   'usd_amount',
   'token_a_address',
   'token_b_address',
   'exchange_contract_address',
   'tx_hash',
   'tx_from',
   'tx_to',
   'trace_address',
   'evt_index',
   'trade_id'],
  'result_set_bytes': 5048,
  'total_row_count': 10,
  'datapoint_count': 220,
  'pending_time_millis': 25,
  'execution_time_millis': 13}}
```

大多数情况下，您主要关心这个 JSON 对象中的 `state` 属性，此例中即`QUERY_STATE_COMPLETED`。

### 获取查询结果

最终，让我们从完成查询的执行中加载结果。

#### 函数调用

``` py
response = get_query_results(execution_id)
```

让我们把 JSON `response` 对象中返回的数据包装成一个漂亮的pandas Dataframe。

``` py
data = pd.DataFrame(response.json()['result']['rows'])
```

#### 返回结果

如果一切顺利的话，您应该在这个函数返回的 `data` 变量中看到您的数据：

``` py
0	2021-05-14T15:17:39+00:00	DEX	191	\xf82d8ec196fb0d56c6b82a8b1870f09502a49f88	Uniswap	\xa2b4c0af19cc16a6cfacce81f192b024d625817d	7.819632e+11	781963170639542600000	KISHU	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	...	WETH	[]	1	\x75e29a7676717b99da65c6faad2e7644d00e2053	None	\x75e29a7676717b99da65c6faad2e7644d00e2053	\x6bc05c2bc156a60c1cacfc379540ad00b7280796613b...	\x7a250d5630b4cf539739df2c5dacb4c659f2488d	10387.825000	2
1	2022-04-06T07:01:37+00:00	DEX	11	\x6591c4bcd6d7a1eb4e537da8b78676c1576ba244	Uniswap	\xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48	1.007936e+04	10079361085	USDC	\x0391d2021f89dc339f60fff84546ea23e337750f	...	BOND	[]	1	\x0000006daea1723962647b7e189d311d757fb793	None	\x0000495194ec698fcf89ccf8abb445daf01db497	\x8b962e59ca9f1d91e465a7af289b4b4c9c7c64c6d30d...	\x0000006daea1723962647b7e189d311d757fb793	10093.794730	2
2	2022-04-06T07:10:12+00:00	DEX	438	\xa25b34d2ec38e338bde108c8c4040be88945d024	Uniswap	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	1.015798e-01	101579832516438100	WETH	\x8020734a29ee290fb81992874bd1de01a16c4204	...	None	[]	1	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	None	\xaac6fb32fd0a7a51768bddd4ac2f643445bd01af	\x8bbaff042cea60af88fac791c4d20f84ed7d21601c41...	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	342.732387	2
3	2022-04-06T07:10:12+00:00	DEX	339	\x8ef79d6c328c25da633559c20c75f638a4863462	Uniswap	\xa71d0588eaf47f12b13cf8ec750430d21df04974	1.058343e+09	1058343424775444053499052032.0	QOM	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	...	WETH	[]	1	\x7540000cab63979795c7d4b326cadbb00ed24a04	None	\x7540000cab63979795c7d4b326cadbb00ed24a04	\x8bea318de386a65ac1c0c88f13e39654c3d4ec53a412...	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	263.520686	2
4	2022-04-06T07:15:58+00:00	DEX	149	\x9c84f58bb51fabd18698efe95f5bab4f33e96e8f	Uniswap	\xb620be8a1949aa9532e6a3510132864ef9bc3f82	NaN	21168910617154070511616.0	None	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	...	WETH	[]	1	\xdf29ee8f6d1b407808eb0270f5b128dc28303684	None	\xdf29ee8f6d1b407808eb0270f5b128dc28303684	\x8bf5a55a772b3c3423ee628bd459655a1d7bd09a5c69...	\xdef171fe48cf0115b1d80b88dc8eab59176fee57	675.194000	2
5	2022-04-06T07:03:20+00:00	DEX	266	\x847e0b52589c9e6fa2dcc42b8ffb34ec924d4cf8	Uniswap	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	8.903535e-04	890353516515079	WETH	\x9cf77be84214beb066f26a4ea1c38ddcc2afbcf7	...	None	[]	1	\x7a250d5630b4cf539739df2c5dacb4c659f2488d	None	\xf2d229cc832661de2aa56249c5b7991006868522	\x8c00c8c20b1f3f1b447c579165c2759c688981dbc408...	\x1b2cf79d0a3622f25fbe10e968b3b25a348e008b	3.004792	2
6	2021-05-17T16:04:09+00:00	DEX	88	\x0d4a11d5eeaac28ec3f61d100daf4d40471f1852	Uniswap	\xdac17f958d2ee523a2206206994597c13d831ec7	1.003227e+02	100322742	USDT	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	...	WETH	[]	1	\x773dd321873fe70553acc295b1b49a104d968cc8	None	\x7af55e2ab6e74f338d674537958ad236d17ab3ac	\x6bc07c4f53719ad8d1a0f5f99d2db3699fa9dce888e3...	\x8df6084e3b84a65ab9dd2325b5422e5debd8944a	100.372301	2
7	2022-04-06T07:24:39+00:00	DEX	219	\xaa51ea59c985a92ce881517a8896931d4a86e9e3	Uniswap	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	3.214029e-01	321402936315917950	WETH	\x4846b0cce69121e4d25b6efe7738eaf27bca7e7f	...	None	[]	1	\x7a250d5630b4cf539739df2c5dacb4c659f2488d	None	\xa053dbafba05e307a7bddede09c7feb235dc34b1	\x8c86abc9c4eaff2b8de48351360781bc153cd16fa108...	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	1084.606349	2
8	2021-05-17T16:04:09+00:00	DEX	91	\x773dd321873fe70553acc295b1b49a104d968cc8	Uniswap	\x95ad61b0a150d79219dcf64e1e6cc01f0b64c4ce	6.477303e+06	6477302710423104532774912.0	SHIB	\xdac17f958d2ee523a2206206994597c13d831ec7	...	USDT	[]	1	\x8df6084e3b84a65ab9dd2325b5422e5debd8944a	None	\x7af55e2ab6e74f338d674537958ad236d17ab3ac	\x6bc07c4f53719ad8d1a0f5f99d2db3699fa9dce888e3...	\x8df6084e3b84a65ab9dd2325b5422e5debd8944a	103.636843	2
9	2022-04-06T07:24:39+00:00	DEX	234	\xaa51ea59c985a92ce881517a8896931d4a86e9e3	Uniswap	\xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2	1.127058e-01	112705776325968480	WETH	\x4846b0cce69121e4d25b6efe7738eaf27bca7e7f	...	None	[]	1	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	None	\xa053dbafba05e307a7bddede09c7feb235dc34b1	\x8c86abc9c4eaff2b8de48351360781bc153cd16fa108...	\x68b3465833fb72a70ecdf485e0e4c7bd8665fc45	380.336913	2
```

所以，您现在有了来自 Dune 查询的数据。

以表格呈现。

用 Python 获取。

🧙🪄

### 撤销查询执行

某些查询可能需要很长的时间来执行（几分钟）。

根据您的工作流程，您可能会想要撤销执行。做法如下：

```py
response = cancel_query_execution(execution_id)
```

当您有一个正在运行的查询并调用此函数，您会得到一个响应对象，用以确认撤销查询。

## 参数化查询

当您使用参数化查询时，只需变动一个位置：您需要将查询参数传递给我们的 API 访问域名。在这之后，其余部分无需任何变动。

所以，让我们定义一个函数 `execute_query_with_params` 来调用参数化查询的访问域名：

```py
def execute_query_with_params(query_id, param_dict):
    """
    Takes in the query ID. And a dictionary containing parameter values.
    Calls the API to execute the query.
    Returns the execution ID of the instance which is executing the query.
    """
    
    url = make_api_url("query", "execute", query_id)
    response = post(url, headers=HEADER, json={"query_parameters" : param_dict})
    execution_id = response.json()['execution_id']
    
    return execution_id
```

#### 创建一个参数字典

在我们的例子中，我们要创建一个只有一个键的字典，即 `wallet_address`，用于查询给定 `wallet_address` 的 gas 总花费：

```py
parameters = {"wallet_address" : "0xb10f35351ff21bb81dc02d4fd901ac5ae34e8dc4"}
```

#### 将参数字典传给访问域名点

现在让我们用我们刚定义好的函数来实现这一目标：

```py
execution_id = execute_query_with_params("638435", parameters)
```

搞定！

一旦您从这个 POST 访问域名获取到 `execution_id`，您就可以在API的所有 GET 访问域名上使用它，就像您使用一个无需参数的简单查询一样。

!!! 完整代码
    本教程的完整代码可在 [这个链接](https://github.com/SusmeetJain/dune_api_python) 查阅。