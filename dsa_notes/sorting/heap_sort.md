# Heap Sort

## Overview
- **comparison-based sorting algorithm** that uses a binary heap structure
- it works by building a max-heap from the input data and repeatedly extracting the largest element from the heap
- **in-place-sorting** algorithm, meaning it sorts without requiring extra memory (beyond the recursion stack)
- not stable : meaning the relative order of equal elements may not be preserved


    Time Complexity: *O(n log n)*


### Refresher : *What is a Heap?*
- a heap is a specialized tree-based data structure where elements are organised according to a heap property:
    - Max-Heap : the parent node is greater than or equal to its children
    - Min-Heap : the parent node is less than or equal to its children

### Refresher : *What is a Binary Heap?*
- is a **complete binary tree**, meaning all levels are completely filled except possibly the last, which is filled from left to right 

### Refresher : *What is Heapify?*
- the process of ensuring the max-heap property is maintained in a subtree

## How it Works:
1. Build a max-heap from the input array
2. Extract the root (maximum element) and place it at the end of the array
3. Reduce the heap size and **heapify** the remaining elements
    - compare the root node with its left and right children
    - if one of the children is larger than the root, swap the largest child with the root
    - recursively heapify the affected subtree to maintain the heap property
4. Repeat until the entire array is sorted

## Heap Representation
- heap sort **does not** explicitly use a tree node structure like a binary tree with nodes
- instead, it leverages the array based implementation of a binary heap
- this makes the implementation simpler and more memory efficient

*The parent-child relationship is derived from array indices:*
- For a node at index `i`:
    - **Left child**: `2 * i + 1`
    - **Right child**: `2 * i + 2`
    - **Parent**: `(i - 1) / 2`

## Implementation

```cpp
void heapify(vector<int>& arr, int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // Left child
    int right = 2 * i + 2; // Right child

    // If the left child is larger than the root
    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If the right child is larger than the largest so far
    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If the largest is not the root, swap and continue heapifying
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Build a max-heap
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // Extract elements from the heap one by one
    for (int i = n - 1; i > 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // Call heapify on the reduced heap
        heapify(arr, i, 0);
    }
}
```