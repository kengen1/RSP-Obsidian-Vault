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

### 3. Union-Set Data Structure


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


## Network Flows and Bipartite Matching