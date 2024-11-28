
## 1. Overview

- an AVL tree is a **self-balancing** [[Binary Search Tree (BST)]]
- the height of the left and right subtrees of any node differs by at most 1
- ensures that the tree remains balanced to maintain O(log n) time complexity for operations like insertion, deletion, and search

## 2. Rotations for Balancing

to maintain balance, AVL trees rotations:

1. **Left Rotation** : Used when the right subtree is heavier
2. **Right Rotation** : Used when the left subtree is heavier
3. **Left-Right Rotation** : Left rotation followed by a right rotation
4. **Right-Left Rotation** : Right rotation followed by a left rotation

*watch this for [AVL Tree Insertion Explanation](https://www.youtube.com/watch?v=1QSYxIKXXP4)*


## 3. Structure

```cpp
struct AVLNode {
    int data;
    AVLNode* left;
    AVLNode* right;
    int height;

    AVLNode(int value) : data(value), left(nullptr), right(nullptr), height(1) {}
};
```

## 4. Operations

| Operation | Description                                     | Time Complexity | Space Complexity |
| ----------- | ------------------------------------------------- | ----------------- | ------------------ |
| Insert    | Inserts a node while maintaining balance        | O(log n)        | O(log n)         |
| Delete    | Deletes a node and rebalances the tree          | O(log n)        | O(log n)         |
| Search    | Searches for a node in the tree                 | O(log n)        | O(log n)         |
| Rotation  | Balances the tree to maintain height properties | O(1)            | O(1)             |


## 5. Implementation

### Helper Function : Get Height
- returns the height of a given **node**
```cpp
int height(AVLNode* node) {
    if(node == nullptr) return 0;
    return node->height;
}
```

### Helper Function : Get Balance Factor
- Balance Factor = height(left subtree) - height(right subtree)
- For each node in an AVL tree:
    - If the left subtree is taller, the balance factor will be positive.
    - If the right subtree is taller, the balance factor will be negative.
    - If the heights are equal, the balance factor will be 0 (perfectly balanced).

```cpp
int getBalance(AVLNode* node) {
    if(node == nullptr) return 0;
    return(node->left) - height(node->right);
}
```

### 1. Right Rotation
*Used when left subtree is heavier*

```cpp
AVLNode* rightRotate(AVLNode* y) {
    AVLNode* rightRotate(AVLNode* y) {
        AVLNode* x = y->left;
        AVLNode* T2 = x->right;

        x->right = y;
        y->left = T2;

        y->height = max(height(y->left), height(y->right)) + 1;
        x->height = max(height(x->left), height(x->right)) + 1;

        return x; // new root
    }
}
```

### 2. Left Rotation
*Used when the right subtree is heavier*

```cpp
AVLNode* leftRotate(AVLNode* x) {
    AVLNode* y = x->right;
    AVLNode* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;  // new root
}
```

### 3. Insertion Operation with Balancing
```cpp
AVLNode* insert(AVLNode* node, int value) {
    // Perform normal BST insertion
    if (node == nullptr) return new AVLNode(value);

    if (value < node->data)
        node->left = insert(node->left, value);
    else if (value > node->data)
        node->right = insert(node->right, value);
    else
        return node;  // Duplicate values not allowed

    // Update height
    node->height = 1 + max(height(node->left), height(node->right));

    // Check the balance factor
    int balance = getBalance(node);

    // Left Left Case
    if (balance > 1 && value < node->left->data)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && value > node->right->data)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && value > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && value < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}
```