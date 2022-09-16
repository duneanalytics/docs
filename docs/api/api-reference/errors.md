---
title: Errors Codes
description: Here's how to handle errors that may come up when working with the Dune API.
---

The good news: you are very early to Dune API.  🧙‍♂️

The bad news: that means we're still working out the gremlins. 👹

For now, the Dune API doesn't always throw error messages, so in some cases when things do not work as expected you'll need to decode what happened using our response objects.

!!! Note
    If this is too technical/difficult/confusing, don't break your wand - reach out to us on the [#dune-api Discord channel](https://discord.com/channels/757637422384283659/1019910980634939433) and we'll help out when you're stuck!

Here are a few common error scenarios:

## Invalid API Key

### Response Object

```
 {'error': 'invalid API Key'}
```

#### Checks
 
  -  Make sure that you are passing your API key to our endpoint *in a header*. See the section on [Authentication](../api-reference/authentication) for how to do that, and our [quick start guides](../quick-start/api-py) for specific language examples.
  - If you are already passing the API key in an header, make sure that it is correctly entered.


## An Internal Error Occurred

### Response Object

```
 {'error': 'An internal error occurred'}
```
#### Checks

  - If you are using one of our GET endpoints, ensure that the `query_id` you have entered is correct.
  - If you are using one of our POST endpoints, ensure that the `execution_id` you obtained from your GET endpoint has been correctly passed on to your POST endpoint.


The documentation here isn't exhaustive!

While we are working on making it better, again, the best place to get any support is our [#dune-api Discord channel](https://discord.com/channels/757637422384283659/1019910980634939433).