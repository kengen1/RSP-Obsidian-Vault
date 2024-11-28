
![Graph Data Structure](https://www.tutorialspoint.com/data_structures_algorithms/images/undirected_graph.jpg)

## 1. Overview

- a non-linear data structure consisting of **nodes** (also called **vertices**) connected by edges
- used to represent relationships between entities
- common applications include social networks, maps, recommendation systems

*Key Components*:

- **Vertices (V)** : The individual nodes or points in the graph
- **Edges (E)** : Connections between pairs of vertices
- **Degrees** : The number of edges connected to a vertex

*Types of Graphs*:

- Undirected Graph
- Directed Graph
- Weighted Graph
- Unweighted Graph

## 2. Structure

![adjacency list graph implementation](https://media.geeksforgeeks.org/wp-content/uploads/20200630125356/adjacency_list.jpg)

- an **adjacency list** represents a graph as an array of lists
- each index in the array corresponds to a vertex
- the list at that index stores the neighbours of the #Arrays 
- an adjacency list implementation of a graph has a *space complexity* of O(V + E) where V is the number of vertices and E is the number of edges
  - this implementation is efficient for sprase graphs (fewer edges relative to vertices)

### Undirected / Unweighted Graph
```cpp
class Graph {
private:
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list

public:
    // Constructor
    Graph(int vertices) {
        V = vertices;
        adj.resize(V); // Initialize the adjacency list
    }
};
```

### Directed Graph
- A directed graph (or digraph) has edges with direction.
- If there is an edge from u to v, you can travel only from u to v, but not vice versa unless there is another edge from v to u.

```cpp
void addEdge(int u, int v) {
    adj[u].push_back(v); // Add directed edge from u to v
}
```

### Weighted Graph
```cpp
#include <vector>
using namespace std;

vector<vector<pair<int, int>>> adj; // Store (neighbor, weight) pairs

void addWeightedEdge(int u, int v, int weight) {
    adj[u].push_back({v, weight});
    adj[v].push_back({u, weight}); // For undirected weighted graph
}
```

## 3. Operations 
- for simplicity sake, these operations are for unweighted / undirected graphs

| **Operation** | **Description**                                  | **Time Complexity**    | **Space Complexity** |
|---------------|---------------------------------------------------|------------------------|----------------------|
| Add Vertex    | Adds a new vertex to the graph.                   | O(1)                   | O(V)                 |
| Add Edge      | Adds an edge between two vertices.                | O(1)                   | O(1)                 |
| Remove Edge   | Removes an edge between two vertices.             | O(deg(V))              | O(1)                 |
| Print Graph   | Prints the adjacency list.                        | O(V + E)               | O(1)                 |
| Check Edge    | Checks if an edge exists between two vertices.    | O(deg(V))              | O(1)                 |

### Add Vertex
- adds a vertex to the graph by expanding the adjacency list

```cpp
void addVertex() {
    adj.push_back(vector<int>()); // Add an empty list for the new vertex
    V++;
}
```

### Add Edge
- adds an edge between two vertices (in the case of an undirected graph)
- where U is the source vertex and V is the destination vertex

```cpp
void addEdge(int u, int v) {
    adj[u].push_back(v); // Add v to u's list
    adj[v].push_back(u); // Add u to v's list
}
```

### Remove Edge
- removes an edge between two vertices by searching for it in both adjacency lists

```cpp
void removeEdge(int u, int v) {
    adj[u].erase(remove(adj[u].begin(), adj[u].end(), v), adj[u].end());
    adj[v].erase(remove(adj[v].begin(), adj[v].end(), u), adj[v].end()); 
}
```


### Print Graph
```cpp
void printGraph() {
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": ";
        for (int neighbor : adj[i])
            cout << neighbor << " ";
        cout << endl;
    }
}
```

### Check Edge
```cpp
bool hasEdge(int u, int v) {
    return find(adj[u].begin(), adj[u].end(), v) != adj[u].end();
}
```

## 4. Example Usage
```cpp
int main() {
    Graph g(5); // Create a graph with 5 vertices

    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(1, 4);
    g.addEdge(3, 4);

    cout << "Graph representation (Adjacency List):" << endl;
    g.printGraph();

    cout << "Does edge (1, 3) exist? " << (g.hasEdge(1, 3) ? "Yes" : "No") << endl;

    g.removeEdge(1, 3);
    cout << "After removing edge (1, 3):" << endl;
    g.printGraph();

    return 0;
}
```