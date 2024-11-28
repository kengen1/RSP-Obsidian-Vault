#Sorting #Divide-and-Conquer 

## Overview

- *divide-and-conquer* algorithm
- best suited for large datasets where memory is not a constraint, as it requires additional space for merging

Time Complexity: *O(n log n)*

## How it Works:

1. **Divide** : Split the input array into two halves
2. **Conquer** : Recursively sort each half
3. **Merge** : Combine the two sorted halves into a single sorted array

![merge sort animation](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif?20151222172210)

## Implementation

```cpp
// Merge two sorted halves into a single sorted array
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // Temporary arrays to hold the two halves
    vector<int> leftArr(n1), rightArr(n2);

    // Copy data to temporary arrays
    for (int i = 0; i < n1; ++i)
        leftArr[i] = arr[left + i];
    for (int j = 0; j < n2; ++j)
        rightArr[j] = arr[mid + 1 + j];

    // Merge the temporary arrays back into arr
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (leftArr[i] <= rightArr[j]) {
            arr[k] = leftArr[i];
            i++;
        } else {
            arr[k] = rightArr[j];
            j++;
        }
        k++;
    }

    // Copy any remaining elements from leftArr
    while (i < n1) {
        arr[k] = leftArr[i];
        i++;
        k++;
    }

    // Copy any remaining elements from rightArr
    while (j < n2) {
        arr[k] = rightArr[j];
        j++;
        k++;
    }
}
```
```cpp
// Recursive function to implement merge sort
void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        // Sort first and second halves
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        // Merge the sorted halves
        merge(arr, left, mid, right);
    }
}

```
