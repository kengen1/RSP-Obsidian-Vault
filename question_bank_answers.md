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
	if(root == nullptr) return new TreeNode(val);
	if(val < root->data) root->left = insertTreeNode(root->left, val);
	else if (val > root->data) root->right = insertTreeNode(root->right, val);
	return root;
}
```

```cpp
TreeNode* findMin(TreeNode* node) {
	while(node->left != nullptr) node = node->left;
	return node;
}

TreeNode* deleteTreeNode(TreeNode* root, int val) {
	if(root == nullptr) return root;
	
	if(val < root->data) {
		root->left = deleteNode(root->left, val);
	}
	else if (val > root->data) {
		root->right = deleteNode(root->right, val);
	}
	else {

		if(root->left == nullptr) {
			TreeNode* temp = root->right;
			delete root;
			return temp;
		}
		else if (root->right == nullptr) {
			TreeNode temp = root->left;
			delete root;
			return temp;
		}

		TreeNode* temp = findMin(root->right);
		root->data = temp->data;
		root->right = deleteNode(root-right, temp->data);
	}
	return root;
}
```

```cpp
bool search(TreeNode* root, int val) {
	if(root == nullptr) return false;
	if(root->data == val) return true;
	if(val < root->data) return search(root->left, val);
	return search (root->right, val);
}
```

```cpp
TreeNode* inorderTraversal(TreeNode* root) {
	if(root ==  nullptr) return;
	inorder(root->left);
	std::cout << root->data << " ";
	inorder(root->right);
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

#### Implement BFS Using a Queue
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

#### Implement DFS Using Recursion
```cpp
void DFS(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;
    std::cout << node << " ";

    for (int neighbor : adj[node]) {
        if (!visited[neighbor])
            DFS(neighbor, adj, visited);
    }
}
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

#### What is the Space Complexity of a Trie
```
O(N * M) where N is the number of words with an average character length of M
```

## Vector Amortised Time
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

#### What Can Be Done to Reduce the Probability of the Worst Case?
```
randomization of the pivot value 
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
```
finds the shortest path from a source node to all other nodes
takes a dynamic programming approach that iteratively relaxes edges up to V-1 times
```

#### What Graph Types Does it Work With?
```
suited for weighted, directed or undirected graphs
it can handle both positive and negatively weighted edges but no negative cycles
```

#### What Does Relaxing Edges Mean?
```
relaxing an edge means updating the shortest distance estimate for a vertex if a shorter path is found by traversing that edge
relaxing edges is trying to improve the shortest path estimates by exploring whether a given edge provides a shorter route to a vertex
```

#### Relaxation in Dijkstra's vs. Bellman-Ford
```
dijkstra's algorithm relaxes edges greedily (choosing the vertex in order of its distance)
    and it will relax them iteratively for all edges connected to the currently selected vector

bellman-ford relaxes all edges V-1 times
```

#### What is the Time Complexity of the Algorithm?
```
O(V * E)
since the relaxing of edges involves processing E edges V-1 times
```

#### What are the General Steps for the Algorithm?
```
1. initialize - set the distance of the source node to 0 and all other nodes to infinity 
2. conduct edge relaxation (repeated V-1) times
3. negatice cycle check
	1. perform a final pass through to check all edges for negative weights
	2. if any edge can still be relaxed, then we know that a negatively weighted edge exists and therefore there is not valid shortest path
```

#### In What Case Would Bellman-Ford Not Be Suitable?
```
negatively weighted cycles
dijkstra's shortest path might be more suitable for graphs that wont have negatively weighted edges
```
---
## ADM Questions:

#### What is the RAM Computation Model?
```
stands for random access machine
its a form of algorithm analysis where every basic operation takes constant time
memory access takes constant time, regardless of where its located 
```

#### What Is the Purpose of RAM ?
```
while it simplifies assumptions, it provides a practical abstraction to predict algorithm performance 
```

#### What are the 3 Types of Notation?
```
big O - describes the upper bound of the growth rate and reflects the worst case performance 
big omega - represents lower bound performance 
big alpha - represents tight bounds , where algorithms perform in a narrow range of efficiency 
```

#### What are 3 Types of Algorithm Analysis?
```
best case
average case
worst case
```


#### What are the Common Types of Growth Rates?
```
constant time - the problem does not grow with increase in size
linear time - grows linearly with the problem size
logaritmic time - grows slowly (the problem space halves with each iteration)
log-linear time
quadratic time - grows with the square of the input size 
exponential time - time doubles for each additional input
factorial time - time grows dramatically with the problem size 
```


#### What are Dominance Relations In Algorithm Analysis?
```
the inefficiency of an algorithm's growth rate takes priority over smaller / more efficient ones
it simplfies the representation of Big O notation, as we only care about the dominant growth rate 
```

#### What are Two Primary Categories of Data Structures?
```
contiguous data structures - represented and stored in sequential blocks of memory
linked data strucutre - represented by pointers in memory
```


#### What are the Benefits of Both?
```
contiguous: efficient for indexing and immediate access to elements
	bad for resizing 

linked: can dynamically resize efficiently but we need to traverse the structure in order to access an element
```


#### What is a Hash?
```
its a fixed sized number within a specific range
```

#### How do Hash Functions Work?
```
inputs are mapped to hashes
these hashes represent a range of memory (or array of buckets) where elements are stored
the hash function distributes elements evenly across buckets
```

#### What is a Collision?
```
when two different keys hash to the same bucket
```

#### How are Collisions Handled in Hash Tables?
```
chaining - each bucket contains a linked list to store multiple elements
open addressing - probe the next available bucket according to a specific rule
```

#### What are Some Probing Strategies?
```
linear probing - check the next bucket over until we find a space 
quadratic probing - uses a quadratic function to determine the next slot
double hashing - use a second hash function to calculate the next slot
```

#### Name 1 Common Application of Sorting
```
binary search, elements need to be sorted before we can efficiently search a list
```

#### What is In-Place Sorting?
```
sorting of elements in its original data structure, additional memory or space is not required 
```

#### What is Stability Sorting?
```
maintaining the oreder of equal elements 
e.g. if there were the elements {1,1,1} in a list, these ones should remain in their relative order once the entire list is sorted 
```


#### What are the Common Big O Notations of 'Efficient Sorting'
```
quadratic sorting (O(n^2)) - if 'good enough' for relatively small datasets
log-linear sorting (O(n log n)) - necessary for large datasets
```

#### What are Some Examples of These Efficient Sorting Algorithms?
```
quadratic sorting : bubble sort, insertion sort
log linear sorting : heap-sort, merge-sort, quick-sort
```

#### What is the Theoretical Limit for Comparison Based Sorting?
```
O(n log n) is often the best possible time complexity that we can achieve
this is due to the fact that there are n! possible orderings for n elements
```

#### How Does HeapSort Work and What is Its TC?
```
Time Complexity : O(n log n)
utilises a max heap to sort elements 
where we extract the maximum elements and place it at the end 
heapify the remaining elements
```

#### How does MergeSort Work and What is its TC?
```
Time Complexity: O(n log n)
divide the list into two halves and recursively sort both halves
merge the sorted halves

merge sort is a stable sorting algorithm
merge sort is not an in-place sorting algorithm
```

#### How does QuickSort Work and What is its TC?
```
Average Case TC : O(n log n)
Worst Case TC : O(n^2) if the random pivot elements are poor

choose a pivot element 
parition the array around the pivot
recursively sort the partitions
```

#### How does Insertion Sort Work and What is its TC?
```
TC : O(n^2)
has a good use case when data is nearly sorted
is an in-place sorting alrogithm

we start from the second element
compare it with the previous elements and place it in the correct position
```

#### How Does Binary Search Work?
```
Time Complexity : O(log n)
provides an efficient search algorithm for sorted data

iteratively cut the search space in half and we compare the target with a calculated midpoint element
```

#### Name a Searching Method for Constant Time Lookups
```
hashmaps / dictionaries enable constant time lookups at the expense of using additional memory to store key value pairs
```

#### What is an Undirected Graph?
```
where you can traverse edges in either direction
```

#### What is a Directed Graph?
```
edges can only be taverse from a single direction
edges point from one vertex to another, but not vice versa unless explicitly defined
```


#### What is a Weighted Graph?
```
a graph where edges hold weight or a cost for traversing them 
```

#### What is a Bipartite Graph?
```
graphs that can be coloured with two colours without conflcits 
conflicts arise when two adjacent or neighbouring nodes hold the same colour
```

#### What is a Cyclic Graph?
```
the edges connecting nodes form a closed cycle (the path starts and ends with the same vertex)
```

#### What is an Acyclic Graph?
```
a graph with no cycles
```

#### What is a DAG?
```
a directed graph with no cycles
Directed Acyclic Graph
```

#### What is a Connected Graph?
```
every vertex is reachable from any other vertex
```

#### What is a Disconnected Graph?
```
Multiple components or subgraphs that are not connected by edges
```

#### What is a Network Flow Algorithm?
```
an algorithm that optimizes the flow of data from a source node to a sink node 
this algorithm takes into account capacity constraints in the graph where edges can only hold a limited amount of flow 
```

#### What is Combinatorial Search
```
its the process of explorinig all possible combinations or arrangements of elements to find solutions that meet specific criteria or constraints
```

#### Why Do We Need Combinatorial Search
```
its essential for problems where you need to consider all possible configurations to find the optimal or valid solution
```

#### What are the Key Concepts of Combinatorial Search Methods?
```
- represents the entire solution space (all possible configurations)
- a cost function that assigns value to each configuration
- search pruning to reduce unecessary exploration by discarding configurations
```

#### What is Backtracking?
```
the systematic way of building a solution step-by-step and undoing steps when you encounter a dead end of sub-optimal configuration
it provides a systematic method to iterator through all possible configurations of a search space 
```

#### What is Search Pruning?
```
the enhancement of backtracking by eliminating infeasible paths EARLY, reducing the number of configurations that need to be explored
```

#### What are Heuristic Search Methods?
```
the method of finding "good enough" solutions for complex combinatorial problems where exhaustive search is infeasible

they use rules or strategies to find reasonably optimal solutions within an appropriate time frame

they prioritize efficiency over guaranteed correctness
```


#### Provide Some Examples of Heuristic Search Methods
```
Monte Carlo (Random Sampling) - randomly generates and evaluates configurations to find a good solution

Simulated Annealing - evaluates neighbouring configurations and moves to a better one if it exists 

Local Search - iteratively improves the current configuration by exploring neighbouring solutions 
```

#### What is Dynamic Programming
```
dynamic programming is an optimization method that solves problems by breaking them into smaller subproblems, storing their results, and reusing them to avoid repeated work
```

#### What is a Bottom-Up Approach
```
The bottom-up approach solves dp problems iteratively. 
It starts with the smallest subproblems and builds up to the final solution, storing intermediate results in a table (tabulation). 
This approach avoids recursion entirely and calculates results in a specific order, often based on the dependencies of the subproblems.

```

#### What is a Top-Down Approach
```
The top-down approach solves dp problems recursively. 
It starts with the main problem and breaks it into smaller subproblems as needed. 
Results of solved subproblems are stored in a cache (memoization) to avoid redundant computation in future recursive calls.

the cache is typically implemented as an array, hashmap or dictionary that is shared across the call stack
```

#### What is the Structure of a Dynamic Programming Solution?
```
1. define subproblems
2. formulate recurrence relation - establish how each subproblem relates to its smaller subproblems
3. set up base cases - define initial values for the simplest subproblems to anchor the recurrence relation
4. choose top-down or bottom-up approach
```

#### What is a Reduction?
```
a technique for proving compelxity by transforming one problem into another
```

#### What is NP-Completeness?
```
the concept of categorizing problems based on their solvability in polynomial time
the problem is as hard as any other problem in NP, meaning we can reduce any problem to them in polynomial time
```

#### What is Polynomial Time (P)?
```
problems that can be solved quickly 
"quickly" is denoted as O(n^k) for some constant k
polynomial time implies a managable growth rate, making the solution feasible for large inputs
```
#### What is Non-Deterministic Polynomial Time (NP) ?
```
problems where a proposed solution can be verified quickly 
```

#### Explain the Concept of P = NP?
```
if every problem that can be verified in polynomial time can also be solved in non-deterministic polynomial time

it would mean that any problem whos solution can be verified quickly can also be solved quickly
```

#### What is Considered NP-Hard?
```
NP hard problems are at least as hard as the hardest problem in NP but no necessarily in NP
```

#### Explain Satisfiability (SAT) and its Relation to NP-Completeness
```
SAT problem asks if there exists an assignment of true/false values to variables such that a Boolean formula is satisfied 
```

#### What is a Greedy Algorithm?
```
a technique where you use a heuristic to choose the most optimal local solution for each iteration
```

#### What is a Brute Force Algorithm?
```
aka exhaustive search
a brute force algorithm explores all possible solutions to a problem to find the correct one, often without considering efficiency.
```

#### What is Divide and Conquer?
```
breaks a problem into smaller subproblems, solves them independently, and combines their solutions to solve the original problem.
```
