---
title: Farcaster Social Network Analysis 
description: How to conduct social network analysis for Farcaster with Dune API and Python (summary statistics, centrality measures, graph sampling, and community detection)
---

In the age of digital interconnectivity, platforms like Facebook and Instagram leverage the intricate webs of user relationships to drive their strategies, from identifying top influencers to deploying targeted ads to deciding what content to recommend on user's feed. Yet, obtaining and analyzing real-world social network data is no small feat. For those with a budding interest in graph theory or network analysis, this guide will pave your path. Delve deep as we walk you through analyzing data from Farcaster, a fully decentralized social network, using Python and the Dune API. It's a unique opportunity that many platforms guard closely.

👣 In this guide, we'll cover the basics of network analysis in four parts: (1) 📊 summary statistics, (2) 📏 centrality measures, (3) 🔍 graph sampling, and (4) 🏘️ community detection.

📌 Dive into our [Github notebook](https://github.com/duneanalytics/python-notebook-examples/blob/main/social_network/Farcaster%20Network%20Analysis%20(Summary%20Stats%2C%20Centrality%20Measures%2C%20Sampling%2C%20%26%20Community%20Detection).ipynb) to actively follow the code as you navigate this guide.

!!! note
    - This example uses the Dune Python client, a framework for interacting with Dune's official API. Dune Client can [be found here](https://github.com/duneanalytics/dune-client) and installed by doing `pip install dune-client`

    - Credit consumption for each Dune API action is estimated and printed out with a ⛽ symbol. To learn more about credit, [please visit this page](./how-tos/credit-system-on-dune.md).

    - The network was constructed using one month of Farcaster data, ending on October 23, 2023.

## Prerequisite

- This guide assumes you have basic understanding of what a graph, or a network is, including terminology like nodes, edges, weights, and directions. 
- If you need help here, please try resources like Medium and YouTube, which are just a Google search away. 
- If you need a specific recommendation, check this out, in both [written format](https://towardsdatascience.com/social-network-analysis-from-theory-to-applications-with-python-d12e9a34c2c7) and [video format](https://www.youtube.com/watch?v=px7ff2_Jeqw )  

## Setups and Dataset

### Construct Dataset
To build a network, we need nodes and their relationships. Refer to [this Dune query](https://dune.com/queries/3078764?category=third_party_data&schema=neynar&catalog=dune) for data required.

- Nodes are identified by a unique "fid" (Farcaster ID).
- Relationships (edges) between nodes are based on four actions: follow, like, repost, and comment.
- Interaction weights are: follow = 5, like = 1, repost = 3, comment = 2. They consider directionality.
- These interactions as parameterized variables, adjust as needed.

### Packages and Imports

Install required packages with:

```bash
pip install -r requirements.txt
```

This is the content in [requirements.txt](https://github.com/duneanalytics/python-notebook-examples/blob/main/social_network/requirements.txt):
```txt
pandas
networkx
python-louvain
matplotlib
plotly
python-dotenv
dune-client
nltk
```

Then, load necessary libraries: 
```py
import pandas as pd 
import networkx as nx 
import community as community_louvain
from networkx import community
import matplotlib.pyplot as plt 
import plotly.graph_objects as go
import dotenv, os, json
from dune_client.types import QueryParameter
from dune_client.client import DuneClient
from dune_client.query import QueryBase
from multiprocessing import Pool
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from collections import Counter
import random
import itertools
import warnings

nltk.download('stopwords')
nltk.download('punkt')
```

### Environment Setup for Dune API Python Client

For the Dune API, obtain an API key:

1. Go to Settings → API.
2. Select "Create new API key".
3. Copy the entire key.

<div style="position: relative; padding-bottom: calc(55.052083333333336% + 41px); height: 0; width: 100%"><iframe src="https://demo.arcade.software/f07eudjtOJz9URF8TGa5?embed" frameborder="0" loading="lazy" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;color-scheme: light;" title="how to generate API key"></iframe></div>

Set up a .env file:
```
DUNE_API_KEY=<insert your key>
DUNE_API_REQUEST_TIMEOUT=120
```
Adjust the timeout as necessary.

### Import Data into Notebook and Construct the DiGraph

There are two methods to export data from Dune and into notebook:

=== "Get Latest Result"

    Retrieve the latest result, which is faster as it bypasses execution.

    ```py 
    query_result = pd.DataFrame(dune.get_latest_result(3078764, max_age_hours=72).result.rows)
    # can call get_latest_result_dataframe once newest version of Dune Client is released
    ```

=== "Query a Query"

    Trigger a new execution, allowing flexible parameter adjustments directly from the notebook.

    ```py 
    query = QueryBase(
        name="Farcaster Centrality Measures",
        query_id=3078764,
        params=[
            # Here we can play with different weights we are assigning to each type of reaction in this directed graph
            QueryParameter.number_type(name="follow_points", value=5),
            QueryParameter.number_type(name="like_points", value=1),
            QueryParameter.number_type(name="recast_points", value=3),
            QueryParameter.number_type(name="reply_points", value=2),
            QueryParameter.number_type(name="past_n_months", value=1),
        ],
    )
    query_result = dune.run_query_dataframe(query=query, performance="large") # specify large cluster for faster runtime
    ```

To build a [DiGraph](https://networkx.org/documentation/stable/reference/classes/digraph.html#networkx.DiGraph) (graph with directed edges), simply use `NetworkX`'s [`from_pandas_edgelist` function](https://networkx.org/documentation/stable/reference/generated/networkx.convert_matrix.from_pandas_edgelist.html).

```py
G = nx.from_pandas_edgelist(query_result, 
                            source='from_user',
                            target='to_user',
                            edge_attr='total_points',
                            create_using=nx.DiGraph())
```

With our setup complete, let's dive into the summary statistics of the social network we've constructed.

## 📊 Part 1: Summary Statistics

Let's start by assessing our graph's summary statistics such as density and average degree. Through metrics like density and average degree, we see Farcaster users are sparsely connected. A plotted degree distribution and number of strongly connected components reveal few highly connected users and significant segmentation into isolated clusters.

Here's a brief code snippet. For the comprehensive version, visit the [Github notebook](https://github.com/duneanalytics/python-notebook-examples/blob/main/social_network/Farcaster%20Network%20Analysis%20(Summary%20Stats%2C%20Centrality%20Measures%2C%20Sampling%2C%20%26%20Community%20Detection).ipynb).

=== "Density"
    ```py
    density = nx.density(G)
    print(f"Density: {density:.4f}")
    ```

=== "Avg Degree" 
    ```py
    avg_degree = sum(dict(G.degree()).values()) / float(len(G.nodes))
    print(f"Average Degree: {avg_degree:.4f}")
    ```

=== "Degree Distribution"
    ```py
    degree_sequence = sorted([d for n, d in G.degree()], reverse=True)

    plt.hist(degree_sequence, bins=20)
    plt.title("Degree Distribution")
    plt.xlabel("Degree")
    plt.ylabel("Count")
    ```

=== "Strongly Connected Components" 
    ```py
    num_strongly_conn_comp = nx.number_strongly_connected_components(G)
    print(f"Number of Strongly Connected Components: {num_strongly_conn_comp}")
    ```

## 📏 Part 2: Centrality Measures
Centrality measures identify important nodes in a network, but "importance" can be defined in many ways. In this guide, we will explore: 

- **Degree Centrality**: Gauges a node's exposure by counting its connected edges.
```py
degree_centrality = nx.degree_centrality(G)
```
- **Betweenness Centrality**: Measures a node's control over communication between others.
```py
betweenness_centrality = nx.betweenness_centrality(G, normalized=True) # can add k=1000 when optimization is needed
```
- **Closeness Centrality**: Assesses how fast information spreads from one node to all others.
```py
closeness_centrality = nx.closeness_centrality(G)
```
- **Eigenvector Centrality**: Evaluates influence based on the importance of connected nodes.
```py
eigenvector_centrality = nx.eigenvector_centrality(G, max_iter=200)
```
- **PageRank**: Used by Google, it considers the structure of incoming links.
```py
pagerank = nx.pagerank(G, alpha=0.85)
```

_Again, above is a brief code snippet. For the comprehensive version, visit the [Github notebook](https://github.com/duneanalytics/python-notebook-examples/blob/main/social_network/Farcaster%20Network%20Analysis%20(Summary%20Stats%2C%20Centrality%20Measures%2C%20Sampling%2C%20%26%20Community%20Detection).ipynb)._

👑 And the influencer crown? Unsurprisingly, it goes to Farcaster's founder, Dan (dwr.eth). Of course, who else could it be? 😉

## 🎨 Bonus part: Visualizing Networks
Visualization enhances any analysis, but visualizing extensive networks like ours can be a maze. Let's navigate two visualization paths you can adapt further:

- In Gephi: [Gephi](https://gephi.org/) is a good tool to presenting large networks comprehensively. Export the graph from Python with nx.write_gml(G, "file_name.gml") and dive into Gephi. Tweak node sizes, colors, and labels to distill insights.

- In Python notebook: for a more focused lens, visualize the top 200 nodes by degree with NetworkX. Node color denotes out-degree: a blue node engages less, while a red one is more active. Node size illustrates in-degree, reflecting the interactions received.

=== "Static" 
    ```py
    # Layout
    pos = nx.spring_layout(G)

    # Node Colors (heatmap-style based on out-degree)
    out_degrees = [G.out_degree(n) for n in G.nodes()]
    max_out_degree = max(out_degrees)
    colors = plt.cm.coolwarm([d/max_out_degree for d in out_degrees])

    # Adjusting alpha for visibility
    alpha_values = [0.7 + 0.3 * (d/max_out_degree) for d in out_degrees]

    # Node Sizes (based on in-degree)
    in_degrees = [G.in_degree(n) for n in G.nodes()]
    size_factor = 10  # adjust this value to fit your needs
    sizes = [d * size_factor for d in in_degrees]

    # Set the figure size
    plt.figure(figsize=(15, 10))

    # Draw Nodes and Edges
    nx.draw_networkx_nodes(G, pos, node_color=colors, node_size=sizes, alpha=alpha_values) 
    nx.draw_networkx_edges(G, pos, edge_color='gray', alpha=0.5)  # Set edge color to gray or any distinct color you prefer
    nx.draw_networkx_labels(G, pos)  # Optional: if you want labels on nodes

    plt.title("Top 200 influential users in Farcaster network")
    plt.show()
    ```

=== "Interactive" 
    ```py
    # Layout
    pos = nx.kamada_kawai_layout(G)

    # Node Colors (heatmap-style based on out-degree)
    out_degrees = [G.out_degree(n) for n in G.nodes()]
    max_out_degree = max(out_degrees)
    colorscale = [[0, 'blue'], [1, 'red']]
    node_colors = [d/max_out_degree for d in out_degrees]

    # Node Sizes (adjusted for better visibility)
    size_factor = 0.5
    sizes = [d * size_factor + 5 for d in in_degrees]  # Added a constant to ensure even nodes with 0 in-degrees are visible

    # Edge coordinates for plotting
    edge_x = []
    edge_y = []
    for edge in G.edges():
        x0, y0 = pos[edge[0]]
        x1, y1 = pos[edge[1]]
        edge_x.extend([x0, x1, None])
        edge_y.extend([y0, y1, None])

    # Node coordinates for plotting
    node_x = [pos[node][0] for node in G.nodes()]
    node_y = [pos[node][1] for node in G.nodes()]

    # Node Labels
    labels = list(G.nodes())

    # Create the plot using Plotly
    edge_trace = go.Scatter(x=edge_x, y=edge_y, mode='lines', line=dict(color='gray', width=0.5), opacity=0.7)
    node_trace = go.Scatter(x=node_x, y=node_y, mode='markers+text', marker=dict(size=sizes, color=node_colors, colorscale=colorscale, showscale=True, opacity=0.8), text=labels, textposition="top center", hoverinfo='text')

    fig = go.Figure(data=[edge_trace, node_trace])

    # Adjusting layout for better visualization
    fig.update_layout(showlegend=False, hovermode='closest', width=1000, height=1000)

    fig.show()
    ```

In our interactive plot, briang (large, blue) contrasts with n (smaller, red). It suggests briang attracts more interactions, whereas n is the initiator in recent activity.

## 🔍 Part 3: Graph Sampling
Graph sampling is essential for handling large networks. Random Node Sampling (RNS) and Random Walk Sampling (RWS) are two simple methods we will cover here.

_Again, below is a brief code snippet. For the comprehensive version, visit the [Github notebook](https://github.com/duneanalytics/python-notebook-examples/blob/main/social_network/Farcaster%20Network%20Analysis%20(Summary%20Stats%2C%20Centrality%20Measures%2C%20Sampling%2C%20%26%20Community%20Detection).ipynb)._

=== "Random Node Sampling" 
    ```py
    def random_node_sampling(graph, num_nodes, seed=None):
        if seed is not None:
            random.seed(seed)  # Set the random seed if provided
            
        sampled_nodes = random.sample(graph.nodes(), num_nodes)
        return graph.subgraph(sampled_nodes)
    ```

=== "Random Walk Sampling" 
    Note that we need to pick a node to start this random walk. 
    ```py
    def random_walk_sampling(graph, start_node, num_nodes, seed=None):
        if seed is not None:
            random.seed(seed)  # Set the random seed if provided

        sampled_nodes = set([start_node])
        current_node = start_node

        while len(sampled_nodes) < num_nodes:
            neighbors = list(graph.neighbors(current_node))
            
            # If there are no neighbors, backtrack to a previously visited node
            if not neighbors:
                previous_nodes = list(sampled_nodes)
                random.shuffle(previous_nodes)
                for previous_node in previous_nodes:
                    neighbors = list(graph.neighbors(previous_node))
                    if neighbors:
                        current_node = random.choice(neighbors)
                        break

            # If there are neighbors, choose a random one
            else:
                current_node = random.choice(neighbors)

            sampled_nodes.add(current_node)

        return graph.subgraph(sampled_nodes)

    ```


## 🏘️ Part 4: Community Detection

Community detection, akin to clustering in traditional data analysis, reveals hidden structures within our sampled graph. While you might lean towards classic algorithms like k-means, specialized methods like the Louvain, which focuses on modularity, offer tailored insights. But remember, there's no universal solution—your choice should resonate with your graph's nature and your objectives.

Here we illustrate how to use Louvain and Girvan-Newman methods to perform community detection on our sampled network (derived by doing random node sampling).

=== "Louvain"
    ```py
    def louvain_community(G, n=3, draw=True):
        partition = community_louvain.best_partition(G)
        pos = nx.spring_layout(G)
        draw_communities(G, partition, pos, draw)
        num_communities, average_size, sorted_communities = get_community_stats(partition)
        print(f"Number of detected communities: {num_communities}")
        print(f"Average community size: {average_size:.2f} nodes\n")
        print_top_communities(n, sorted_communities)
        return sorted_communities[:n] if n else sorted_communities
    ```
=== "Girvan-Newman"
    ```py
    def girvan_newman_community(G, n=3, draw=True):
        communities_generator = community.girvan_newman(G)
        top_level_communities = next(communities_generator)
        partition_gn = {node: cid + 1 for cid, community in enumerate(top_level_communities) for node in community}
        pos = nx.spring_layout(G)
        draw_communities(G, partition_gn, pos, draw)
        num_communities, average_size, sorted_communities = get_community_stats(partition_gn)
        print(f"Number of detected communities: {num_communities}")
        print(f"Average community size: {average_size:.2f} nodes\n")
        print(f"Top {n} Communities:")
        print_top_communities(n, sorted_communities)
        return sorted_communities[:n] if n else sorted_communities
    ```
=== "Example community detection"
    ```py
    result_louvain_random_node = louvain_community(random_node_sampling(G, 500, 11).to_undirected())
    ```

With these communities in hand, it's time to dig deeper.  Here we illustrate how to take the top 3 communities detected in above steps, use [Dune API and parameters to retrieve social posts of these communities](https://dune.com/queries/3128246), and perform a word frequency analysis. This will shed light on the unique conversational nuances of each group.

```py
# Create a figure and a grid of subplots
fig, axs = plt.subplots(3, 1, figsize=(20, 15))

for idx, result_list in enumerate(result_louvain_random_node): # replace the results here
    # Joining items and formatting string
    quoted_items = "', '".join(result_list)
    formatted_string = f"'{quoted_items}'"
    
    # Define the query
    query = QueryBase(
        name="Farcaster texts lookup by handles",
        query_id=3128246, # https://dune.com/queries/3128246
        params=[
            QueryParameter.text_type(name="farcaster_handles", value=formatted_string),
            QueryParameter.number_type(name="past_n_months", value=1),
        ],
    )
    query_result = dune.run_query_dataframe(query=query, performance="large")  # Specify large cluster for faster runtime
    
    est_credits = query_result.size/1_000 + 20 # 20 credits for large cluster
    print(f"⛽ Estimated credit consumption from this run is {est_credits:,.1f}")
    

    # Concatenating all text data from the 'text' column into a single string
    text_data = query_result['text'].str.cat(sep=' ')

    # Tokenization
    tokens = word_tokenize(text_data.lower())  # Converts to lowercase

    # Removing stopwords
    tokens = [word for word in tokens if word.isalpha() and word not in stopwords.words('english')]

    # Word frequency
    word_freq = Counter(tokens)

    # Get the most common words and their counts
    words, counts = zip(*word_freq.most_common(10))
    
    # Plotting on the corresponding subplot
    axs[idx].bar(words, counts)
    axs[idx].set_xlabel('Words')
    axs[idx].set_ylabel('Frequency')
    axs[idx].set_title(f'Word Frequency Analysis - List {idx + 1}')
    
    # Set the font size of the x-axis labels
    axs[idx].tick_params(axis='x', labelsize=15)  # Change 12 to the desired font size


# Adjust the spacing between the plots
plt.tight_layout()
plt.show()
```

But of course, with text analysis, you can venture into topic modeling or sentiment analysis. There's a universe of analytical adventures waiting!

## Conclusion
We've crafted a primer on conducting social network analysis using Farcaster with the Dune API and Python. Farcaster's decentralized data offers a unique perspective, especially when mainstream platforms like Facebook restrict access, and even Twitter is tightening its grip. Dive into summary statistics, centrality measures, graph sampling, and community detection using real-world data.

Explore how to interact with Dune's data via its API and seamlessly export for your analysis endeavors. If your curiosity beckons and you're keen to experiment, let this guide be your helper companion.

Let's get connected! Any questions or thoughts about this guide or ideas for future guide, let me know via [LinkedIn](https://www.linkedin.com/in/jackieyingzhuzhang/), [Twitter](https://twitter.com/agaperste) or [Warpcast](https://warpcast.com/agaperste-)!


