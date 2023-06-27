[View code on GitHub](https://dune.com/docs/api/api-reference/get-results/execution-status.md)

# Explanation of Execution Status App Technical Guide

The Execution Status technical guide is a part of the Dune Docs project and provides information on how to check the status of an execution request. The guide is located in the app folder of the project and is focused on the app feature that allows users to execute queries and check their status. 

The guide provides a detailed explanation of how to use the GET Execution Status API request to check the status of a query execution. It includes information on the arguments and returns of the API request, as well as an example request and response. 

The Arguments section of the guide explains that there are no arguments required for the Execution Status API request. The Returns section explains that the API request returns the status of a query execution along with relevant metadata of the results if the execution is completed. 

The Example Request section provides an example of how to pass the execution_id obtained from making an Execute Query ID POST request to complete an Execution Status API request. It includes both a URL and cURL example. 

The Example Response section provides two examples of JSON responses that can be returned by the Execution Status API request. The first example shows the response when the query is still executing, while the second example shows the response when the execution is complete. The section also provides a detailed explanation of the different properties of the response data, such as execution_id, query_id, state, submitted_at, expires_at, execution_started_at, execution_ended_at, and result_metadata. 

Finally, the Check Execution Status FAQ section provides answers to common questions about the different states of query execution, such as "Executing" and "Pending". It also provides a list of all status codes for reference. 

Overall, the Execution Status technical guide provides a comprehensive explanation of how to check the status of a query execution using the Execution Status API request. It is a useful resource for developers working on the Dune Docs project who need to understand how to use this feature of the app.
## Questions: 
 1. What is the purpose of this API and how does it relate to blockchain technology?
   - This API is used to check the status of a query execution request. It is not directly related to blockchain technology, but it may be used in conjunction with blockchain data analysis.
2. What authentication is required to make requests to this API?
   - The cURL example shows that an API key is required to make requests to this API. A blockchain SQL analyst may want to know how to obtain an API key and what level of access it provides.
3. What is the maximum size of the response data that can be generated with this request?
   - The `result_set_bytes` property in the `result_metadata` object indicates the size of the response data in bytes, but it does not specify a maximum size. A blockchain SQL analyst may want to know if there are any limitations on the amount of data that can be returned by this API.