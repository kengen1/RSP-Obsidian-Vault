# Deque (Double-Ended-Queue)

## 1. Overview
- allows for insertion and deletion from both ends of the queue
- combines the properties of both **stacks** and **queues**
- **C++ Standard Template Library (STL)** provides the `std::deque` class for implementation

## 2. Operations

| **Operation**  | **Time Complexity** | **Description**                    |
|----------------|---------------------|------------------------------------|
| push_back      | O(1)                | Adds an element to the rear.       |
| push_front     | O(1)                | Adds an element to the front.      |
| pop_back       | O(1)                | Removes the last element.          |
| pop_front      | O(1)                | Removes the first element.         |
| front          | O(1)                | Returns the first element.         |
| back           | O(1)                | Returns the last element.          |
| empty          | O(1)                | Checks if the deque is empty.      |
| size           | O(1)                | Returns the number of elements.    |
| at / operator[]| O(1)                | Accesses the element at a given index. |


## 3. STL Implementation

```cpp
int main() {
    deque<int> dq;

    // Add elements to both ends
    dq.push_back(10);
    dq.push_front(20);

    cout << "Front: " << dq.front() << endl;  // Output: 20
    cout << "Back: " << dq.back() << endl;    // Output: 10

    // Access elements by index
    dq.push_back(30);
    cout << "Element at index 1: " << dq[1] << endl;  // Output: 10

    // Remove elements from both ends
    dq.pop_front();
    cout << "After pop_front, front: " << dq.front() << endl;  // Output: 10

    dq.pop_back();
    cout << "After pop_back, back: " << dq.back() << endl;  // Output: 10

    // Check size and if it's empty
    cout << "Size: " << dq.size() << endl;  // Output: 1
    cout << "Is empty? " << (dq.empty() ? "Yes" : "No") << endl;

    return 0;
}
```