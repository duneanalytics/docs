[View code on GitHub](https://dune.com/blob/master/api\quick-start\api-py.md)

This app technical guide covers how to access the Dune API using Python. It provides a step-by-step guide to set up the environment, install necessary libraries, and create functions to interact with the Dune API. The guide assumes prior experience with Python and recommends using Python3, a virtual environment, and the `pip` package manager.

The guide covers the following sections:

1. **Getting Set Up**: Installing the `requests`, `pandas`, and `jupyter notebook` libraries.
2. **Import the necessary libraries**: Importing `requests` and `pandas`.
3. **API Keys**: Setting up the API key and header for making API calls.
4. **Simplifying URL generation**: Creating a function to generate URLs for different API endpoints.
5. **Wrapping API endpoints in functions**: Defining functions to execute a query, get query status, get query results, and cancel query execution.
6. **Using the Dune API**: Demonstrating how to execute a query, get query execution status, get query results, and cancel query execution.
7. **Parameterized Queries**: Creating a function to execute queries with parameters.

The guide provides examples for each section, making it easy to follow and implement the code. The complete code for this tutorial is available on [GitHub](https://github.com/SusmeetJain/dune_api_python).
## Questions: 
 1. **How do I pass my API key to the Dune API?**

   You need to pass your API key in the header of your API calls. In the example provided, the API key is stored in a variable called `API_KEY`, and the header is created as a dictionary: `HEADER = {"x-dune-api-key" : API_KEY}`.

2. **How can I execute a parameterized query using the Dune API?**

   To execute a parameterized query, you need to create a dictionary containing the parameter values and pass it to the `execute_query_with_params` function along with the query ID. For example: `parameters = {"wallet_address" : "0xb10f35351ff21bb81dc02d4fd901ac5ae34e8dc4"}` and `execution_id = execute_query_with_params("638435", parameters)`.

3. **How can I cancel a query execution if it's taking too long?**

   You can cancel a query execution by calling the `cancel_query_execution` function and passing the `execution_id` of the running query. For example: `response = cancel_query_execution(execution_id)`.