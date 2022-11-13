---
title: Javascript
description: Here's how to access the Dune API via JavaScript.
---

!!! Warning
    This guide is not yet comprehensive. If you have questions, please reach out to our team via the #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) channel on Discord.

Let's get started using the Dune API via JavaScript!

We'll show you one of the several ways the API can be consumed via JavaScript, in this case using the `node-fetch` package. You can also try to use the native fetch funcionality which is available in the newest LTS version of node, node 18. We would be upgrading this guide in the near future to use the same.

!!! example "Prerequisites"
    This Quick Start Guide assumes you have some level of familiarity with Node.js (Node), Node Package Manager (NPM) and Node Version Manager (NVM).

To start, make sure you're using the current LTS version of Node.js (Node 18) and the latest version of NPM:

## Getting Set Up

```
nvm use --lts
npm install latest
```

Then install the node-fetch package:

```
npm install node-fetch
```

Next, create a project directory and initiate an ESMcompatible Node project:

```
mkdir dune_api_js
cd dune_api_js
npm init esm --yes
```

This will initiate a project for you which will include a `package.json` file. Open this file and add the following line to it:

``` json
"type": "module"
```

## Example Dune API Script

For the example here, we have used a simple example Query that fetches a small set of data, this query has the`query_id`, `1258228`.

Replace `#! YOUR_API_KEY` with your Dune API key in the following code, then add it to the `main.js` file in your project:

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

## Example Dune API Script for a Parameterized Query

If you are working with a parameterized query, use the script in this section instead of the previous one. For the example here, we have used a simple query that takes in a wallet address as a parameter. This query has the `query_id`, `1258228`. And we pass an example address as a value to the `wallet_address` parameter.

Replace `#! YOUR_API_KEY` with your Dune API key in the following code, then add it to the `main.js` file in your project:

``` js
import { Headers } from 'node-fetch';
import fetch from 'node-fetch';

// Add the API key to an header object
const meta = {
    "x-dune-api-key": "YOUR_API_KEY"
};
const header = new Headers(meta);

// Add parameters we would pass to the query
var params = { "query_parameters" : { "wallet_address": "0xb10f35351ff21bb81dc02d4fd901ac5ae34e8dc4" }};
var body = JSON.stringify(params);

//  Call the Dune API
const response = await fetch('https://api.dune.com/api/v1/query/638435/execute', {
    method: 'POST',
    headers: header,
    body: body // This is where we pass the parameters
});
const response_object = await response.text();

// Log the returned response
console.log(response_object);

```

## Running the Script

You can now run your script from the command line.

```
node main.js
```
You should see a response being returned.

You can also edit the Query URL to fetch data from any other Queries you'd like! 🪄
If it is a parameterized query, you would need to accordingly update the parameters as well.

Please note that the code here only calls the API end point that starts the execution of the query. To fetch the data generated from the execution of this query, you would need to call other API endpoints. See the [API Reference](../api-reference/authentication.md) section to learn more about various endpoints the Dune API currently offers.

!!! Link to Code
    You can also find some code from this tutorial in this [Github Repository](https://github.com/SusmeetJain/dune_api_js).
