# Graph Traversal

## 1. Overview

- There are two primary types of graph traversal:
  - **Depth-First Search (DFS)** : Explores each path as deep as possible before backtracking
  - **Breadth-First Search (BFS)** : Explores vertices level-by-level from the starting point

## 2. Depth-First Search

- recursively explores paths from a starting vertex as deep as possible before backtracking

![dfs animation](https://codepumpkin.com/wp-content/uploads/2017/04/dfs.gif)

### How it Works:

1. Start at a given vertex and mark it as visited
2. recursively visit all unvisited neighbours
3. backtrack when no unvisited neighbours remain

### Implementation

- utilises the call stack to recursively visit all unvisited neighbours
- initial call of the traversal function involves defining a starting node in the graph

```cpp
void DFS(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : adj[node]) {
        if (!visited[neighbor])
            DFS(neighbor, adj, visited);
    }
}
```

## 3. Breadth-First Search

- exploration of every neighbour of a given node before moving to the next "level"
- it uses a queue to keep track of nodes at each level

![bfs animation](https://codepumpkin.com/wp-content/uploads/2017/04/BFS.gif)

### How it Works:

1. Start at a given vertex and enqueue it
2. Process the front vertex in the queue and mark it as visited
3. Enqueue all unvisited neighbours of the current vertex
4. Repeat until the queue is empty

### Implementation

```cpp
void BFS(int start, vector<vector<int>>& adj, int V) {
    vector<bool> visited(V, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```
