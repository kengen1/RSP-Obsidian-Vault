#Trees 
## 1. Overview

- A Binary Search Tree (BST) is a specialized tree where:
  - All nodes in the left subtree contain values less than the parent node
  - All nodes in the right subtree contain values greater than the parent node
- The ordering property enables efficient searching, insertion and deletion

## 2. Properties of a BST

- In-order traversal of a BST results in sorted data
- Duplicate elements can either be disallowed or placed in the right subtree
- A balanced BST ensures that the height is kept O(log n), improving search performance

- A BST is not always balanced
    - dependent on the order of insertion of elements
    - if the elements are inserted in sorted or nearly sorted order, the tree will become skewed

## 3. Additional Operations


| **Operation**   | **Description**                                      | **Time Complexity (Balanced)** | **Time Complexity (Unbalanced)** | **Space Complexity** |
|-----------------|------------------------------------------------------|--------------------------------|----------------------------------|----------------------|
| Find Min / Max  | Finds the minimum/maximum value in the BST.          | O(log n)                       | O(n)                            | O(log n)             |
| Successor       | Finds the next larger element for a given node.      | O(log n)                       | O(n)                            | O(log n)             |
| Predecessor     | Finds the next smaller element for a given node.     | O(log n)                       | O(n)                            | O(log n)             |


### Implementation

## Find Minimum
- found by traversing the leftmost node
```cpp
TreeNode* findMind(TreeNode* root) {
    while(root->left != nullptr) {
        root = root->left;
    }
    return root;
}
```

### Find Maximum
- found by traversing the rightmost node
```cpp
TreeNode* findMax(TreeNode* root) {
    while(root->right != nullptr) {
        root = root->right;
    }
    return root;
}
```

### Finding the Successor
- The successor of a node is the smallest node greater than the current node
- If the node has a right subtree, the successor is the leftmost in the right subtree

```cpp
TreeNode* findSuccessor(TreeNode* root, TreeNode* node) {
    // If the node has a right subtree, the successor is the leftmost node in that subtree
    if(node->right != nullptr) {
        return findMin(node->right);
    }

    // Otherwise, we traverse the tree to find the lowest ancestor for which the node lies in the left subtree
    TreeNode* successor = nullptr;
    while (root != nullptr) {
        if (node->data < root->data) {
            successor = root;  // Potential successor.
            root = root->left; // Move left to continue search.
        } else {
            root = root->right; // Move right if the current root is smaller or equal.
        }
    }
    return successor;}
```

### Finding the Predecessor
```cpp
TreeNode* findPredecessor(TreeNode* root, TreeNode* node) {
    // If the node has a left subtree, the predecessor is the rightmost node in that subtree
    if (node->left != nullptr) {
        return findMax(node->left);
    }

    // Otherwise, we traverse the tree to find the highest ancestor for which the node lies in the right subtree
    TreeNode* predecessor = nullptr;
    while (root != nullptr) {
        if (node->data > root->data) {
            predecessor = root;  // Potential predecessor.
            root = root->right;  // Move right to continue search.
        } else {
            root = root->left;  // Move left if the current root is larger or equal.
        }
    }
    return predecessor;
}
```