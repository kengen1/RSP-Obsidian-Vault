[[Linked List]]
## 1. Overview
- a type of linked list where the **last node points to the first node**, forming a circular traversal of pointers
- it can be a singly or doubly linked list, so long as the last node is connected to the head
- there are no null references at the end of the list
- commonly used when a list needs to be repeatedly traversed

![circular linked list](https://media.geeksforgeeks.org/wp-content/uploads/20240917161541/Circular-Linked-List.webp)

## 2. Structure

```cpp
struct CNode {
    int data;
    CNode* next;

    CNode(int value) : data(value), next(nullptr) {}
};
```

## **3. Unique Operations**

| **Operation**        | **Description**                                     | **Time Complexity** | **Space Complexity** |
|----------------------|-----------------------------------------------------|---------------------|----------------------|
| Insert At End        | Adds a node at the end and links it to the head.    | O(n)                | O(1)                 |
| Delete From End      | Deletes the last node and updates the next pointer. | O(n)                | O(1)                 |
| Circular Traversal   | Traverses the list starting from the head.          | O(n)                | O(1)                 |
| Check if Circular    | Checks if the list is circular.                     | O(n)                | O(1)                 |

---

### **Insert At End**
```cpp
void insertAtEnd(CNode*& head, int value) {
    CNode* newNode = new CNode(value);

    if (head == nullptr) {  // Empty list case
        head = newNode;
        newNode->next = head;  // Point to itself
        return;
    }

    CNode* temp = head;
    while (temp->next != head) {
        temp = temp->next;
    }
    temp->next = newNode;
    newNode->next = head;
}
```

---

### **Delete From End**
```cpp
void deleteFromEnd(CNode*& head) {
    if (head == nullptr) return;  // Empty list case

    if (head->next == head) {  // Only one node in the list
        delete head;
        head = nullptr;
        return;
    }

    CNode* temp = head;
    while (temp->next->next != head) {
        temp = temp->next;
    }

    delete temp->next;
    temp->next = head;
}
```

---

### **Circular Traversal**
```cpp
void circularTraversal(CNode* head) {
    if (head == nullptr) return;

    CNode* temp = head;
    do {
        std::cout << temp->data << " -> ";
        temp = temp->next;
    } while (temp != head);

    std::cout << "(head)" << std::endl;
}
```

---

### **Check if Circular**
```cpp
bool isCircular(CNode* head) {
    if (head == nullptr) return true;

    CNode* temp = head->next;
    while (temp != nullptr && temp != head) {
        temp = temp->next;
    }
    return (temp == head);
}
```
