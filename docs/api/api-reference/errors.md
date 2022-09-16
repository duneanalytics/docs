---
title: Handling Errors
description: Here's how to .
---

The amazing thing is, you are very early.
Now that also means, we are still working on getting the details right.

Our API at the moment, doesn't always throw error messages. So in a lot of cases, when things do not work as expected, you would need to decipher that from our response objects.

!!! Note
    If this is too technical/ difficult for you, you don't need to break you head, just reach out to us on Discord over the #dune-api channel. And we will help you where ever you are stuck!

Here are a few common scenarios. 

### Response Object

```
 {'error': 'invalid API Key'}
```

#### Checks
 
  -  Make sure that you are passing the API key to our end point *in a header*. See the section on Authentication for what that means. And our quick start guides for specific language examples.
  - If you are already passing the API key in an header, make sure that it is correctly entered.

### Response Object

```
 {'error': 'An internal error occured'}
```
#### Checks

  - If you are using our GET endpoint, ensure that the query ID you have entered is correct.
  - If you are using one of our POST endpoints, ensure that the execution ID you obtained from the GET endpoint has been correctly passed on to this endpoint.


The documentation here isn't exhaustive, while we are working on making it better, we will repeat ourselves, the best place to get any support is our Discord channel.