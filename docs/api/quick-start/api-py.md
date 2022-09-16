---
title: Python
description: Here's how to access the Dune API via Python.
---

Let's get started using the Dune API via Python!

In this example we'll be using Python3. We recommend using a virtual environment and the `pip` package manager.

!!! example "Prerequisites"
    This Quick Start Guide assumes you have some prior experience using Python, though we aimed to make the code here easy to follow. If you have questions, please reach out to our team via the #[dune-api](https://discord.com/channels/757637422384283659/973606737393352745) channel on Discord.

## Getting Set Up

We'll primarily be working with the `requests` library to access the API, so let's install it:

``` bash
pip install requests
```

We'll also use `pandas` to load the data returned from APIs into a neat DataFrame (table), and `jupyter notebooks` to have a nice interactive interface to do all of this.

So let us install these as well:

``` bash
pip install pandas
pip install jupyter notebook
```

We recommend following rest of the Quick Start in a jupyter notebook. You can start the interface with this simple command:

``` bash
jupyter notebook
```

### Import the necessary libraries

``` py
from requests import get, post
import pandas as pd
```

### API Keys

Any call you make to the Dune API will require you to pass your API key with your call's header:

``` py
API_KEY = "YOUR_API_KEY"
HEADER = {"x-dune-api-key" : API_KEY}
```

### Simplifying URL generation

Though not a necessary step, using this function will make it easier to generate URLs for different API endpoints:

``` py
BASE_URL = "https://api.dune.com/api/v1/"

def make_api_url(module, action, ID):
    """
    We shall use this function to generate a URL to call the API.
    """
    
	url = BASE_URL + module + "/" + ID + "/" + action
	
    return url
```

## Wrapping API endpoints in functions

The Dune API currently has four primary end points as documented in the [API Reference](../api-reference/authentication.md) section. We are going to wrap these up in neat functions which will make using the Dune API as easy as a flick of the 🪄:

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

## Using the Dune API

### Execute a Query

To [Execute a Query](../api-reference/execute-query-id.md), you can pass any `query_id` from Dune that you want to fetch data from, then pass it to the `execute_query` function:

#### Function Call

``` py
execution_id = execute_query("1258228")
```

#### Output

This function returns an `execution_id` which will look something like the sample output shown here:

``` py
'01GCQKPC4QZ6Q8645C3JC4WBT1'
```

This execution ID is the required input for rest of the API functions.

### Get Query Execution Status

To get the [Query Execution Status](../api-reference/execution-status.md), take the `execution_id` that was returned from the `execute_query` function in the previous section, then pass it to `get_query_status` function as shown here:

#### Function Call

``` py
response = get_query_status(execution_id)
```
#### Output

The `response` object returned by this function will look something like the example shown here:

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

In most cases, you will primarily be concerned with accessing the `state` property in this JSON object, which in this case is `QUERY_STATE_COMPLETED`.

### Get Query Results

Finally, let's load the results from the now-completed execution of our Query.

#### Function Call

``` py
response = get_query_results(execution_id)
```

Lets wrap the data received from this JSON `response` object up into a neat pandas Dataframe.

``` py
data = pd.DataFrame(response.json()['result']['rows'])
```

#### Output

If everything worked smoothly, you should see your data in the `data` variable returned by this function:

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

So you now have data from your Dune query.

In a table.

In Python. 

🧙🪄

### Cancel Query Execution

Some queries can take a long time to execute (minutes).

Depending on your workflow, you may want to interrupt execution at times. Here's how to do that:

```py
response = cancel_query_execution(execution_id)
```

When you have a running Query and call this function, you'll get a response object returned to you confirming the cancellation of query execution.

!!! Complete-Code
    The complete code for this tutorial is available on [this link](https://github.com/SusmeetJain/dune_api_python).
