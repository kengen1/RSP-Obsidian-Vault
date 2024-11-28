#Path-Finding #Shortest-Path #Weighted-Graphs [[Graphs]] #Dynamic-Programming 
## 1. Overview
- Finds the shortest path from a source node to all other nodes
- **Graph Type**: Weighted, directed or undirected graph (handles both positive and negative weights but no negative cycles)
- **Approach**: Dynamic Programming approach that iteratively relaxes edges up to `V-1` times (where `V` is the number of vertices)
- **Time Complexity**: `O(V * E)`, where `V` is the number of vertices and `E` is the number of edges.

![bellman ford](https://i.sstatic.net/WalA2.gif)

## 2. Algorithm Steps
1. Initialization
- Set the distance to the source node as 0 and all other nodes as `infinity`

2. Edge Relaxation (repeated `V-1` times):
    - For each edge `(u, v)` with weight `w`:
        - If the distance to `u` is known and `distance[u] + w < distance[v]`, update `distance[v]` to `distance[u] + w`.
    - Repeat this process `V-1` times to ensure that the shortest paths are calculated

3. Negative Cycle Check:
- Perform a final pass through all edges to check for **negative weight cycles**
- If any edge can still be relaxed, then the graph contains a **negative weight cycle**, and no valid shortest path exists

## 3. Implementation
```cpp
#include <iostream>
#include <vector>
#include <limits>

using namespace std;

struct Edge {
    int src, dest, weight;
};

vector<int> bellmanFord(int V, int E, vector<Edge>& edges, int src) {
    vector<int> dist(V, numeric_limits<int>::max());
    dist[src] = 0;

    // Relax edges V-1 times
    for (int i = 1; i <= V - 1; i++) {
        for (const Edge& edge : edges) {
            if (dist[edge.src] != numeric_limits<int>::max() && 
                dist[edge.src] + edge.weight < dist[edge.dest]) {
                dist[edge.dest] = dist[edge.src] + edge.weight;
            }
        }
    }

    // Check for negative weight cycles
    for (const Edge& edge : edges) {
        if (dist[edge.src] != numeric_limits<int>::max() && 
            dist[edge.src] + edge.weight < dist[edge.dest]) {
            cout << "Graph contains a negative weight cycle" << endl;
            return {};  // Return an empty result if a negative cycle is found
        }
    }

    return dist;
}
```