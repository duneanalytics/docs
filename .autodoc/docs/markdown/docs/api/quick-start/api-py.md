[View code on GitHub](https://dune.com/docs/api/quick-start/api-py.md)

This app technical guide covers how to access the Dune API using Python. It provides a step-by-step guide to set up the environment, install necessary libraries, and create functions to interact with the Dune API. The guide assumes prior experience with Python and covers the following topics:

1. **Getting Set Up**: Installing the `requests`, `pandas`, and `jupyter notebook` libraries using `pip`.
2. **Importing Libraries**: Importing the `requests` and `pandas` libraries.
3. **API Keys**: Setting up the API key and header for making API calls.
4. **Simplifying URL Generation**: Creating a function to generate URLs for different API endpoints.
5. **Wrapping API Endpoints in Functions**: Defining functions to execute queries, get query status, get query results, and cancel query execution.
6. **Using the Dune API**: Demonstrating how to execute a query, get query execution status, get query results, and cancel query execution.
7. **Parameterized Queries**: Defining a function to execute queries with parameters and demonstrating its usage.

The guide includes examples of function calls and their expected outputs, making it easy for users to follow along and interact with the Dune API using Python.
## Questions: 
 1. **How do I pass my API key to the Dune API?**

   You need to pass your API key in the header of your API calls. In the provided code, you can set your API key in the `API_KEY` variable and the header is set in the `HEADER` variable as `{"x-dune-api-key" : API_KEY}`.

2. **How can I execute a parameterized query using the provided functions?**

   You can use the `execute_query_with_params` function to execute a parameterized query. You need to pass the `query_id` and a dictionary containing the parameter values as arguments to this function.

3. **How can I cancel the execution of a running query?**

   You can use the `cancel_query_execution` function to cancel the execution of a running query. You need to pass the `execution_id` of the running query as an argument to this function.