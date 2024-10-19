# Chapter 3 : Data Structures

## 3.1 Contiguous vs. Linked Data Structures

* **Contiguous Structures**: These store data sequentially in memory

  * e.g. arrays, matrices, heaps, hash tables
  * efficient for indexing, but resizing is costly
* **Linked Structures**: Elements are connected by pointers

  * e.g. linked lists, trees, graphs, adjacency lists
  * dynamic in size, but accessing an element requires traversal

**Take-home lesson**: Choose contiguous structures for faster access and linked structures for flexibility

## 3.2 Stacks and Queues

* Stack

  * Last In, First Out (LIFO)
  * `push(x)`: add element to the top
  * `pop()`: remove the top element
* Queue

  * First In, First Out (FIFO)
  * `enqueue(X)`: add element to the back of the queue
  * `dequeue()`: remove element from the front of the queue

## 3.3 Dictionaries

* data structures that store key-value pairs for fast lookups
* efficient for storing and retrieving data by unique keys

## 3.4 Binary Search Trees

* a BST organizes data to allow for efficient search, insertion and deletion
* each node has at most two children
* left child < parent < right child
* **balanced trees** maintain a balanced structure to ensure logarithmic operations
  * e.g. AVL or Red-Black Trees

## 3.5 Priority Queues

* allows elements to be processed based on their priority
* e.g. heap data structure (used in heap sort and Dijkstra's algorithm)
* `insert(x)`: add an element
* `extractMin()` or `extractMax()` : remove the element with the highest or lowest priority

## 3.7 Hashing and Strings

* hash tables: use a hash function to map keys to buckets for fast lookups
  * handles collisions using techniques like chaining or open addressing
* string data structures: focuses on efficient string manipulation
  * e.g. suffix trees and **tries**

### How Hash Functions Work

* a hash function maps an input (e.g. a string or an integer) to a fixed-size number (the hash) within a specific range
* this range corresponds to an array of buckets where elements are stored
* ideally, a hash function should:
  1. distribute elements uniformly across buckets
  2. minimize collisions: different inputs should map to different buckets as much as possible

### Handing Collisions in Hash Tables

* when two different keys hash to the same bucket , this is called a **collision**
* there are two common techniques to handling collisions:

#### 1. Chaining

* each bucket contains a **linked list** (or another data structure) to store multiple elements
* read more --> https://www.geeksforgeeks.org/c-program-hashing-chaining/

#### 2. Open Addressing

* when a collision occurs, the algorithm probes the next available bucket to a specific rule
* probing strategies:
  * linear probing: check the next bucket sequentially until an empty slot is found
  * quadratic probing: use a quadratic function to determine the next slot
  * double hashing: use a second hash function to calculate the next slot

#### Trade-offs Between Chaining and Open Addressing

* Chaining
  * more

## 3.8 Specialized Data Structures

* Geometric data structures

  * used for problems involing spatial relationships
  * applications in *nearest neighbour search, collision detection, computational geometry* problems
* Graph data structures

  * consist of vertices (nodes) connected by edges (links)
  * **adjacency list** : lists connected nodes for each vertex (space efficient)
  * **adjacency matrix** : 2D matrix indicating the presence of edges (fast for edge lookup)
  * **weighted graphs** : edges have weights (application in shortest path problems)
  * **directed vs undirected graphs** : edge directionality affects traversal through a graph
  * graphs are used in things like routing application, social networks, dependency graphs

## Take-home Lessons

* choose data structures wisely

  * the right choice depends on the specific problem
  * balancing trade-offs between space and time
* understand access and modification costs

  * data structures differ in how efficiently they perform operations like insertion, search and deletion
