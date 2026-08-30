# European Flight Network Analysis

Graph-based analysis of the European air transportation network using real-world OpenFlights data.

This project was developed as part of an academic course project focused on graph algorithms and network analysis.

## Overview

The project analyzes the structure of the European flight network in order to identify:

- Central airports
- Structural hubs and bridges
- Communities within the network
- Relationships between airport activity and structural importance
- Vulnerabilities in network connectivity
- Differences between random failures and targeted airport removals

The analysis focuses on the structural properties of the network rather than flight frequency, passenger volume, or real-time aviation data.

## Dataset

The project uses data from the **OpenFlights** dataset:

- Airports dataset: 7,698 records
- Routes dataset: 67,663 records
- Valid route records after cleaning: 67,240
- European route records after filtering: 15,224
- Active European airports included in the graph: 496

The active graph contains:

- **496 nodes**
- **4,903 edges**
- **2 connected components**
- **492 airports in the largest connected component**

Most of the analysis was performed on the largest connected component.

## Graph Model

The flight network was modeled as an **undirected weighted graph**:

- Each airport is represented as a node
- A route between two airports is represented as an edge
- Edge weight represents the number of route records between the two airports

The graph was treated as undirected because the analysis focused on overall connectivity rather than route direction.

## Analysis

### Centrality Measures

Several centrality measures were calculated in order to capture different types of structural importance:

- **Degree Centrality** – number of directly connected airports
- **Betweenness Centrality** – importance of an airport as a bridge on shortest paths
- **Closeness Centrality** – structural proximity to the rest of the network
- **PageRank** – importance based on the importance of connected airports

Using multiple measures made it possible to distinguish between airports that are highly connected, structurally central, or important as bridges between different parts of the network.

### Activity vs. Structural Centrality

Airport activity was estimated using weighted degree, representing the total number of route records associated with each airport.

The project compared this activity estimate with the different centrality measures using:

- Top-10 rankings
- Ranking overlap
- Spearman correlation

This analysis showed that high activity and structural centrality are strongly related, but they do not represent the same concept.

### Local Clustering

The **Local Clustering Coefficient** was calculated for each airport in order to examine how strongly its neighboring airports are connected to one another.

The analysis was used to distinguish between:

- Airports located in highly interconnected local regions
- Airports acting as bridges between less-connected areas

A custom exploratory definition of **bridge-hub candidates** was also used by combining:

- High Degree
- High Betweenness
- Low Local Clustering

### Community Detection

The **Louvain algorithm** was used to detect communities within the network.

The analysis examined:

- Number and size of detected communities
- Geographic and structural patterns
- Airports connecting different communities
- Relationship between inter-community connections and Betweenness Centrality

The algorithm identified **8 communities** in the largest connected component.

### Network Robustness

The project tested how the network reacts to gradual airport removal.

Four removal strategies were compared:

- Random removal
- Degree-based removal
- Betweenness-based removal
- PageRank-based removal

For each removal rate, the analysis measured:

- Remaining number of nodes
- Size of the largest connected component
- Relative size of the largest component
- Number of connected components

Random removal was repeated 30 times for each removal rate and averaged.

## Key Findings

- Different centrality measures identify different types of important airports.
- Airports with many direct connections are not always the most structurally critical.
- Airports with high Betweenness can act as important bridges even when their activity is not among the highest.
- Degree and weighted activity were strongly correlated.
- Community detection revealed a partially modular structure within the European flight network.
- The network was relatively resilient to random airport removal.
- Targeted removal of central airports caused significantly greater fragmentation.
- Betweenness-based removal caused especially strong damage at earlier removal stages.
- Degree-based removal caused severe fragmentation at higher removal rates.

## Technologies

- Python
- Pandas
- NetworkX
- Jupyter Notebook
- Graph Algorithms
- Network Analysis
- Data Analysis
- Louvain Community Detection
- PageRank

## Project Files

- `european_flight_network_analysis.ipynb` – Main analysis notebook
- Project report – Methodology, results, and conclusions
