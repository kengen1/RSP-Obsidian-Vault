# Chapter 6 : Weighted Graph Algorithms

## Minimum Spanning Trees (MSTs)
- a Minimum Spanning Tree is a subgraph that connects all vertices of a graph with the minimum possible total edge weight, without forming cyclces
- MSTs are essential in applications where minimizing costs is crucial, such as:
    - designing networks
    - road systems
    - electrical circuits

---
### 1. Prim's Algorithm
- builds a Minimum Spanning Tree by growing a connected tree one vertex at a time
- starts from a single vetex
- it is a *greedy* algorithm
- it selects the smallest edge that adds a new vertex to the tree, ensuring no cycles are formed

**Steps**:
1. Initialize all vertices as unexplored
2. Start from any vertex and add it to the MST
3. Use a priority queue to find the smallest edge that connects an unexplored vertex to the MST
4. Repeat the process until all vertices are part of the MST

**Time Complexity**:
- O(n²) for simple implementation
- O(m + n log n) using a priority queue

**Use Case** :  Best suited for dense graphs, such as designing utility networks
- since we are processing edges incrementally (one vertex at a time)
- implementation of priority queue to keep track of the smallest available edge

---

### 2. Kruskal's Algorithm
- builds a Minimum Spanning Tree by treating the graph as a collection of **disjoint sets** (each vertex starts as its own component)
- merges these sets by adding the smallest edges between components, ensuring no cycles are created
- is also a *greedy* algorithm
- leverages the **union-find** data structure to efficiently track connected components

**Steps**:
1. Sort all edges by weight
2. Use a union-find data structure to track connected components
3. Add the smallest edge that does not form a cycle
4. Repeat until all vertices are connected 

**Time Complexity**:
- O(m log m) where m is the number of edges

**Use Case** : Effective for sparse graphs, such as road networks
- since we are processing edges globally

---

### 3. Union-Find Data Structure
- The **Union-Find** (or **Disjoint Set**) data structure efficiently manages a collection of disjoint sets, supporting operations that are crucial for algorithms like **Kruskal's MST**.

**Set Representation**: Each "set" in a Union-Find represents a **subgraph** of connected vertices (a connected component)

**Operations**:
- **Union Operation**: Merges two sets containing different elements, effectively "unionizing" them into a single set. 
    - We are merging specifically vertices from the two sets when an edge joins them 
- **Find Operation**: Identifies which set a particular element belongs to, often used to check if two elements are in the same set.

**Key Concepts**:
- **Path Compression**: Optimizes the `Find` operation by making elements point directly to the root of their set, flattening the structure to speed up future searches.
- **Union by Rank/Size**: Ensures that smaller trees are attached under larger trees during a `Union` to keep the structure balanced.

**Time Complexity**:
- With **path compression** and **union by rank**, the amortized time complexity for each operation is nearly constant, O(α(n)), where α is the inverse Ackermann function, which grows extremely slowly.

**Use Case**: Essential for **cycle detection** and efficient management of connected components in algorithms like **Kruskal’s MST**.

---

## Shortest Path Algorithms
- finds the minimum path or distance between nodes in a graph 
- usually done by using **edge-weights** representing costs, distances, or times
- commonly used in:
    - navigation systems
    - network routing protocols
    - scheduling and resource allocation

---

### 1. Dijkstra's Algorithm
- finds the shortest path from a **source vertex to all other vertices** by always exploring the shortest known path first
- uses a priority queue to efficiently manage nodes for exploration

**Steps**:
1. Initialise the distances from the source to all vertices as infinity
    - Set the source node's distance to 0
    - Infinity (or a very large integer) is used to represent the initial distance to all nodes except the source, indicating that the nodes are **unreachable** at the start
2. Add the source node to the priority queue
3. Extract the vertex with the smallest distance, and update its neighbours if a shorter path is found
4. Repeat until all vertices are processed

**Time Complexity**:
- O(n²) for simple implementation
- O(m + n log n) using a Fibonacci heap

**Use Case** : Works well with **non-negative edge weights**

---

### 2. Bellman-Ford Algorithm
- iteratively **relaxes all edges** to find the shortest paths from a single source vertex
- suitable for graphs with negative edge weights

**What is "Relaxing" an edge?** : means trying to improve the known shortest path to a vertex by checking if a shorter path can be found through another vertex

**What are negative weight cycles?** : a loop in a graph where the sum of the edge weights is negative
- if you keep going around in this cycle, the total distance will decrease indefinitely, making it impossible to find the shortest path

**What is a "Relaxation Iteration**? : A relaxation iteration refers to going over all edges in the graph once to update distances to each vertex if a shorter path is found.
- The Bellman-Ford algorithm repeats this process multiple times to find the shortest paths.

**Steps**:
1. Initialise distances of all vertices as infinity, except for the source vertex, which is set to 0
2. Repeat (n-1) times, updating distances for every edge if a shorter path is found
3. Check for negative weight cycles by performing one more relaxation iteration

**Time Complexity**: O(m * n)

**Use Case**: Useful for graphs where negative edge weights might be present

---

### 3. Floyd-Warshall Algorithm
- computes the shortest paths between all pairs of vertices using dynamic programming
- iteratively improves the shortest paths by considering all possible intermediate vertices
    - what is an intermediate vertex?

**Steps**:
1. Create a matrix to store the shortest distances between all pairs of vertices
2. For each vertex, update the distance between all pairs using the vertex as an intermediate 
3. Repeat until no further updates can be made

**Time Complexity** : O(n²)

**Use Case** : Best suited for dense graphs and problems that require all-pair shortest paths, such as routing networks

---

## Network Flows and Bipartite Matching

### 1. Network Flows
- Network flow algorithms focus on **optimizing flow from a source node to a sink node** (subject to capacity constraints on edges)
- **Flow**: Imagine that you’re sending something, like water, goods, or data, through a network. The amount of "flow" is how much of this stuff you’re sending from one point to another.
- **Source and Sink Nodes**: The source node is where the flow starts (like a factory for goods), and the sink node is where it ends (like a warehouse).
- **Capacity Constraints**: Each connection (or edge) in the graph can only carry a limited amount of flow. Think of this like the width of a pipe—it can only carry a certain amount of water at a time. In the same way, each edge has a capacity that limits how much flow can pass through it.
- **Optimization**: The goal of network flow algorithms is to figure out the maximum flow from the source to the sink that respects these capacity limits on the edges.

**Algorithms**:
- *Ford-Fulkerson Algorithm:* Increases flow iteratively by finding augmenting paths (paths from source to sink with available capcity on each edge) in the **residual graph** (a graph that shows remaining capacity of each edge after current flow).
- *Edmonds-Karp Algorithm:* An implementation of Ford-Fulkerson using BFS, with a time complexity of O(m² n).

**Steps**:
1. initialize the flow to 0
2. find an augmenting path from the source to the sink using BFS
3. update flow along the path and adjust capacities in the residual graph
4. repeat until no more augmenting paths exist

**Use Case**: Used in logistics to optimize goods transportation and telecommunications to maximize data flow.