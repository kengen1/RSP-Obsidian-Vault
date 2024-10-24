# Queue

## 1. Overview

- linear data structure
- follows the *First-In-First-Out (FIFO)* principle
- elements are added to the rear and removed from the front
- **C++ Standard Template Library (STL)** provides the `std::queue` class for implementation

## 2. Operations


| **Operation** | **Time Complexity** | **Description**                    |
| --------------- | --------------------- | ------------------------------------ |
| Enqueue       | O(1)                | Adds an element to the rear.       |
| Dequeue       | O(1)                | Removes an element from the front. |
| Front         | O(1)                | Returns the front element.         |
| Back          | O(1)                | Returns the rear element.          |
| Empty         | O(1)                | Checks if the queue is empty.      |
| Size          | O(1)                | Returns the size of the queue.     |

*Note* STL queue internally keeps a counter to track its number of elements, which allowes for the `size()` function to be constant

## 3. STL Implementation

```cpp
int main() {
    queue<int> q;

    // Enqueue elements
    q.push(10);
    q.push(20);
    q.push(30);

    cout << "Front element: " << q.front() << endl;  // Output: 10
    cout << "Back element: " << q.back() << endl;    // Output: 30

    // Dequeue elements
    q.pop();
    cout << "After one dequeue, front: " << q.front() << endl;  // Output: 20

    // Check if the queue is empty
    cout << "Is the queue empty? " << (q.empty() ? "Yes" : "No") << endl;

    // Print the size of the queue
    cout << "Queue size: " << q.size() << endl;

    return 0;
}
```
