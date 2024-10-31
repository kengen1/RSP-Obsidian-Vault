# Dijkstra's Shortest Path Algorithm

## 1. Overview

- Finds the shortest path from a source node to all other nodes in a graph with non-negative weights
- **Graph Type**: Weighted, directed or undirected graph with non-negative weights
- **Data Structure**: Uses a **priority queue** (min-heap) to store nodes based on their current shortest distance from the source
- **Approach**: Greedy algorithm that explores the shortest paths first
- **Time Complexity**: O((V + E) log V)
  - since the extraction of the minimum element from the heap is of O(log V)


![dijkstras shortest path animation](https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif)


## 2. Algorithm Steps
1. Initialize:
- Set the distance to the source node as 0 and all other nodes as `infinity`
- Use a priority queue (min-heap) to keep track of nodes with the minimum distance

2. Process the Current Node:
- Extract the node with the smallest distance from the priority queue
- For each of its adjacent nodes
    - Calculate the distance from the source node to this adjacent node
    - If this calculated distance is smaller than the known distance, update the distance and add the node to the priority queue

3. Repeat until the priority queue is empty
4. Output the shortest distance from the source node to each other node

## 3. Implementation
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <limits>

using namespace std;

vector<int> dijkstra(int V, vector<vector<pair<int, int>>> &adj, int src) {
    vector<int> dist(V, numeric_limits<int>::max()); // Initialize distances as infinite
    dist[src] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, src}); // {distance, vertex}

    while (!pq.empty()) {
        int u = pq.top().second;
        int uDist = pq.top().first;
        pq.pop();

        if (uDist > dist[u]) continue; // Skip if distance is outdated

        for (auto &neighbor : adj[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}
```