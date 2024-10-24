# **Doubly Linked List**

## **1. Overview**

- A **linear data structure** where each node points to both its **previous and next node**.
- Allows for **bi-directional traversal** (forward and backward).
- **More flexible** than a singly linked list but requires **more memory** due to the additional pointer.

![doubly linked list](https://media.geeksforgeeks.org/wp-content/uploads/20240809123741/Insertion-at-the-End-in-Doubly-Linked-List-copy.webp)

---

## **2. Structure**

```cpp
struct DNode {
    int data;
    DNode* prev;
    DNode* next;

    DNode(int value) : data(value), prev(nullptr), next(nullptr) {}
};
```

---

## **3. Unique Operations**


| **Operation**         | **Doubly Linked List**   | **Singly Linked List** |
|-----------------------|--------------------------|------------------------|
| Reverse Traversal     | O(n)                     | Not Possible           |
| Delete From End       | O(1)                     | O(n)                   |
| Insert Before Node    | O(1)                     | O(n)                   |
| Delete Arbitrary Node | O(1)                     | O(n)                   |
| Insert At End         | O(1) with tail pointer   | O(n)                   |

---

### **Reverse Traversal**

```cpp
void reverseTraversal(DNode* tail) {
    DNode* temp = tail;
    while (temp != nullptr) {
        std::cout << temp->data << " <- ";
        temp = temp->prev;
    }
    std::cout << "null" << std::endl;
}
```

---

### **Delete From End**

```cpp
void deleteFromEnd(DNode*& head, DNode*& tail) {
    if (tail == nullptr) return;  // Empty list

    if (tail == head) {  // Only one node
        delete tail;
        head = tail = nullptr;
        return;
    }

    DNode* temp = tail;
    tail = tail->prev;
    tail->next = nullptr;
    delete temp;
}
```

---

### **Insert Before Node**

```cpp
void insertBefore(DNode*& node, int value) {
    DNode* newNode = new DNode(value);
    newNode->next = node;
    newNode->prev = node->prev;

    if (node->prev != nullptr) {
        node->prev->next = newNode;
    }
    node->prev = newNode;
}
```

---

### **Delete Arbitrary Node**

```cpp
void deleteNode(DNode*& node) {
    if (node->prev != nullptr) node->prev->next = node->next;
    if (node->next != nullptr) node->next->prev = node->prev;
    delete node;
}
```

---

### **Insert At End**

```cpp
void insertAtEnd(DNode*& head, DNode*& tail, int value) {
    DNode* newNode = new DNode(value);

    if (tail == nullptr) {  // Empty list case
        head = tail = newNode;
        return;
    }

    tail->next = newNode;
    newNode->prev = tail;
    tail = newNode;
}
```
