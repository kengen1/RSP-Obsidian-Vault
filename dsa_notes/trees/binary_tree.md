# Binary Tree

![Binary Tree](https://cdn.programiz.com/sites/tutorial2program/files/binary_tree_1.png)

## 1. Overview

- non linear data structure
- each node can have at most two children (left and right)
- applied in problems involving hierarchical relationships

Concept: *height*

- the length of the path from the root to the deepest node

Concept: *balance*

- a tree is considered balanced when:
- the height difference between the left and right subtrees is no more than 1

## 2. Structure

```cpp
struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int value) : data(value), left(nullptr), right(nullptr);
}
```

## 3. Operations


| Operation | Description                                       | Time Complexity (Balanced) | Time Complexity (Unbalanced) | Space Complexity                       |
| ----------- | --------------------------------------------------- | ---------------------------- | ------------------------------ | ---------------------------------------- |
| Insert    | Inserts a new node into the binary tree.          | O(log n)                   | O(n)                         | O(log n) (balanced), O(n) (unbalanced) |
| Delete    | Deletes a specific node from the binary tree.     | O(log n)                   | O(n)                         | O(log n) (balanced), O(n) (unbalanced) |
| Search    | Searches for a specific value in the binary tree. | O(log n)                   | O(n)                         | O(log n) (balanced), O(n) (unbalanced) |
| Traversal | In-order, Pre-order, Post-order traversal.        | O(n)                       | O(n)                         | O(n)                                   |


### Insertion
- If the value is smaller, insert it into the left subtree
- If the value is larger or equal, insert it into the right subtree

```cpp
TreeNode* insert(TreeNode* root, int value) {

    if(root == nullptr) return new TreeNode(value);

    if(value < root->data) root->left = insert(root->left, value);
    else insert(root->right, value);

    return root;
}
```

### Deletion
- if the node to delete is found, there are three possible cases:
    1. node has no children - delete directly
    2. noed has one child - replace node with child
    3. node has two children - find the minimum node in the right subtree,
        replace the current node's data with it, and delete the duplicate
```cpp
TreeNode* findMin(TreeNode* node) {
    while(node->left != nullptr) node = node->left;
    return node;
}

TreeNode* deleteNode(TreeNode* root, int key) {
    if(root == nullptr) return root;

    if(key < root->data) {

        root->left = deleteNode(root->left, key);

    } else if (key > root->data) {

        root->right = deleteNode(root->right, key);

    } else {

        if(root->left == nullptr) {
            TreeNode* temp = root->right;
            delete root;
            return temp;
        } else if(root->right == nullptr) {
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }

        TreeNode* temp = findMin(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}
```

### Search
- If the key is smaller, search the left subtree.
- If the key is larger, search the right subtree.

```cpp
bool search(TreeNode* root, int val) {
    if(root == nullptr) return false;
    if(root->data == val) return true;
    if(val < root-> data) return search(root->left, val);
    return search(root->right, val);
}
```
### Traversal
**See traversal markdown files for details...**

## 4. Recusrion in Tree Operations
- recrusion is commonly used in tree operations because **trees are recursive data structures**
    - each node in a tree has subtrees
- allows for complex problems to be broken down into smaller sub-problems
- the function call stack handles the order of node processing without requiring additional logic 
- **Alternative to recursive operations**: while loops combined with stacks or queues can achieve the same result as recursion
