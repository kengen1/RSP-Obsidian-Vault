#Traversal #Trees #DFS #BFS 

## 1. Overview

- Tree traversal is the process of visiting each node in a binary tree exactly once.
- There are two main categories:
  - **Depth-First-Search (DFS)**: Explores as deep as possible along each branch before #Backtracking .
  - **Breadth-First-Search (BFS)**: Visits nodes level-by-level from top to bottom.

## 2. Traversal Types and Use Cases

| **Traversal Type** | **Order**                  | **Use Case**                                                    |
| -------------------- | ---------------------------- | ----------------------------------------------------------------- |
| In-order           | Left → Root → Right      | Retrieve elements in**sorted order** (BST).                     |
| Pre-order          | Root → Left → Right      | **Copy** or **serialize** a tree.                               |
| Post-order         | Left → Right → Root      | **Delete** a tree or **evaluate postfix** expressions.          |
| Level-order        | Top to Bottom (Level-wise) | Explore **hierarchical structures** or find **shortest paths**. |

## 3. Depth-First Search

### 3.1 In-order Traversal

![In-order Traversal](https://media.geeksforgeeks.org/wp-content/uploads/20230303154301/inorder.gif)

#### How it Works:
1. Start with the root node
2. Recursively visit the left subtree until reaching the leftmost node
3. Print the node once the left child has been processed
4. Move to the right subtree and repeat

#### Implementation
```cpp
void inorder(TreeNode* root) {
    if(root == nullptr) return;
    inorder(root->left);
    std::cout << root->data << " ";
    inorder(root->right);
}
```

### 3.2 Pre-order Traversal

![Pre-order Traversal](https://media.geeksforgeeks.org/wp-content/uploads/20230303153728/preordercom-gif-maker.gif)

#### How it Works:
1. Start at the root node and print it
2. Move to the left subtree and recursively traverse it
3. Once the left subtree is done, move to the right subtree

#### Implementation
```cpp
void preorder(TreeNode* root) {
    if(root == nullptr) return;
    std::cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}
```

### 3.3 Post-order Traversal

![Post-order Traversal](https://media.geeksforgeeks.org/wp-content/uploads/20230303154128/postorder.gif)

#### How it Works:
1. Recursively visit the left subtree
2. Once done, visit the right subtree
3. After both subtrees are processed, print the current node

- this traversal is useful when nodes must be processed after their children (e.g., deletion)

#### Implementation
```cpp
void postorder(TreeNode* root) {
    if(root == nullptr) return;
    postorder(root->left);
    postorder(root->right);
    std::cout << root->data << " ";
}
```

## 4. Breadth-First Search

### 4.1 Level-order Traversal

![Level-order Traversal](https://media.geeksforgeeks.org/wp-content/uploads/20240501114531/level-order-in-cpp---animated.gif)

#### How it Works:
1. Use a queue to keep track of nodes at each level
2. Start with the root node in the queue
3. Process the front node from the queue and print it
4. Enqueue the left and right children of the current node (if they exist)
5. Repeat until the queue is empty

#### Implementation
```cpp
void levelOrder(TreeNode* root) {
    if(root == nullptr) return;

    std::queue<TreeNode*> q;
    q.push(root);

    while(!q.empty()) {
        TreeNode* current = q.front();
        q.pop();
        std::cout << root->data << " ";

        if(current->left != nullptr) q.push(current->left);
        if(current->right != nullptr) q.push(current->right);
    }
}
```
