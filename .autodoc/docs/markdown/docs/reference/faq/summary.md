[View code on GitHub](https://dune.com/docs/reference/faq)

The `docs/reference/faq` folder contains a collection of app technical guides that answer frequently asked questions about the Dune project. These guides provide valuable information for users who want to understand various aspects of Dune, such as its data sources, API access, and result refreshing mechanisms.

For example, the `does-dune-have-a-token.md` guide clarifies that Dune does not have a token, which is essential for users looking to integrate Dune with other applications or services that require token-based authentication. This information helps users adjust their integration plans and explore alternative authentication methods.

The `does-dune-have-an-api.md` guide confirms that Dune has an API and provides information on how to access it. Users must sign up for a paid plan and add on API access to use the API. This guide also provides links to pricing details and more in-depth information on using the API, such as authentication, endpoints, and data formats. This guide is useful for users who want to retrieve data from Dune programmatically, for example, to obtain a list of all companies in Dune's database.

In the `how-are-results-refreshing.md` guide, users can learn about the result refreshing mechanism in the Dune app. The guide explains that when a visualization is viewed on a query page or dashboard, Dune checks the age of the most recent result. If the result is older than three hours, Dune automatically queues an execution for the query and runs it in the background. This ensures that dashboards are always up to date when viewed, without the need for the query creator to set a refresh schedule.

Lastly, the `how-does-dune-get-its-data.md` guide offers an overview of how Dune obtains its data by working with node providers across the industry to ingest raw historical data from various blockchains. The guide also explains how users can submit their own smart contracts for decoding via the decoding page, provided they have an ABI. This information is useful for users who want to understand Dune's data sources and work with smart contracts on the platform.

Overall, the guides in the `docs/reference/faq` folder provide concise and relevant information for users who want to understand various aspects of the Dune project. These guides are essential for analysts who are curious about using the project and need clarification on specific features or functionalities.
