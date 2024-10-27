# Red-Black Trees

## 1. Overview
- a Red-Black Tree (RBT) is a self-balancing Binary Search Tree
- ensures that the tree remains balanced with O(log n) time compelxity for insertion, deletion and search
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


Links:
 red black trees: https://www.youtube.com/watch?v=qvZGUFHWChY
 red black tree rotations: https://www.youtube.com/watch?v=95s3ndZRGbk
 red black tree insertions : https://www.youtube.com/watch?v=4O66Vwldxqo
 red black tree visualizer : https://www.cs.usfca.edu/~galles/visualization/RedBlack.html
 