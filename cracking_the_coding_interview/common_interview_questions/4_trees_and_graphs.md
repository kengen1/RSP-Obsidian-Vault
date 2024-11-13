### 1. Route Between Nodes
   - **Problem**: Given a directed graph, determine if there is a route between two nodes.
   - **Solution**: Use BFS or DFS to explore the graph from one node to the other.

### 2. Minimal Tree
   - **Problem**: Given a sorted (increasing order) array with unique integer elements, create a binary search tree (BST) with minimal height.
   - **Solution**: Recursively insert the middle element of the array as the root of each subtree.

### 3. List of Depths
   - **Problem**: Given a binary tree, create a linked list of all nodes at each depth.
   - **Solution**: Use BFS to traverse the tree level by level, adding nodes at each level to a linked list.

### 4. Check Balanced
   - **Problem**: Determine if a binary tree is balanced, defined as a tree where the heights of the two subtrees of any node never differ by more than one.
   - **Solution**: Use a recursive function that checks the height of each subtree, returning -1 if any subtree is unbalanced.

### 5. Validate BST
   - **Problem**: Determine if a binary tree is a binary search tree.
   - **Solution**: Recursively check that each node's value is within an allowed range (derived from parent nodes).

### 6. Successor
   - **Problem**: Find the "next" node (in-order successor) of a given node in a BST.
   - **Solution**: If the node has a right child, the successor is the leftmost node in that subtree; otherwise, traverse up until finding a node that is a left child of its parent.

### 7. Build Order
   - **Problem**: Given a list of projects and dependencies, find an order to build the projects.
   - **Solution**: Use topological sorting with DFS or Kahn’s Algorithm to find an order that satisfies the dependencies.

### 8. First Common Ancestor
   - **Problem**: Find the first common ancestor of two nodes in a binary tree.
   - **Solution**: Traverse the tree from the root, checking where the two nodes split paths. Avoid extra storage by passing information up the recursion.

### 9. BST Sequences
   - **Problem**: Find all possible arrays that could have led to a given BST.
   - **Solution**: Use a recursive approach to weave arrays from left and right subtrees, maintaining relative order within each subtree.

### 10. Check Subtree
   - **Problem**: Determine if one tree is a subtree of another.
   - **Solution**: Traverse the larger tree, checking if the subtree rooted at any node matches the smaller tree.

### 11. Random Node
   - **Problem**: Implement a binary tree node class with a `getRandomNode` function, which returns a random node from the tree.
   - **Solution**: Use the size of each subtree to determine the probability of choosing any particular node.

### 12. Paths with Sum
   - **Problem**: Count the paths that sum to a given value in a binary tree.
   - **Solution**: Use a recursive approach with a hashmap to track cumulative sums as you traverse the tree.
