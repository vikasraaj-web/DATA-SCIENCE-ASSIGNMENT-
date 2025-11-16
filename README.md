# Modularity on the Karate Club Graph

[cite_start]A project for **DSC212: Graph Theory Module**. [cite: 2]

## 📜 Abstract

[cite_start]This project implements a **spectral modularity maximization method** from scratch. [cite: 8] [cite_start]It applies this algorithm to the classic **Zachary's Karate Club network**, a famous real-world social network of 34 members (nodes) and 78 friendships (edges). [cite: 12, 15, 25]

[cite_start]The goal is to use the graph's structure *before* a real-life conflict split the club to see if our algorithm can computationally **discover the social "fault lines"** [cite: 24] [cite_start]and correctly predict the two factions that emerged (one led by the instructor, "Mr. Hi," and one by the club administrator). [cite: 19, 23, 27]

## 🔬 The Method: Recursive Spectral Bipartition

We are trying to find the optimal division of the network into communities. [cite_start]Modularity, $Q$, is a quality score that measures how "surprising" a division is compared to a random null model[cite: 35, 36, 41].

### The Modularity Matrix

[cite_start]The core of this method is the **modularity matrix**, $B$[cite: 57]:

$$B = A - \frac{kk^T}{2m}$$

* [cite_start]$A$ is the **adjacency matrix** (the actual connections)[cite: 60].
* [cite_start]$\frac{kk^T}{2m}$ is the **expected number of edges** between nodes in a random graph with the same node degrees[cite: 61, 76, 79].

[cite_start]The modularity score $Q$ for any given two-way split (encoded in a vector $s \in \{-1, +1\}^n$) is[cite: 55, 85]:

$$Q = \frac{1}{4m}s^TBs$$

[cite_start]Our goal is to **find the vector $s$ that maximizes $Q$**[cite: 90].

### Spectral Solution

[cite_start]Since checking all $2^n$ possible splits is computationally impossible, we "relax" the problem by allowing $s$ to contain real numbers instead of just $\pm1$[cite: 102, 103, 104].

[cite_start]A classic result in linear algebra (the Rayleigh-Ritz theorem) states that the vector $s$ that maximizes $s^TBs$ (under a unit-length constraint) is the **leading eigenvector $u_1$** of the modularity matrix $B$[cite: 108, 258, 259, 281].

[cite_start]We then get our "hard" split by a simple thresholding[cite: 114, 115]:

* [cite_start]If a node's entry in $u_1$ is **positive**, assign it to **Group 1**[cite: 115].
* [cite_start]If a node's entry in $u_1$ is **negative or zero**, assign it to **Group 2**[cite: 115].

### Recursive Bisection

[cite_start]To find *more than two* communities, we apply this method recursively[cite: 119, 153]:

1.  [cite_start]Start with the full set of nodes[cite: 155].
2.  [cite_start]For each new community $C$, create its **restricted modularity matrix $B^{(C)}$**[cite: 123, 125, 156].
3.  [cite_start]Compute the **leading eigenpair $(\lambda_1^{(C)}, u_1^{(C)})$** of $B^{(C)}$[cite: 127, 157].
4.  [cite_start]**If $\lambda_1^{(C)} > 0$:** This means a split *improves* modularity, so we **split this community** further (based on the sign of $u_1^{(C)}$) and recurse[cite: 128, 159, 160].
5.  [cite_start]**If $\lambda_1^{(C)} \le 0$:** This means no further split can improve modularity, so the community is considered **"indivisible,"** and the recursion stops for this branch[cite: 130, 136, 158, 288].

---

## 📊 Project Tasks

This notebook implements the following tasks as required:

1.  [cite_start]**Implement** the recursive spectral modularity algorithm from scratch[cite: 196].
2.  [cite_start]**Visualize** the Karate Club graph after each split, coloring nodes by their new community assignments[cite: 197].
3.  [cite_start]**Compute** four key node metrics after each iteration using `networkx`[cite: 198]:
    * [cite_start]Degree Centrality [cite: 199]
    * [cite_start]Betweenness Centrality [cite: 200]
    * [cite_start]Closeness Centrality [cite: 201]
    * [cite_start]Clustering Coefficient [cite: 202]
4.  [cite_start]**Plot** the **evolution** of these metrics for all 34 nodes across the algorithm's iterations[cite: 203].
5.  [cite_start]**Discuss** the results, noting which nodes consistently remain central and how community structure influences these metrics[cite: 204].

---

## 🚀 How to Run

1.  Clone this repository.
2.  Open the `.ipynb` notebook file in a compatible environment (like Google Colab, VS Code, or Jupyter Lab).
3.  Run the cells from top to bottom. The notebook is designed to run sequentially without any manual edits.

---

## 📚 Libraries Used

* **networkx** (for graph operations and metrics)
* **numpy** (for matrix algebra)
* **matplotlib & seaborn** (for visualizations)
* **pandas** (for organizing metrics data)
* **scipy** (for efficient eigenvalue computation)

---

## 📄 Attribution

[cite_start]The modularity objective, modularity matrix $B$, and spectral bipartition method are based on the foundational work of M. E. J. Newman[cite: 148, 149]:

> [cite_start]Newman (2006), "Modularity and community structure in networks," PNAS 103(23):8577-8582. [cite: 149, 150]
