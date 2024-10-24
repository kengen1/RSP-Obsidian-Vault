# Doubly Linked List

## 1. Overview
- is a linear data structure
- each node points to both its previous and next node
- allows for bi-directional travel
- more flexible than a singly linked list but requires more memory due to the additional pointer

![doubly linked list](https://media.geeksforgeeks.org/wp-content/uploads/20240809123741/Insertion-at-the-End-in-Doubly-Linked-List-copy.webp)

## Structure
```cpp
struct DNode {
    int data;
    DNode* prev;
    DNode* next;

    DNode*(int value) : data(value), prev(nullptr), next(nullptr);
};
```