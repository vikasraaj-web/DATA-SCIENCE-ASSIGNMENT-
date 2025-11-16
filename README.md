# DSC212: Graph Theory - Modularity on the Karate Club Graph

This repository contains the solution for the Research Assignment on "Modularity on the Karate Club Graph" as part of the DSC212 course.

## Project Overview

The goal of this project is to implement a recursive spectral modularity partitioning algorithm to detect communities in the famous Zachary's Karate Club graph. The solution is contained within a single Jupyter Notebook (`.ipynb`) that runs from top-to-bottom.

### Tasks Completed
The notebook successfully implements all the required tasks:
-   **Recursive Spectral Partitioning:** Implements the algorithm to recursively split the graph based on the leading eigenvector of the modularity matrix ($B$).
-   **Community Visualization:** Generates plots of the graph after each split, coloring nodes by their current community.
-   **Node Metrics:** Computes four key node metrics (Degree Centrality, Betweenness Centrality, Closeness Centrality, and Clustering Coefficient) at each iteration.
-   **Metric Evolution:** Plots the evolution of these metrics for each node across all iterations.
-   **Discussion:** Includes a short discussion analyzing which nodes remain central and how community structure influences the metrics.

## How to Run

This notebook is designed to run from top-to-bottom without any manual edits.

### 1. Requirements
You will need the following Python libraries. You can install them using `pip`:
```bash
pip install networkx numpy matplotlib jupyter
