# Rotations in Balanced Binary Search Trees

## 1. Overview

- Rotations are used to **restructure or "balance" a tree** when a node's insertion or deletion violates the balancing rules
- They ensure that the height of the tree remains logarithmic (O(log n))

***Are rotations the same for AVL and Red-Black Trees?***

- Yes, both AVL and Red-Black Trees use the **same types of rotations**: **Left Rotation**, **Right Rotation**, **Left-Right Rotation**, and **Right-Left Rotation**.
- However, **AVL Trees** apply rotations more frequently (after every insertion or deletion), while **Red-Black Trees** apply rotations only to maintain color properties.

## 2. Types of Rotations


| **Rotation Type**   | **When It’s Used**                              | **Effect**                                    |
| --------------------- | -------------------------------------------------- | ----------------------------------------------- |
| Left Rotation       | When a right-heavy subtree needs to be balanced. | Rotates left to shift nodes leftwards.        |
| Right Rotation      | When a left-heavy subtree needs to be balanced.  | Rotates right to shift nodes rightwards.      |
| Left-Right Rotation | When a node is right-heavy in the left subtree.  | First a left rotation, then a right rotation. |
| Right-Left Rotation | When a node is left-heavy in the right subtree.  | First a right rotation, then a left rotation. |

## 3. Left Rotation
*the left rotation shifts a node down to the left and lifts its right child up*

### Example
![left rotation animation](https://adrianmejia.com/images/left-rotation2.gif)

### Logic / Pseudocode
1. **Identify the nodes**:  
   - Let **1** (`x`) be the node we’re rotating left.  
   - Let **2** (`y`) be the **right child** of `x`.  
   - `3` is the **right child** of `y`.

2. **Reassign relationships**:  
   - `x.right` is set to `y.left`.  
     - In this example, **`y.left` is null**, so `x.right` becomes `null`.
   - `y.left` is set to `x`, making `y` the new parent of `x`.

3. **Update the parent**:  
   - If **`x` was the root**, `y` becomes the **new root** (which is the case in this example).
   - If `x` had a parent (it doesn’t in this case), the parent of `x` would be updated to point to `y`.

---


### **Implementation**
```cpp
AVLNode* leftRotate(AVLNode* x) {
    AVLNode* y = x->right;
    AVLNode* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;   // T2 referring to a temp pointer holding a subtree that would be otherwise lost during rotation

    // Update heights (only needed in AVL trees)
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;  // New root after rotation
}
```

## 4. Right Rotation Example
*right rotation is the mirror of the left rotation, shirting a node down to the right and lifting its left child up*

### Example
![right rotation animation](https://adrianmejia.com/images/right-rotation2.gif)

### Logic / Pseudocode
1. **Identify the nodes**:  
   - Let **3** (`y`) be the node we’re rotating right.  
   - Let **2** (`x`) be the **left child** of `y`.  
   - **1** is the **left child** of `x`.

2. **Reassign relationships**:  
   - `y.left` is set to `x.right`.  
     - In this example, **`x.right` is null**, so `y.left` becomes `null`.
   - `x.right` is set to `y`, making **`x` the new parent** of `y`.

3. **Update the parent**:  
   - If **`y` was the root**, `x` becomes the **new root**.
   - If `y` had a parent (it doesn’t in this case), the parent of `y` would point to `x`.

---
### Implementation
```cpp
AVLNode* rightRotate(AVLNode* y) {
    AVLNode* x = y->left;
    AVLNode* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;   // T2 referring to a temp pointer holding a subtree that would be otherwise lost during rotation

    // Update heights (only needed in AVL trees)
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;  // New root after rotation
}
```

## 5. Left-Right Rotation Example
*a double rotation where we first rotate left on the left child, followed by a right rotation on the root*

### Example
![left-right rotation animation](https://adrianmejia.com/images/left-right-rotation.gif)

### Logic / Pseudocode
1. **Identify the nodes**:  
   - Let **3** (`z`) be the node causing imbalance.  
   - Let **1** (`x`) be the left child of `z`.  
   - Let **2** (`y`) be the right child of `x`.

2. **Perform Two Rotations**:
   - **First Rotation**:  
     - Perform a **left rotation** on node **1** (`x`).  
     - After the left rotation:
       ```
           3
          /
         2
        /
       1
       ```
     - Now node **2** is the new child of **3**, and **1** becomes the left child of **2**.

   - **Second Rotation**:  
     - Perform a **right rotation** on node **3** (`z`).
     - After the right rotation:
       ```
           2
          / \
         1   3
       ```

3. **Reassign relationships**:
   - After the **left rotation**, `x.right` is set to `y.left` (which is null).
   - `y.left` is set to `x`, and `y` becomes the new left child of `z` in the right rotation.

4. **Update the parent**:
   - If **`z` was the root**, `y` becomes the new root.
   - If `z` had a parent, it would be updated to point to `y`.

---

### **Implementation of Left-Right Rotation**

```cpp
AVLNode* leftRightRotate(AVLNode* z) {
    // Step 1: Left rotate the left child of z
    z->left = leftRotate(z->left);

    // Step 2: Right rotate the node z
    return rightRotate(z);
}
```

## 6. Right-Left Rotation
*a double rotation where we first right rotate on the right child, followed by a left rotation on the root*

### Example
Before rotation
```
      10
        \
         30
        /
       20
```

After right rotation on 30, followed by a left rotation on 10
```
      20
     /  \
    10   30
```

### Implementation
```cpp
AVLNode* rightLeftRotate(AVLNode* node) {
    node->right = rightRotate(node->right);
    return leftRotate(node);
}
```