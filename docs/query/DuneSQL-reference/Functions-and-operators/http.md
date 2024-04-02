---
title: HTTP functions
---

The HTTP functions send HTTP requests to a specified URL.
Using the HTTP functions, you can interact with HTTP servers directly in SQL queries.
They allow to fetch data from external APIs, as well as invoke remote procedure calls.


### Functions

#### http_get()
**``http_get(url: varchar)``** → varchar

**``http_get(url: varchar, headers: array(varchar))``** → varchar

The function sends an HTTP GET request to the given URL, optionally including the provided headers,
and returns the response body as `varchar`.

Often, the response is a JSON document. You can process it further with [JSON-processing SQL functions](json.md).
Other response formats, like html, are also supported.

#### http_post()
**``http_post(url: varchar, body: varchar)``** → varchar

**``http_post(url: varchar, body: varchar, headers: array(varchar))``** → varchar

The function sends an HTTP POST request to the given URL, including the provided data in the request body,
and optionally including the headers. It returns the response body as `varchar`.

The type of the body argument is `varchar`. It gives you flexibility to send JSON data as well as text.


### Access

The HTTP functions are available free of charge to all Dune paying customers.


### API support and credentials

There are no limits to the supported APIs. The URL can point to any public or private API.

If you need to pass credentials for the API, you can include them in the headers.
For example, you can use the `Authorization` header to pass a token.
If you choose to hardcode the credentials in the query, please make sure to keep the query private.
Optionally, you can use a query parameter as a placeholder:

```sql
SELECT http_get(
    'https://api.blastscan.io/api?module=block&action=getblocknobytime&timestamp=1711712564&closest=before&apikey={{api_key}}'
);
```

### Limits

***Call timeout:*** A call issued by an HTTP function times out after 5 seconds.

***Throttling:*** Requests from each query execution are limited to 50 requests per second per proxy.
There are currently 3 proxies configured per clusterset. The rate limit is shared between all HTTP function calls
made within the query.

***Response size limit:*** Maximum accepted response body size is 1_000_000 bytes.

***Data size limit:*** Maximum accepted request body size for `http_post()` is 1_000_000 bytes.


### Examples

#### Single HTTP GET request to list coins from CoinGecko

```sql
SELECT http_get('https://api.coingecko.com/api/v3/coins/list');
```

#### Multiple HTTP GET requests parametrized with Dune data

```sql
SELECT
    http_get(concat('https://coins.llama.fi/prices/current/ethereum:', CAST(contract_address AS varchar)))
FROM tokens_ethereum.stablecoins;
```

#### JSON processing with http_get()

```sql
SELECT
    contract_address,
    json_query(
        http_get(concat('https://coins.llama.fi/prices/current/ethereum:', CAST(contract_address AS varchar))),
        'lax $.coins.*?(@.decimals==18).keyvalue()?(@.name=="symbol" || @.name=="price" || @.name=="decimals").value'
        WITH ARRAY WRAPPER
        EMPTY ARRAY ON EMPTY
) as coin_data
FROM tokens_ethereum.stablecoins;
```

#### Using http_get() in a subquery as a static filter
By wrapping the `http_get()` function in a subquery, you can use it as a static filter in the main query.
It helps to avoid repeating the same HTTP request multiple times.

```sql
SELECT *
FROM
    ethereum.transactions t1,
    (SELECT from_hex(json_extract_scalar(http_get('https://api.ensideas.com/ens/resolve/vitalik.eth'),'$.address'))) t2(x)
WHERE t1."from" = t2.x;
```

#### RPC call with http_post()

```sql
SELECT http_post(
		'https://docs-demo.quiknode.pro',
		'{"method":"eth_chainId","params":[],"id":1,"jsonrpc":"2.0"}',
		ARRAY['Content-Type: application/json']);
```

#### Handling quotation marks
If your payload contains the `'` character, you need to quote it properly because it is the bounding character of `varchar`.
Each `'` character should be doubled, and the query engine will unwrap them.

```sql
SELECT json_value(
	        http_post(
			    'https://httpbin.org/post',
				'foo',
				ARRAY['MyHeader : Use two '' quotes']),
			'lax $.headers.Myheader');
```
