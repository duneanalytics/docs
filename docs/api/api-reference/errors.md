---
title: Errors Codes
description: Here's how to handle errors that may come up when working with the Dune API.
---

Dune uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided. Codes in the `5xx` range indicate an error with Dune's servers (these are rare).

## Common Error Code Summary
| Method      | Description                                                   |
| ----------- | ------------------------------------------------------------- |
| `400`       | Invalid request                                               |
| `402`       | Reached maximum number of private queries                     |
| `403`       | Not allowed to create or update this query                    |
| `404`       | Query not found, or it’s private and belongs to somebody else |
| `409`       | Query was updated in the meantime (this is currently never returned, but might be in the future if we add the version parameter or a nonce to the request) |

## Invalid API Key

### Response Object

```
 {'error': 'invalid API Key'}
```

#### Checks
 
  -  Make sure that you are passing your API key to our endpoint *in a header*. See the section on [Authentication](../api-reference/authentication.md) for how to do that, and our [quick start guides](../quick-start/api-py.md) for specific language examples.
  - If you are already passing the API key in an header, make sure that it is correctly entered.


## An Internal Error Occurred

### Response Object

```
 {'error': 'An internal error occurred'}
```
#### Checks

  - If you are using one of our GET endpoints, ensure that the `query_id` you have entered is correct.
  - If you are using one of our POST endpoints, ensure that the `execution_id` you obtained from your GET endpoint has been correctly passed on to your POST endpoint.


In cases when things do not work as expected, please reach out to us on the [#dune-api Discord channel](https://discord.com/channels/757637422384283659/1019910980634939433) and we'll help out when you're stuck!