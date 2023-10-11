---
title: Create Sankey Diagram
description: How to create Sankey diagram with Dune's data
---

While Dune's ability to easily execute queries and make visualizations are pretty neat, as of today (Sep. 29, 2023), you are not able to create Sankey diagrams on Dune yet. So in this guide, we will quickly show you how to use Dune API to fetch data and Python libraries to make Sankey diagrams.

!!! note
    This example uses the Dune Python client, which can [be found here](https://github.com/duneanalytics/dune-client) and installed by doing `pip install dune-client`

## 🎓 What is a Sankey Diagram?
Sankey diagrams are flow diagrams in which the width of the arrows or lines are proportional to the flow quantity they represent. They're commonly used to depict the flow of energy, material, or costs between stages. So if you've been longing to visualize the movement of tokens between wallets, or how users transition between different app states, a Sankey diagram is your weapon of choice!

For a deeper dive, [check this article](https://medium.com/@twelsh37/understanding-plotly-sankey-charting-3ee263a81549).

### Expected Data Input:
The key components for a Sankey are:

- Source & Target: Indexes of where the flow starts and where it ends.
- Value: The quantity of flow between the source and target.

## ⛲ Let's Generate that Sankey!

Here, we will walk through two examples. Example 1 is to graph a Sankey for a certain subset of RabbitHole Quests with Optimism grant, see how the questors are retained after 1 month period. Example 2 is to graph a Sankey for the token flow when swapping USDC for WETH using Uniswap if the swap is not direct. 

We will show you different ways to fetch data from Dune API in the process as well. 

### 1. Setup
Import all necessary libraries and authenticate to set up DuneClient.

!!! note 
    1. Make sure you create have a .env file created with your 'DUNE_API_KEY' in it! 
    2. Replace the path to your own directory in `os.chdir(...)`

``` py
import pandas as pd
import plotly.graph_objects as go
import colorlover as cl
import pandas as pd
import dotenv, os, json
from dune_client.types import QueryParameter
from dune_client.client import DuneClient
from dune_client.query import QueryBase

# change the current working directory where .env file lives
os.chdir("...") # please replace with path to your own current directory
# load .env file
dotenv.load_dotenv(".env")
# setup Dune Python client
dune = DuneClient.from_env()
```

### 2. Fetch the data for Sankey 

=== "Example 1:  Get query result by fetching the latest result executed"

    ``` py
        query_result = dune.get_latest_result(3055630, max_age_hours=72)
        query_result = pd.DataFrame(query_result.result.rows)
    ```

=== "Example 2: Run query execution with param to get query result"

    ``` py
        query = QueryBase(
            name="Flow of tokens when swapping on Uniswap (Ethereum chain)",
            query_id=3062941,
            params=[
                QueryParameter.text_type(name="include_direct_swap", value="false"),
                QueryParameter.number_type(name="threshold", value=50),
                QueryParameter.text_type(
                    name="token_A_address", value="0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48" # USDC address
                ),
                QueryParameter.text_type(
                    name="token_B_address", value="0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2" # WETH address
                ),
            ],
        )
        query_result = dune.run_query_dataframe(query=query, performance="large") # specify large cluster for faster runtime
    ```

### 3. Customize colors, if needed 

=== "Example 1"

    ``` py
        predefined_colors = {
            'velodrome': 'rgb(66, 135, 245)',
            'beethoven': 'rgb(245, 66, 78)',
            'clipper': 'rgb(226, 194, 88)',
            'matcha': 'rgb(156, 217, 177)',
            'uniswap': 'rgb(209, 21, 102)',
            'rabbithole': 'rgb(112, 24, 225)'
        }
    ```

=== "Example 2"

    ``` py
        predefined_colors = {
            "USDC": "rgb(38, 112, 196)",
            "USDT": "rgb(0, 143, 142)",
            "WETH": "rgb(144, 144, 144)",
            "WBTC": "rgb(247, 150, 38)",
            "COMP": "rgb(32, 217, 152)",
            "DAI": "rgb(254, 175, 48)",
            "MKR": "rgb(38, 173, 158)",
            "UNI": "rgb(255, 21, 126)",
        }
    ```

### 4. Define the function to make Sankey diagram 

```py
# function to create Sankey diagram
def create_sankey(
    query_result: pd.DataFrame,
    predefined_colors: dict,
    columns: dict,
    viz_config: dict,
    title: str = "unnamed",
):
    """
    Creates a Sankey diagram based on input query_result
    , which must contain source, target, value columns
    """
    # Check if the dataframe contains required columns
    required_columns = [columns["source"], columns["target"], columns["value"]]
    for col in required_columns:
        if col not in query_result.columns:
            raise ValueError(f"Error: The dataframe is missing the '{col}' column")

    # Check if 'value' column is numeric
    if not pd.api.types.is_numeric_dtype(query_result[columns["value"]]):
        raise ValueError("Error: The 'value' column must be numeric")

    # preprocess query result dataframe
    all_nodes = list(
        pd.concat(
            [query_result[columns["source"]], query_result[columns["target"]]]
        ).unique()
    )
    # In Sankey, 'source' and 'target' must be indices. Thus, you need to map projects to indices.
    query_result["source_idx"] = query_result[columns["source"]].map(all_nodes.index)
    query_result["target_idx"] = query_result[columns["target"]].map(all_nodes.index)

    # create color map for Sankey
    colors = cl.scales["12"]["qual"]["Set3"]  # default color
    color_map = {}
    for node in all_nodes:
        for name, color in predefined_colors.items():
            if name.lower() in node.lower():  # check if name exists in the node name
                color_map[node] = color
                break
        else:
            color_map[node] = colors[
                len(color_map) % len(colors)
            ]  # default color assignment

    fig = go.Figure(
        go.Sankey(
            node=dict(
                pad=viz_config["node_pad"],
                thickness=viz_config["node_thickness"],
                line=dict(color="black", width=viz_config["node_line_width"]),
                label=all_nodes,
                color=[
                    color_map.get(node, "blue") for node in all_nodes
                ],  # customize node color
            ),
            link=dict(
                source=query_result["source_idx"],
                target=query_result["target_idx"],
                value=query_result[columns["value"]],
                color=[
                    color_map.get(query_result[columns["source"]].iloc[i], "black")
                    for i in range(len(query_result))
                ],  # customize link color
            ),
        )
    )
    fig.update_layout(
        title_text=title,
        font_size=viz_config["font_size"],
        height=viz_config["figure_height"],
        width=viz_config["figure_width"],
    )

    return fig
```

### 5. Plot the Sankey!

=== "Example 1"

    ``` py
        create_sankey(
            query_result=query_result,
            predefined_colors=predefined_colors,
            columns={"source": "source", "target": "target", "value": "value"},
            viz_config={
                "node_pad": 15,
                "node_thickness": 20,
                "node_line_width": 0.5,
                "font_size": 12,
                "figure_height": 800,
                "figure_width": 1000   
            },
            title="RabbitHole OP Grant questors to retained users after 1 month by project"
        ).show()
    ```

=== "Example 2"

    ``` py
        create_sankey(
            query_result=query_result,
            predefined_colors=predefined_colors,
            columns={"source": "source", "target": "target", "value": "value"},
            viz_config={
                "node_pad": 15,
                "node_thickness": 20,
                "node_line_width": 0.5,
                "font_size": 12,
                "figure_height": 800,
                "figure_width": 1000   
            },
            title="Flow of tokens when swapping on Uniswap (Ethereum chain)"
        ).show()
    ```
