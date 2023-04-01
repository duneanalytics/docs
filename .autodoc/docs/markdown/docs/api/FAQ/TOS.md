[View code on GitHub](https://dune.com/docs/api/FAQ/TOS.md)

# Dune API TOS

This section of the app technical guide covers the Dune API Terms of Service (TOS). The TOS outlines the rules and guidelines for using the Dune API. It is important for developers to understand and comply with these terms in order to use the API effectively and avoid any legal issues.

The header provides a link to the actual API TOS document, which is hosted on the Dune website. Developers should review this document thoroughly before using the API.

Example:

```
// Make a request to the Dune API
fetch('https://api.dune.com/data')
  .then(response => {
    // Handle response
  })
  .catch(error => {
    // Handle error
  });
```

# Authentication

This section covers the authentication process for accessing the Dune API. Developers must obtain an API key in order to access the API. The header provides an overview of the authentication process and links to additional resources for obtaining an API key.

Example:

```
// Set API key as authorization header
const headers = {
  'Authorization': 'Bearer YOUR_API_KEY_HERE'
};

// Make a request to the Dune API with headers
fetch('https://api.dune.com/data', { headers })
  .then(response => {
    // Handle response
  })
  .catch(error => {
    // Handle error
  });
```

# Rate Limiting

This section covers the rate limiting policy for the Dune API. The API has a limit on the number of requests that can be made within a certain time period. The header provides an overview of the rate limiting policy and links to additional resources for understanding and managing rate limits.

Example:

```
// Check if rate limit has been reached
if (response.headers.get('X-RateLimit-Remaining') === '0') {
  // Handle rate limit reached error
}
```

Overall, this app technical guide provides important information for developers using the Dune API. It covers the API TOS, authentication process, and rate limiting policy, which are all crucial aspects of using the API effectively and responsibly.
## Questions: 
 1. What specific APIs does Dune Docs offer and what are their respective terms of service?
- The app technical guide only provides a link to the API terms of service page, so a blockchain SQL analyst may want to know more about the specific APIs offered by Dune Docs and their corresponding terms of service.

2. Does Dune Docs have any restrictions or limitations on the usage of their APIs?
- The app technical guide does not provide any information on restrictions or limitations on API usage, so a blockchain SQL analyst may want to know if there are any such restrictions in place.

3. Is there any documentation available on how to integrate Dune Docs APIs into a blockchain SQL project?
- The app technical guide only provides a link to the API terms of service page, so a blockchain SQL analyst may want to know if there is any additional documentation available on how to integrate Dune Docs APIs into their project.