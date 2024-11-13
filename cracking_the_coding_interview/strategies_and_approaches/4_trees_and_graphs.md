# Trees and Graphs

- avoid abiguous assumptions to do with the type of tree you are dealing with in a question:
    - tree vs. binary tree
    - binary tree vs. bst
    - balance vs. unbalanced
    - complete - full - perfect binary trees

- traversal types
    - in-order is the most common
    - the common cases for using traversal types on interview questions

- binary heaps
    - how to idenitfy heap questions and their implementation in ambiguous questions

- tries being a type of n-ary tree that are used to store characters (between 1 and 26 chars)
- while a hash table can quickly look up whether a string is a valid word, it cannot tell us if a string is a prefix of any valid words. A trie can do this quickly
- many problems involving lists of valid words leverage a trie as an optimization 
- used in situations where we search through the tree on related prefixes repeatedly (e.g., looking up M, then MA, then MAN, then MANY)


- for graphs, DFS is often preferred if we want to visit every node in the graph (due to simplicity of implementation)
- for finding the shortest path (or any path) between two nodes, BFS is generally better
- if you are asked to implement a BFS, the key thing to remember is the ues of the queue

- bidirectional search runs two BFS , one from the source and destination node
- search completes when the two paths collide, upon which they are merged together
- note its behaviour on directed graphs
- note the increase in speed compared to traditional BFS
- when to use traditional BFS and when to use bi-directional search