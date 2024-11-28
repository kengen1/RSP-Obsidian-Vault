[[Queue]]
## 1. Overview

- specialized queue where elements are served based on their priority rather than their insertion order
- **C++ Standard Template Library (STL)** provides the `std::priority_queue` class for implementation
- the STL implementation uses a **max-heap**
  - meaning the largest element has the highest priority
- useful for *Dijkstra's algorithm, A search*, task scheduling, and event simulation

## 2. Operations

| **Operation**  | **Time Complexity** | **Description**                       |
|----------------|---------------------|---------------------------------------|
| push / emplace | O(log n)            | Adds an element to the priority queue. |
| pop            | O(log n)            | Removes the element with the highest priority. |
| top            | O(1)                | Returns the element with the highest priority. |
| empty          | O(1)                | Checks if the priority queue is empty. |
| size           | O(1)                | Returns the number of elements.       |

## 3. STL Implementation

```cpp
int main() {
    priority_queue<int> pq;

    pq.push(10);
    pq.push(30);
    pq.push(20);

    cout << "Top element: " << pq.top() << endl;  // Output: 30

    pq.pop();
    cout << "After pop, top element: " << pq.top() << endl;  // Output: 20

    cout << "Size of queue: " << pq.size() << endl;

    return 0;
}
```

## 4. Custom Comparator : How It Works
- the `std::priority_queue` uses a comparison function to determine the priority of elements
- the default priority queue behaves as a **max-heap**, meaning the largest element has the highest priority
- you can change the behaviour to a **min-heap** or any custom order using a custom comparator

### Creating a Min-Heap with `std::greater`

```cpp
int main() {
  // Min-heap priority queue
  priority_queue<int, vector<int>, greater<int>> minHeap;

    minHeap.push(10);
    minHeap.push(30);
    minHeap.push(20);

    cout << "Top element: " << minHeap.top() << endl;  // Output: 10

    return 0;
}
```

### Custom Comparator With Struct
- you can define your own comparator if you want more control over the element order

```cpp
// Custom comparator to sort in ascending order (min-heap)
struct Compare {
    bool operator()(int a, int b) {
        return a > b;  // Returns true if a has lower priority than b
    }
};

int main() {
    // Priority queue with custom comparator
    priority_queue<int, vector<int>, Compare> customPQ;

    customPQ.push(10);
    customPQ.push(30);
    customPQ.push(20);

    cout << "Top element: " << customPQ.top() << endl;  // Output: 10

    return 0;
}
```