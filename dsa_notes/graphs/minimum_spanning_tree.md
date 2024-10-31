# Minimum Spanning Tree

## 1. Overview

- a subset or subgraph for a weighted and undirected graph
- the minimum spanning tree connects all vertices of a graph with the minimum possible total edge weight, without forming a cycle

## 2. Algorithms to Compute MST


| **Feature**                             | **Kruskal's Algorithm**          | **Prim's Algorithm**   |
| ----------------------------------------- | ---------------------------------- | ------------------------ |
| **Approach**                            | Edge-based                       | Vertex-based           |
| **Suitable for Sparse vs Dense Graphs** | Sparse Graphs                    | Dense Graphs           |
| **Complexity**                          | `O(E log E)`                     | `O(E log V)`           |
| **Data Structure Used**                 | Union-Find                       | Priority Queue         |
| **Starting Point**                      | Any Edge (based on sorted order) | Arbitrary Start Vertex |

## 3. Prim's Algorithm

- builds a Minimum Spanning Tree by starting at an arbitrary vertex and repeatedly selecting the cheapest edge that connects a vertex in the MST to a vertex outside the MST.
- it is a greedy algorithm

### Visualization

![prims algo animation](https://upload.wikimedia.org/wikipedia/commons/9/9b/PrimAlgDemo.gif)

### How It Works:

1. Initialize all vertices as unexplored
2. Start from any vertex and add it to the MST
3. Use a priority queue to find the smallest edge that connects an unexplored vertex to the MST
4. Repeat the process until all vertices are part of the MST

### Implementation

```cpp
vector<Edge> primMST(Graph& graph, int start) {
    priority_queue<Edge, vector<Edge>, Compare> minHeap;
    vector<bool> inMST(graph.V, false);
    vector<Edge> mst;

    inMST[start] = true;
    for (Edge& e : graph.adj[start]) minHeap.push(e);

    while (!minHeap.empty() && mst.size() < graph.V - 1) {
        Edge minEdge = minHeap.top();
        minHeap.pop();

        int v = minEdge.v;
        if (inMST[v]) continue;

        inMST[v] = true;
        mst.push_back(minEdge);

        for (Edge& e : graph.adj[v]) if (!inMST[e.v]) minHeap.push(e);
    }
    return mst;
}
```

---

## 4. Kruskal's Algorithm

- sorts all edges in the graph by weight and adds them one by one, ensuring no cycles are formed
- treats the graph as a collection of **disjoint-sets**
- each vertex starts as its own separate component
- merges these sets by adding the smallest edges between components

### Visualization

![kruskals algo animation](https://upload.wikimedia.org/wikipedia/commons/b/bb/KruskalDemo.gif)

### How It Works:

1. Sort all edges by weight
2. Use a union-find data structure to track connected components
3. Add the smallest edge that does not form a cycle
4. Repeat until all vertices are connected

### Implementation

```cpp
vector<Edge> kruskalMST(Graph& graph) {
    sort(graph.edges.begin(), graph.edges.end());  // Sort edges by weight
    UnionFind uf(graph.V);  // Union-Find for cycle detection
    vector<Edge> mst;

    for (Edge& edge : graph.edges) {
        if (uf.find(edge.u) != uf.find(edge.v)) {  // Check cycle
            uf.unionSets(edge.u, edge.v);  // Join the components
            mst.push_back(edge);
        }
    }
    return mst;
}
```
