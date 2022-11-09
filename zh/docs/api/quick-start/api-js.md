---
title: Javascript
description: Here's how to access the Dune API via JavaScript.
---

!!! Warning
    This guide is not yet comprehensive. If you have questions, please reach out to our team via the #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) channel on Discord.

Let's get started using the Dune API via JavaScript!

We'll show you one of the several ways the API can be consumed via JavaScript, in this case using the `node-fetch` package.

!!! example "Prerequisites"
    This Quick Start Guide assumes you have some level of familiarity with Node.js (Node), Node Package Manager (NPM) and Node Version Manager (NVM).

To start, make sure you're using the current LTS version of Node.js (Node 16) and the latest version of NPM:

## Getting Set Up

```
nvm use lts
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

Just run this script to get a response from the Dune API:

```
node main.js
```
You should see a response being returned on your command line.

For the example here, we have used a simple example Query that fetches a small set of data:`query_id: 1258228`
You can also edit the Query URL to fetch data from any other Queries you'd like! 🪄

The code here only calls the API end point that starts the execution of the query. To fetch the data generated from the execution of this query, you would need to call other API endpoints. See the [API Reference](../api-reference/authentication.md) section to learn more about various endpoints the Dune API currently offers.

!!! Complete-Code
    The complete code for this tutorial is available on [this link](https://github.com/SusmeetJain/dune_api_js).
