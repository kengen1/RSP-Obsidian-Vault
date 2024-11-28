#ADM #Traversal [[Graphs]]
## Types of Graphs

- **Undirected Graphs** : Edges have no direction
- **Directed Graphs** : Each edge points from one vertex to another
- **Weighted Graphs** : Edges have associated weights or costs
- **Bipartite Graphs** : Graphs that can be coloured with two colours without conflicts
- **Cyclic Graphs** : Contains at least one cycle (a path that starts and ends at the same vertex)
- **Acyclic Graphs** :  Has no cycles. Acyclic Graphs (DAGs) are used in topological sorting
- **Connected Graphs** : Every vertex is reachable from any other vertex
- **Disconnected Graphs** : Multiple components that are not connected

## Graph Data Structures

1. Adjacency List:

   - Stores neighbours for each vertex in a list
   - Space-efficient for sparse graphs
2. Adjacency Matrix

   - A 2D matrix indicating the presence or absence of edges
   - Suitable for dense graphs but consumes more space


## Key Graph Traversal Algorithms


| Feature          | Breadth-First Search          | Depth-First Search           |
| ------------------ | ------------------------------- | ------------------------------ |
| Data Structure   | Queue (FIFO)                  | Stack (LIFO) / Recursion     |
| Path Exploration | Explores all neighbours first | Explores a path to its depth |
| Use Case         | Shortest Path, Level-Order    | Topological sorting, cycles  |

### 1. Breadth First Search (BFS)

- Explores all neighbours of a vertex before moving deeper
- Use Case : Finding the shortest path in unweighted graphs
- Data Structure : Queue (FIFO) to store vertices to explore
- Time Complexity : O(V + E) where V is the number of vertices and E is the number of edges

Steps:

1. mark the starting vertex as discovered and enqueue it
2. while the queue is not empty:
   - dequeue a vertex and process it
   - enqueue all undiscovered neighbours

### 2. Depth-First Search (DFS)

- Explores a path as far as possible before backtracking
- Use Case : Suitable for topological sorting and finding connected components
- Data Structure : Either an explicitly Stack (LIFO) recursive implementation using the call stack
- Time Complexity : O(V + E)

Steps:

1. start from the initial vertex and mark it as discovered
2. recursively visit undiscovered neighbours
3. mark the vertex as processed after all its neighbours are explored


## Applications of Traversal
- Connected Components : identify separate clusters in graphs
- Cycle Detection : identify cycles using back edges in DFS
- Topological Sorting : order vertices of a directed acyclic graph (DAG)
- Path Finding : BFS ensures the shortest path in **unweighted graphs**


## Take-Home Lessons
- Choosing the right algorithm
    - Use BFS for shortest paths or level-order processing
    - Use DFS for more exploratory tasks such as finding components or cycles
- Memory Considerations
    - Adjacency lists are generally better for large sparse graphs
- Graph Representation Matters
    - Dense graphs benefit from adjacency matrices, but lists are more flexible for most cases
