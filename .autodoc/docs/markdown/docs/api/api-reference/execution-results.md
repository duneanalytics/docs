[View code on GitHub](https://dune.com/docs/api/api-reference/execution-results.md)

This technical guide provides information on how to obtain the results data of an execution request in the Dune Docs project. The guide is focused on the Execution Results API feature of the app. The guide provides details on how to make a GET request to the API endpoint to retrieve the status, metadata, and query results from a query execution. 

The guide provides an example request that requires passing the `execution_id` obtained from making an Execute Query ID POST request. The guide also provides an example cURL request. The guide further provides an example response in JSON format, which includes details such as the execution ID, query ID, state, submitted time, execution start and end times, and the actual rows of data being returned. The metadata of the queried data being returned is also included in the response. The metadata includes details such as the names of the columns in the data returned, the size of the returned data, the number of rows in the data, the total number of datapoints returned, the time it took to assign a slot in the server for the request, and the time it took for the actual execution of the query with the request. 

The guide also provides an example of how to get the results in CSV format by appending "/csv" to the URL pattern. The guide advises against using the API key as a parameter in public documents where the API key can be viewed and compromised. 

Finally, the guide provides a FAQ section that answers questions such as whether data can be ingested by getting a direct connection to the database, whether query results data are saved for faster retrieval, how long the results data from an execution are stored for, and how much data can be retrieved in a single API result call. 

In summary, this technical guide provides developers with a detailed explanation of how to obtain the results data of an execution request in the Dune Docs project. The guide provides examples of requests and responses, as well as a FAQ section that answers common questions.
## Questions: 
 1. What is the purpose of the Dune Docs app and how does it relate to blockchain technology?
- The app technical guide does not provide information on the overall purpose of the Dune Docs app, so a blockchain SQL analyst may need to seek additional documentation or context to understand how it relates to blockchain technology.

2. How does the Dune Docs app handle security and authentication for API requests?
- The app technical guide does not provide information on security and authentication measures for API requests, so a blockchain SQL analyst may need to seek additional documentation or context to understand how the app handles these aspects.

3. What is the pricing model for using the Dune Docs app and how does it compare to other blockchain data analysis tools?
- The app technical guide does not provide information on the pricing model for using the Dune Docs app, so a blockchain SQL analyst may need to seek additional documentation or context to understand the costs associated with using the app and how it compares to other blockchain data analysis tools.