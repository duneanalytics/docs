[View code on GitHub](https://dune.com/blob/master/api\api-reference\execution-status.md)

# Execution Status

This technical guide explains how to check the status of an execution request in the Dune Docs project. The guide is focused on the `app` folder of the project. The guide provides a detailed explanation of the `GET` Execution Status API request, including its arguments, returns, example request, and example response.

The Arguments section of the guide explains that no arguments are required for the API request. The Returns section explains that the API request returns the status of a query execution along with relevant metadata of the results if the execution is completed.

The Example Request section provides an example of how to pass the `execution_id` obtained from making an Execute Query ID POST request to complete an Execution Status API request. The example shows the endpoint URL and the cURL command to make the request.

The Example Response section provides two examples of the JSON response that the API request returns. The first example shows the response when the query is still executing, while the second example shows the response when the execution is complete. The section explains the meaning of each property in the response, including `execution_id`, `query_id`, `state`, `submitted_at`, `expires_at`, `execution_started_at`, `execution_ended_at`, and `result_metadata`.

The guide also includes a Check Execution Status FAQ section that answers common questions about the different status codes for `state`. The section explains the difference between the states "Executing" and "Pending" and provides a list of all status codes for reference.

Overall, this technical guide provides a comprehensive explanation of how to check the status of an execution request in the Dune Docs project. It is a useful resource for developers who need to monitor the progress of their query executions.
## Questions: 
 1. What is the purpose of this API and how does it relate to blockchain technology?
   - This API is used to check the status of a query execution request. It is not directly related to blockchain technology, but it could potentially be used in conjunction with blockchain data queries.
2. What authentication methods are required to use this API?
   - The cURL example shows that an API key is required to make requests to this API. It is unclear from this documentation whether any other authentication methods are supported.
3. Are there any limitations on the size or complexity of queries that can be executed using this API?
   - The documentation does not provide any information on limitations for query size or complexity. A blockchain SQL analyst may need to test the API with various query types and sizes to determine any potential limitations.