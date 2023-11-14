---
title: Python
description: Here's how to access the Dune API via Python.
---

Let's get started using the Dune API via Python!

In this example we'll be using Python3. We recommend using a virtual environment and the `pip` package manager.

!!! example "Prerequisites"
    This Quick Start Guide assumes you have some prior experience using Python, though we aimed to make the code here easy to follow. If you have questions, please reach out to our team via the #[dune-api](https://discord.com/channels/757637422384283659/1019910980634939433) channel on Discord.

## Python SDK - Quickstart


The following code demo

### Install & Setup

```sh
pip install dune-client
```

Export your `DUNE_API_KEY` or place it in a `.env` file like so:

```
# Required
DUNE_API_KEY=

# Optional (defaults provided here)
DUNE_API_BASE_URL=https://api.dune.com
DUNE_API_REQUEST_TIMEOUT=10
```

and `source .env`.

#### run_query

This is a combination of `execute_query` which waits for completion, followed by `get_execution_results`

```python
from dune_client.types import QueryParameter
from dune_client.client import DuneClient
from dune_client.query import QueryBase

query = QueryBase(
    name="Sample Query",
    query_id=1215383,
    params=[
        QueryParameter.text_type(name="TextField", value="Word"),
        QueryParameter.number_type(name="NumberField", value=3.1415926535),
        QueryParameter.date_type(name="DateField", value="2022-05-04 00:00:00"),
        QueryParameter.enum_type(name="EnumField", value="Option 1"),
    ],
)
print("Results available at", query.url())

dune = DuneClient.from_env()
results = dune.run_query(query)

# or as CSV
# results_csv = dune.run_query_csv(query)

# or as Pandas Dataframe
# results_df = dune.run_query_dataframe(query)
```

#### run_sql

Create and run your query entirely from your IDE! The run query method is a hybrid of (create, execute, get_results and optionally archive after). 

```py
from dune_client.types import QueryParameter
from dune_client.client import DuneClient

expensive_transactions = """
	SELECT block_time, hash,
    FROM {{Blockchain}}.transactions
    ORDER BY CAST(gas_used as uint256) * CAST(gas_price AS uint256) DESC
    LIMIT {{N}}"""

client = DuneClient.from_env()
results = client.run_sql(
	query_sql=expensive_transactions, 
	params=[
		QueryParameter.text_type("Blockchain", "ethereum"), 
		QueryParameter.number_type("N", 10)
	])
```

### Further Examples

There [client project repo](https://github.com/duneanalytics/dune-client) contains extensive [end-to-end testing](https://github.com/duneanalytics/dune-client/blob/main/tests/e2e/test_client.py) of all available API routes.

## API Breakdown

The `DuneClient` is composed of 

- [`ExecutionAPI`](https://github.com/duneanalytics/dune-client/blob/05787719526a441e39baf6252adf531bf941cd98/dune_client/api/execution.py#L24-L27) for query execution and result fetching functions.

<details><summary>Details</summary>

```py
def execute_query(
    self, query: QueryBase, performance: Optional[str] = None
) -> ExecutionResponse:
    """Post's to Dune API for execute `query`"""

def cancel_execution(self, job_id: str) -> bool:
    """POST Execution Cancellation to Dune API for `job_id` (aka `execution_id`)"""

def get_execution_status(self, job_id: str) -> ExecutionStatusResponse:
    """GET status from Dune API for `job_id` (aka `execution_id`)"""

def get_execution_results(self, job_id: str) -> ResultsResponse:
    """GET results from Dune API for `job_id` (aka `execution_id`)"""

def get_execution_results_csv(self, job_id: str) -> ExecutionResultCSV:
    """
    GET results in CSV format from Dune API for `job_id` (aka `execution_id`)

    this API only returns the raw data in CSV format, it is faster & lighterweight
    use this method for large results where you want lower CPU and memory overhead
    if you need metadata information use get_results() or get_status()
    """

def get_results_dataframe(self, job_id: str) -> Any:
    """
    Get query results as a pandas dataframe (requires manual installation of pandas)
    """
```
</details>

- [`QueryAPI`](https://github.com/duneanalytics/dune-client/blob/05787719526a441e39baf6252adf531bf941cd98/dune_client/api/query.py#L16-L20) for CRUD Operations (available with premium subscription only).


<details><summary>QueryAPI Details</summary>

```py
def create_query(
    self,
    name: str,
    query_sql: str,
    params: Optional[list[QueryParameter]] = None,
    is_private: bool = False,
) -> DuneQuery:
    """
    Creates Dune Query by ID
    https://dune.com/docs/api/api-reference/edit-queries/create-query/
    """

def get_query(self, query_id: int) -> DuneQuery:
    """
    Retrieves Dune Query by ID
    https://dune.com/docs/api/api-reference/edit-queries/get-query/
    """

def update_query(
    self,
    query_id: int,
    name: Optional[str] = None,
    query_sql: Optional[str] = None,
    params: Optional[list[QueryParameter]] = None,
    description: Optional[str] = None,
    tags: Optional[list[str]] = None,
) -> int:
    """
    Updates Dune Query by ID
    https://dune.com/docs/api/api-reference/edit-queries/update-query

    The request body should contain all fields that need to be updated.
    Any omitted fields will be left untouched.
    If the tags or parameters are provided as an empty array,
    they will be deleted from the query.
    """

def archive_query(self, query_id: int) -> bool:
    """
    https://dune.com/docs/api/api-reference/edit-queries/archive-query
    returns resulting value of Query.is_archived
    """

def unarchive_query(self, query_id: int) -> bool:
    """
    https://dune.com/docs/api/api-reference/edit-queries/archive-query
    returns resulting value of Query.is_archived
    """

def make_private(self, query_id: int) -> None:
    """
    https://dune.com/docs/api/api-reference/edit-queries/private-query
    """

def make_public(self, query_id: int) -> None:
    """
    https://dune.com/docs/api/api-reference/edit-queries/private-query
    """
```

</details>

- [`ExtensionAPI`](https://github.com/duneanalytics/dune-client/blob/05787719526a441e39baf6252adf531bf941cd98/dune_client/api/extensions.py#L30-L34) provides high-level helper methods as compositions of functionality from the `ExecutionAPI` and `QueryAPI` classes.

<details><summary>ExtensionAPI Details</summary>

```py
def run_query(
    self,
    query: QueryBase,
    ping_frequency: int = 5,
    performance: Optional[str] = None,
) -> ResultsResponse:
    """
    Executes a Dune `query`, waits until execution completes,
    fetches and returns the results.
    Sleeps `ping_frequency` seconds between each status request.
    """

def run_query_csv(
    self,
    query: QueryBase,
    ping_frequency: int = 5,
    performance: Optional[str] = None,
) -> ExecutionResultCSV:
    """
    Executes a Dune query, waits till execution completes,
    fetches and the results in CSV format
    (use it load the data directly in pandas.from_csv() or similar frameworks)
    """

def run_query_dataframe(
    self,
    query: QueryBase,
    ping_frequency: int = 5,
    performance: Optional[str] = None,
) -> Any:
    """
    Execute a Dune Query, waits till execution completes,
    fetched and returns the result as a Pandas DataFrame

    This is a convenience method that uses run_query_csv() + pandas.read_csv() underneath
    """

def get_latest_result(
    self,
    query: Union[QueryBase, str, int],
    max_age_hours: int = THREE_MONTHS_IN_HOURS,
) -> ResultsResponse:
    """
    GET the latest results for a query_id without re-executing the query
    (doesn't use execution credits)

    :param query: :class:`Query` object OR query id as string or int
    :param max_age_hours: re-executes the query if result is older than max_age_hours
        https://dune.com/docs/api/api-reference/get-results/latest-results
    """

def download_csv(self, query: Union[QueryBase, str, int]) -> ExecutionResultCSV:
    """
    Almost like an alias for `get_latest_result` but for the csv endpoint.
    https://dune.com/docs/api/api-reference/get-results/latest-results
    """

############################################################################
# Below features use APIs that are only available on paid subscription plans
############################################################################

###############
# Plus Features
###############

def upload_csv(self, table_name: str, data: str, description: str = "") -> bool:
    """
    https://dune.com/docs/api/api-reference/upload-data/?h=data+upload#endpoint
    The write API allows you to upload any .csv file into Dune. The only limitations are:

    - File has to be < 200 MB
    - Column names in the table can't start with a special character or digits.
    """

##################
# Premium Features
##################

def run_sql(
    self,
    query_sql: str,
    params: Optional[list[QueryParameter]] = None,
    is_private: bool = True,
    archive_after: bool = True,
) -> ResultsResponse:
    """
    Allows user to provide execute raw_sql via the CRUD interface
    - create, run, get results with optional archive/delete.
    - Query is by default made private and archived after execution.
    Requires premium subscription!
    """
```
</details>


## Raw Requests

If you want to understand the details or proceed without the client library, then check out the full walkthrough using HTTP requests [here](./python/raw-walkthrough.md).
