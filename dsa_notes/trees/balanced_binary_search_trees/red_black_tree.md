# Red-Black Trees

## 1. Overview

- a Red-Black Tree (RBT) is a self-balancing Binary Search Tree
- ensures that the tree remains balanced with O(log n) time complexity for insertion, deletion and search
- each node in a red-black tree follows colouring rules (either red or black) to enforce balance

## 2. Properties of a Red-Black Tree

1. each node is either red or black
2. the root is always black
3. every leaf node (null) is considered black
4. a red node cannot have a red child (no two consecutive red nodes)
5. every path from a node to its descendant leaves must have the same number of black nodes

### Comparison with AVL Trees

- AVL trees are more balanced that a red-black tree
- but AVL trees will cause more rotations to occur during insertion and deletion of nodes

### Balancing Red-Black Trees with Rotations

#### 1. Example: Inserting Nodes (10 -> 20 -> 30)

Before Fixing (Unbalanced State)

```
     10(B)
       \
       20(R)
         \
         30(R)
```

- this configuration **violates the Red-Black Tree property** that no two consecutive red nodes should exist
- 20 and 30 are both red
- simply changing the colour isn't enough because the tree is also unbalanced
- to fix this, we perform a left rotation on node (10)

After Left Rotation on Node 10

```
     20(B)
     /   \
   10(R)  30(R)
```

we have:

- reduced the depth of the right side, balancing the tree by bringing 20 to the root
- recoloured the tree, making the new root black and its children red

## 3. Structure

```cpp
struct RBNode {
    int data;
    RBNode* left;
    RBNode* right;
    RBNode* parent;
    bool isRed;

    RBNode(int value) : data(value), left(nullptr), right(nullptr), parent(nullptr), isRed(true){}
};
```

## 4. Rotations and Colour Flipping

Red-black trees using rotations (similar to AVL trees) and colour flipping to maintain balancing rules

** See "rotations" markdown file for details

## 5. Operations


| **Operation** | **Description**                                  | **Time Complexity** | **Space Complexity** |
| --------------- | -------------------------------------------------- | --------------------- | ---------------------- |
| Insert        | Insert a node with rebalancing                   | O(log n)            | O(log n)             |
| Delete        | Delete a ndoe with rebalancing                   | O(log n)            | O(log n)             |
| Search        | Search for a node in the tree                    | O(log n)            | O(log n)             |
| Rotate        | Rotate the nodes to restore red-black properties | O(1)                | O(1)                 |

### Insertion
when inserting a new node:
1. insert the new node, the same way you would with a normal BST
2. colour the new node red
3. fix any violations of the red-black tree properties using rotations and colour changes

```cpp
RBNode* insert(RBNode* root, RBNode* newNode) {
    if (root == nullptr) return newNode;

    if (newNode->data < root->data) {
        root->left = insert(root->left, newNode);
        root->left->parent = root;
    } else if (newNode->data > root->data) {
        root->right = insert(root->right, newNode);
        root->right->parent = root;
    }

    // Fix violations after insertion
    return fixViolations(root, newNode);
}
```
## 6. Fixing Red-Black Violations

After a rotation has been conducted, colour changes are needed to maintain the Red-Black properties.
There are 3 general cases where recolouring is required:

- **Case 1** : The uncle is red

  - recolour the parent and uncle to black and the grandparents to red
  - move up the tree to fix futher violations
- **Case 2** : The uncle is black, and the node is on the opposite side (left-right or right-left)

  - perform a rotation to align the child and parent (left-right or right-left rotation)
- **Case 3** : The uncle is black, and the node is on the same side (left-left or right-right)

  - perform a single rotation and recolour the parent and grandparent

### Fix-Up Logic:

```cpp
void fixViolations(RBNode*& root, RBNode*& node) {
    while (node != root && node->parent->isRed) {
        if (node->parent == node->parent->parent->left) {
            RBNode* uncle = node->parent->parent->right;

            if (uncle != nullptr && uncle->isRed) {
                // Case 1: Recolor
                node->parent->isRed = false;
                uncle->isRed = false;
                node->parent->parent->isRed = true;
                node = node->parent->parent;
            } else {
                if (node == node->parent->right) {
                    // Case 2: Left rotation on parent
                    node = node->parent;
                    leftRotate(node);
                }
                // Case 3: Right rotation on grandparent
                node->parent->isRed = false;
                node->parent->parent->isRed = true;
                rightRotate(node->parent->parent);
            }
        } else {
            // Mirror case: Parent is right child of grandparent
            RBNode* uncle = node->parent->parent->left;

            if (uncle != nullptr && uncle->isRed) {
                // Case 1: Recolor
                node->parent->isRed = false;
                uncle->isRed = false;
                node->parent->parent->isRed = true;
                node = node->parent->parent;
            } else {
                if (node == node->parent->left) {
                    // Case 2: Right rotation on parent
                    node = node->parent;
                    rightRotate(node);
                }
                // Case 3: Left rotation on grandparent
                node->parent->isRed = false;
                node->parent->parent->isRed = true;
                leftRotate(node->parent->parent);
            }
        }
    }
    root->isRed = false;  // Ensure the root is always black
}
```

---

### Resources / Links
red black trees: https://www.youtube.com/watch?v=qvZGUFHWChY
red black tree rotations: https://www.youtube.com/watch?v=95s3ndZRGbk
red black tree insertions : https://www.youtube.com/watch?v=4O66Vwldxqo
red black tree visualizer : https://www.cs.usfca.edu/~galles/visualization/RedBlack.html