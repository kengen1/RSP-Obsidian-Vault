## Linked Lists
#### What Kind of Data Structure Is a Linked List?
```
a linked list is a linked data structure where elements are connected by pointers
```

#### What Kind of Linked Lists Are There?
```
- singly linked list
- doubly linked list (pointers to both the previous and next node in the list)
- circular linked list (the tail points back to the head of the list)
```

#### What Is the General Structure of a Linked List?
```cpp
// we need a structure that can store data and a pointer to the next node in the list
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};
```

#### What Operations Would You Have for This Structure?
```
- insertAtBeginning
- insertAtEnd
- insertAtPosition
- deleteFromBeginning
- deleteFromEnd
- deleteFromPosition
```

#### How Would You Implement These Operations?
```cpp
void insertAtBeginning(Node*& head, int val) {
    // create a new node with our value as its data
    // make our new node's next pointer equal head
    // make head equal our new node
}
```

```cpp
void insertAtEnd(Node*& head, int val) {
    // create a new node with our value as its data
    
    // check if head is null
        // if it is, make head equal to our new node and return
    
    // create an iterator node equal to head
    // while loop using iterator node to iterate through list
    // once the iterator reaches nullptr we know we are at the end of the list
    // make the iterator's next node equal to our new node
}
```

```cpp 
insertAtPosition(Node*& head, int pos, int val){
    //create a new node with our value as its data
    
    // check if head is null
        // if it is, make head equal to our new node and return 

    // create an iteartor node equal to head
    // for loop thorugh the list until we reach pos or our iterator is nullptr
    
    // we have now reached pos
    // check if its out of bounds before inserting

    // newNode->next = iterator->next;
    // iterator->next = newNode;
}
```

```
the deletion of nodes in their respective operations are similar in approach to their insertion counterparts where the primary difference is the use of the delete call to deallocate memory for the nodes.
```

#### What Is the Time Complexity of These Operations?
```
- insertAtBeginning - Time Complexity: O(1), Space Complexity: O(1)
- insertAtEnd - Time Complexity: O(n), Space Complexity: O(1)
- insertAtPosition - Time Complexity: O(n), Space Complexity: O(1)
- deleteFromBeginning - Time Complexity: O(1), Space Complexity: O(1)
- deleteFromEnd - Time Complexity: O(n), Space Complexity: O(1)
- deleteFromPosition - Time Complexity: O(n), Space Complexity: O(1)
```


## Binary Trees
#### What Kind of Data Structure Is a Binary Tree?
```
it is a linked structure where elements are connected by pointers
```

#### What Kind of Binary Trees Are There?
```
- Binary Search Tree - enforces the rule that items < root go into the left subtree and items > go into right subtree
- Balanced Binary Search Trees - enforces additional rules to ensure that insertion and deletion of nodes does not exceed O(log n) TC
- Heap (min and max) - a complete binary tree that maintains a specific order of elements, commonly used to implement a priority queue
```

#### What Is the General Structure of a Binary Tree?
```cpp
// we need a structure that can store the data for a given node, and pointers to its left and right children
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : data(val), left(nullptr), right(nullptr) {}
};
```

#### What Are the Different Traversal Types for a Binary Tree?
```
DFS:
    in-order: left->root->right
    pre-order: root->left->right
    post-order: left->right->root
BFS:
    level-order: top-to-bottom, left-to-right
```

#### What Are the Common Operations for a BST?
```
- insert
- delete
- search
- traverse

less important:
- find min/max
- find Predecessor (next largest node)
- find Successor (next smallest node)
```

#### How Would you Implement These Operations?
```cpp
TreeNode* insertTreeNode(TreeNode* root, int val) {

}
```

```cpp
TreeNode* deleteTreeNode(TreeNode* root, int val) {

}
```

```cpp
TreeNode* search(TreeNode* root, int val) {

}
```

```cpp
TreeNode* inorderTraversal(TreeNode* root) {

}
```

#### What Is the Time Complexity of These Operations?
```
- insert : O(log n) in a balanced tree, O(n) in an unbalanced tree
- delete : O(log n) in a balanced tree, O(n) in an unbalanced tree
- search : O(log n) in a balanced tree, O(n) in an unbalanced tree
- traverse : O(n)
```

## Graphs
#### What Kind of Data Structure Is a Graph?
```
a graph is a non-linear data structure (not arranged sequentially)
they can be either linked of contiguous structures depending on their implementation
```

#### How Would You Represent a Graph?
```
i would use a contiguous data strucutre, like a vector of vectors to represent an adjacency list
the adjacency list would contain all vertices and each vertex would have its own list of neighbours
```

#### What Is the General Structure of Your Above Representation?
```cpp
class Graph() {
    int V; // the number of vertices in the graph
    vector<vector<int>> adjList;
    public:
        Graph(int vertices){
            V = vertices;
            adjList.resize(V);
        }
}
```

#### What Are the Common Operations of a Graph?
```
addVertex
addEdge
removeEdge
printGraph
```

#### How Would You Implement These Operations?
```cpp
void addVertex() {
    adj.push_back(vector<int>()); // Add an empty list for the new vertex
    V++;
}
```

```cpp
void addEdge(int u, int v) {
    adjList[u].push_back(v);
    adjList[v].push_back(u);
}
```

```cpp
void removeEdge(int u, int v) {
    adj[u].erase(remove(adj[u].begin(), adj[u].end(), v), adj[u].end());
    adj[v].erase(remove(adj[v].begin(), adj[v].end(), u), adj[v].end()); 
}
```

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

#### What Is the Time Complexity of These Operations?
```
- addVertex: O(1)
- addEdge: O(1)
- removeEdge: O(deg(V))
- printGraph: O(n)
```

#### What Are the Main Types of Traversal Through a Graph?
```
BFS - look at all neighbours for a given vertex before looking at its children
DFS - recursively search the children of a vertex until none remain, then backtrack up the callstack and do the same for its neighbours
```

## Tries
#### What Is a Trie?
```
a trie (or prefix tree), is an n-ary tree where each node has up to 26 children, each being a character in the alphabet
each node in the tree represnts a character in a string
```

#### What Common Applications Are There for Tries?
```
- autocomplete
```

#### What Is Its General Structure?
```cpp
struct TrieNode {
    TrieNode* children[26];  // Assuming only lowercase English letters (a-z)
    bool isEndOfWord;        // Marks the end of a word

    TrieNode() {
        isEndOfWord = false;
        for(int i = 0; i < 26; i++) {
            children[i] = nullptr;
        }
    }
}
```

#### What Is the Time Complexity of Search Functions Such as ContainsWord or ContainsPrefix?
```
ContainsWord (search): O(m)
ContainsPrefix (startsWith): O(m)
```

## Vector Amortized Time
#### What Kind of Data Structure Is a Vector?
```
a vector is a contiguous data structure
it is a dynamically sized array
```

#### How Does a Vector Dynamically Increase in Size?
```
once a vector has reached its current capacity
a new vector is created with double its current size
the contents from the old vector are copied over to the new vector
this happens at the point of insertion of a new element so the new element is also copied over
the old vector is deleted and removed from memory 
```

#### What Is the Amortized Time Complexity of the Resizing of a Vector?
```
amortized time is the averaged-out time complexity over a sequence of operations
it takes into account occasional expensive operations which are offset by many cheap ones
the amortized time of insertions for vectors is constant O(1) since the ocassional resizing of the vector is not significant
resizing occurs more frequently at lower sizes of the array but as it growths, resizing becomes less frequent
```

## Bit Manipulation
#### Describe How the AND Operation Works?
```
sets a bit to 1 if both bits are 1
```

#### Describe How the OR Operation Works?
```
sets a bit to 1 if at least 1 bit is 1
```

#### Describe How the XOR Operation Works?
```
sets a bit to 1 if only 1 bit is set to 1
```

#### Describe How the NOT Operation Works?
```
inverts all bits
```

#### Describe How Left Shifting Bits Works?
```
shifts bits left, filling with 0 on the right
```

#### Describe How Right Shifting Bits Works?
```
shifts bits right, removing the right-most bit with each shift
```


## System Design
#### What Is a Singleton Design Pattern?
```
there can only be a single instance of a class that exists at a given time
this instance is globally shared 
```

#### Why Would We Need to Implement a Singleton Design Pattern?
```
the instantiation of a class only needs to be done a single time
access to a single instance of a class needs to be shared across the application
```

#### Why is the Singleton Design Pattern Considered an Anti-Design-Pattern?
```
it can lead to hidden dependencies between classes where changes to the global instance can have unexpected consequences
unit testing becomes more difficult if the singleton pattern is meant to carry state across tests
```

#### What Is a Factory Design Pattern?
```
a base class that creates sub-classes that inherit from the base class
the chosen subclass being instantiated is chosen at runtime by passing in a defining parameter
```

#### Why Would We Need to Implement a Factory Design Pattern?
```
we have a series of classes that share common functionality and we want to choose which to use at runtime
```

## Union Find (Disjoint Set)
#### What Is a Union Find Data Structure / What Is Its Purpose?
```
it is a datastructure that aims to merge two disjoint sets together
```

#### What Is the Structure of Union Find?
```
the union find class will contain 2 parameters
- a rank vector which tracks the depth of each element in the set
- a parent vector which tracks the parent node of each element in the set
```

#### What Are the Common Operations for Union Find?
```
union - merges two sets together by linking the root of one to the root of another
- we attach the root of the tree with the smaller rank to the root of the tree with the higher rank
find - finds the root of an element's set
```

#### How Does Path Compression Work?
```
path compression involves flattening the tree representing a set, by having all nodes in the set point directly to the root
this makes future lookups more efficient
```

#### How Does Ranking Work?
```
each node starts with a rank of 0
ranking is done when the union opration is conducted 
during the union operation we find the root of both sets and calculate the depth of each node during that process
```

#### Why Doesn't Path Compression Inhibit Ranking?
```
the rank of a node is based on its depth before path compression

path compression is not changing the relative order of nodes
it only changes the parent pointers
after path compression, nodes still respect the same rank structure
```

#### What Is the Amortized Time Complexity of These Operations?
```
the amortized time compelxity of both the union and find operations is 
O(α(n)) where α represents the inverse ackermann function
this represents an almost constant time complexity for both operations 
```

#### What Is the Inverse Ackermann Function and What Makes Our Operations Bound by This?
```
the inverse ackermann function represents a function that grows very slowly, at an almost constant rate
the union find data structure is bound by the inverse ackermann function because of its path compression 
keeping the tree as flat as possible, makes future operations constant
```

## Quick Select
#### What Is the Purpose of the Quick Select Algorithm?
```
to find the k-th smallest (or largest) element in an unsorted array
```

#### How Does It Relate to Quick Sort?
```
it uses a similar partition-based selection method that quick-sort employs
elements are arranged relative to a pivot value
```

#### What is a Partition?
```
its an operation in which an array is rearranged such that elements smaller than a chosen pivot value are moved to one side, and elements larger than the pivot are moved to the other side
the pivot itself is placed in its correct position, which is its final position in a sorted array.
```

#### What Is a Pivot Value?
```
the pivot value is an element chosen from the array that is used to partition the array into two subarrays. 
the pivot is used as a reference to arrange the elements such that those smaller than the pivot are placed before it, and those larger are placed after it. 
```

#### What Are the Major Components of Quick Select?
```
the parition operation that utilises a pivot value
```

#### What Are the General Algorithm Steps?
```
1. choose a pivot (commonly the last element or a random element)
2. parition the array around the pivot value
3. the pivot element should be in its correct position at the end
4. check the pivot's position relative to k
    if `pivotIndex == k`, return the pivot as the k-th smallest element
    if `pivotIndex > k`, recursively apply Quickselect on the left subarray
    if `pivotIndex < k`, recursively apply Quickselect on the right subarray  
```

#### What Is the Average and Worst Case Time Complexity of Quick Select?
```
average case is O(n) due to the efficient partitioning that focuses only on one side of the array
worst case is O(n^2) in the case where the pivot selections are poor and the array is not divided efficiently
```

## Binary Search Trees
#### What Makes a Binary Search Tree Balanced?
```
a binary tree is balanced when the height of the left and right subtrees never exceeds a height difference of 1
```

#### Why Are Balanced Trees Important?
```
having a balanced tree ensures that insertion and deletion and searching of nodes in the tree has a maximum time compelxity of O(log n)
an unbalanced tree can cause these operations to reach up to O(n) (which is essentially just a linked list)
```

#### List Some Types of Balanced Binary Search Trees.
```
- AVL tree
- Red-Black tree
```

#### What Types of Rotations Are There for Self-Balancing Trees?
```
left rotation - when a right-heavy subtree needs to be balanced
right rotation - when a left-heaby subtree needs to be balanced
left-right rotation - when a node is right-heavy in the left subtree
right-left rotation - when a node is left-heavy in the right subtree
```

#### How Do These Rotations Work?
```
left rotation: shifts a node down to the left and lifts its right child up
right rotation: shifts a node down to the right and its left child up
left-right-rotation: rotate left on the left child, followed by a right rotation on the root
right-left rotation: rotate right on the right child, followed by a left rotation on the root
```

#### What Are the Properties of an AVL Tree?
```
its a binary search tree that follows the same rules of elements that are less than the root go into the left subtree, elements that are greater go into the right
it holds an additional height property that can manage whether the tree is balanced or not 
the rotations occur upon insertion of a new element 
```

#### What Are the Properties of a Red-Black Tree?
```
each node in the tree follows colouring rules (either red or black) to enforce balance
    the colour of the node is determined by a isRed boolean parameter
    nodes by default are set to red
the root is always black
every leaf node (null) is considered black
a red node cannot have a red child (no two consecutive red nodes)
every path from a node to its descendant leaves must have the same number of black nodes
```

#### How do AVL and Red-Black Trees Compare?
```
AVL trees are more balanced than a red-black tree
AVL trees will incur more rotations during insertion and deletion of nodes
```

## Minimum Spanning
#### What Is a Minimum Spanning Tree?
```
a minimum-spanning-tree is a subgraph for a given connected, weighted graph that forms a path to all vertices with the minimum total edge weight
```

### For Prim's Algorithm:
#### What Is the Approach?
```
prim's algorithm is a greedy algorithm 
it will start at an arbitrary vertex
and will recursively pick the neighbouring vertex with the lowest edge weight that is not already a member of the MST
```

#### What Use Case Is It Suitable For?
```
it is good for dense graphs since it incrementally grows the MST by exploring edges
```

#### What Data Structure Is Utilised?
```
prim's algorithm uses a min-heap (priority queue) to select and manage the minimum weight edge
```

#### What Is the Time Complexity of the Algorithm?
```
O(E log V)
where E is the number of existing edges in the priority queue
and log V is the extract min function for our priority queue
```

#### Where Is the Starting Point?
```
it can start at any edge (usually based on sorted order)
```

#### What Are the General Algorithm Steps?
```
1. initialize all vertices as unexplored
2. start from any vertex and add it to the MST
3. use a priority queue to find the smallest edge that connects an explored vertex to the MST
4. repeat the process until all vertices are part of the MST
```

### For Kruskal's Algorithm:
#### What Is the Approach?
```
sorts all edges in the graph first
adds them one-by-one, ensuring no cycles are formed
treats the graph as a collection of disjoint sets
each vertex starts as its own separate subgraph
merges these sets by adding the smallest edges between components
```

#### What Use Case Is It Suitable For?
```
its suitable for sparse graphs since we are preprocessing edges and sorting them
```

#### What Is the Time Complexity of the Algorithm?
```
O(E log E)
where the preprocessing and sorting of edge weights is the dominance relation of E log E
```

#### What Data Structure Is Utilised?
```
kruskals algorithm uses the union find data structure to connect subgraphs together
```

Where Is the Starting Point?
- What Are the General Algorithm Steps?

## Pathing Finding Algorithms
#### What Is Dijkstra's Shortest Path Algorithm?
```
it finds the shortest path between a source and destination node
```

#### What Graph Types Does It Work With?
```
works in weighted, directed or undirected graphs
does not work with graphs that have negatively weighted edges
```

#### What Data Structure Does Dijkstra's Incorporate?
```
uses a priority queue (min-heap) to store nodes based on their current shortest distance from the source node
```

#### What Is the Time Complexity of the Algorithm?
```
O((V+E) log V)
where (V+E) is the sum of the number of vertices and edges which captures the size of the graph
and log V is the extraction of the minimum element from the heap
```

#### What Are the General Steps for the Algorithm?
```
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
```

#### In What Case Would Dijkstra's Not Be Suitable?
```
if our graph has negatively weighted edges
```

#### What is the Bellman-Ford Shortest Path Algorithm?

#### What Graph Types Does it Work With?

#### What Data Structure Does it Incorporate?

#### What is the Time Complexity of the Algorithm?

#### What are the General Steps for the Algorithm?

#### In What Case Would Bellman-Ford Not Be Suitable?

---
## ADM Questions:

- what is the RAM computation model
- what are the 3 types of algorithm analysis
- what are the common types of growth rates 
- what are dominance relations in terms of algorithm analysis

- what are the two primary categories of data structures
- how do hash functions work
- how are collisions handled in hash tables

- name 1 common application of sorting
- what is in-place sorting
- what is stability in sorting 
- what are the common time complexties of 'efficient' sorting algorithms, provide some examples for each
- what is the theoretical limit for comparison based sorting
- how does heapsort work
- how does mergesort work
- how does quicksort work
- how does insertion sort work
- how does binary search work
- what searching method is there that enabled constant-time-look-ups

- what is an undirected graph
- what is a directed graph
- what is a weighted graph
- what is a bipartite graph
- what is a cyclic graph
- what is an acyclic graph
- what is a connected graph
- what is a disconnected graph 
- what is a network flow algorithm

- what is combinatorial search
- why do we need combinatorial search
- what are the key concepts of combinatorial search methods
- what is backtracking 
- what is search pruning
- what are heuristic search methods
- provide some examples of heuristic search methods

- what is dynamic programming
- what are its key concepts
- what is a bottom-up approach
- what is a top-down approach

- what is a reduction 
- what is NP-completeness
- what is polynomial-time (P)
- what is nodeterministic polynomial time (NP)
- explain the concept of P = NP 
- what is considered NP-hard
- explain Satifiability (SAT) and its relation to NP-completeness

- what is a greedy algorithm
- what is a brute force algorithm
- what is divide and conquer