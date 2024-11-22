# Linked List

![Linked List Data Structure](https://cdn.programiz.com/sites/tutorial2program/files/linked-list-concept.png)

## 1. Overview

* is a linear data structure
* elements of a linked list are called nodes
* nodes are connected using pointers
* each node contains data and a reference to the next node in the sequence
* they provide **dynamic** memory allocation and are used in scenarios where frequent insertion and deletion of elements is required

## 2. Structure

```cpp
struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};
```

## 3. Operations


| Operation           | Description                                                                | Time Complexity | Space Complexity |
| --------------------- | ---------------------------------------------------------------------------- | ----------------- | ------------------ |
| insertAtBeginning   | Attaches a new node at the start of the linked list.                       | O(1)            | O(1)             |
| insertAtEnd         | Attaches a new node at the end of the linked list.                         | O(n)            | O(1)             |
| insertAtPosition    | Attaches a new node at a specific position in the linked list.             | O(n)            | O(1)             |
| deleteFromBeginning | Removes the head of the linked list and updates the head to the next node. | O(1)            | O(1)             |
| deleteFromEnd       | Removes the node present at the end of the linked list.                    | O(n)            | O(1)             |
| deleteFromPosition  | Removes a node from a given position in the linked list.                   | O(n)            | O(1)             |
| iterate             | Prints all the values of the nodes present in the linked list.             | O(n)            | O(1)             |

### insertAtBeginning

```cpp
void insertAtBeginning(Node*& head, int value) {
    Node* newNode = new Node(value);
    newNode->next = head;
    head = newNode;
}
```

### insertAtEnd

```cpp
void insertAtEnd(Node*& head, int value){
    Node* newNode = new Node(value);
  
    if(head == nullptr) {
        head = newNode;
        return;
    }

    Node* temp = head;      //iterator node

    while(temp->next != nullptr) {  // iterate through the list to find the tail node
        temp = temp->next;
    }

    temp->next = newNode;   // assign the tail's next to point to our newly inserted node
}
```

### insertAtPosition

```cpp
void insertAtPosition(Node*& head, int position, int value) {
    Node* newNode = new Node(value);

    if(position == 0) {    // edge case
        insertAtBeginning(head, value);
        return;
    }

    Node* temp = head;  // iterator node

    for(int i = 1; i < position && temp != nullptr; i++) {
        temp = temp->next;
    }

    if(temp == nullptr) return; // position is out of bounds (invalid)

    newNode->next = temp->next;
    temp->next = newNode;
}
```

### deleteFromBeginning

```cpp
void deleteFromBeginning(Node*& head) {
    if(head == nullptr) return;     // if list is empty

    Node* temp = head;
    head = head->next;
    delete temp;        //remember to deallocate memory after removing unwanted node
}
```

### deleteFromEnd

```cpp
void deleteFromEnd(Node*& head) {
    if(head == nullptr) return;     //empty list case

    if(head->next == nullptr) { 
        delete head;
        head = nullptr;
        return;
    }

    Node* temp = head;      // traversal node

    while(temp->next != nullptr) {  // traverse to the second-last node in the list
        temp = temp->next;
    }

    delete temp->next;
    temp->next = nullptr;
}
```

### deleteFromPosition

```cpp
void deleteFromPosition(Node*& head, int position) {
    if(position == 0) { 
        deleteFromBeginning(head);
        return;
    }

    Node* temp = head;  // iterator node

    for(int i=1; i < position && temp->next != nullptr; i++) {
        temp = temp->next;
    }

    if(temp->next == nullptr) return;

    Node* nodeToDelete = temp->next;
    temp->next = temp->next->next;
    delete nodeToDelete;
}
```

### Display / Iterate

```cpp
void display(Node* head) {
    Node* temp = head;
    while (temp != nullptr) {
        std::cout << temp->data << " -> ";
        temp = temp->next;
    }
    std::cout << "null" << std::endl;
}
```
