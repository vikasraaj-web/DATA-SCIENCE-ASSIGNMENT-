# Modularity on the Karate Club Graph

A project for **DSC212: Graph Theory Module**.

## 📜 Abstract

This project implements a **spectral modularity maximization method** from scratch. It applies this algorithm to the classic **Zachary's Karate Club network**, a famous real-world social network of 34 members (nodes) and 78 friendships (edges).

The goal is to use the graph's structure *before* a real-life conflict split the club to see if our algorithm can computationally **discover the social "fault lines"** and correctly predict the two factions that emerged (one led by the instructor, "Mr. Hi," and one by the club administrator).

## 🔬 The Method: Recursive Spectral Bipartition

We are trying to find the optimal division of the network into communities. Modularity, $Q$, is a quality score that measures how "surprising" a division is compared to a random null model.

### The Modularity Matrix

The core of this method is the **modularity matrix**, $B$:

$$B = A - \frac{kk^T}{2m}$$

* $A$ is the **adjacency matrix** (the actual connections).
* $\frac{kk^T}{2m}$ is the **expected number of edges** between nodes in a random graph with the same node degrees.

The modularity score $Q$ for any given two-way split (encoded in a vector $s \in \{-1, +1\}^n
