# Quickselect Algorithm

![quick select algorithm visualization](https://upload.wikimedia.org/wikipedia/commons/0/04/Selecting_quickselect_frames.gif)

## 1. Overview

- **Purpose**: Find the **k-th smallest (or largest) element** in an unsorted array
- **Approach**: Uses a partition-based selection method similar to Quicksort, where elements are arranged relative to a pivot

- **Applications**:
    - Finding Median: Find the middle value in an unsorted array
    - Top-K Elements: Retrieve the largest or smallest `k` elements without sorting the entire array

## 2. Algorithm Steps
1. Choose a Pivot: Select a pivot element (commonly the last element on a random element)
2. Partition:
    - Partition the array around the pivot, so that all elements smaller than the pivot are on the left and all elements greater are on the right
    - After partitioning, the **pivot** element is in its final position in a sorted array
3. Recursive Selection:
    - Check the pivot's position (`pivotIndex`) relative to `k`
        - If `pivotIndex == k`, return the pivot as the k-th smallest element
        - If `pivotIndex > k`, recursively apply Quickselect on the left subarray
        - If `pivotIndex < k`, recursively apply Quickselect on the right subarray

## 3. Implementation

```cpp
int partition(vector<int>& arr, int left, int right) {
    int pivot = arr[right];
    int i = left - 1;

    for (int j = left; j < right; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[right]);
    return i + 1;
}

int quickSelect(vector<int>& arr, int left, int right, int k) {
    if (left <= right) {
        int pivotIndex = partition(arr, left, right);

        if (pivotIndex == k) {
            return arr[pivotIndex];
        } else if (pivotIndex > k) {
            return quickSelect(arr, left, pivotIndex - 1, k);
        } else {
            return quickSelect(arr, pivotIndex + 1, right, k);
        }
    }
    return -1;
}
```

## 4. Time Complexity

| Operation   | Average Time Complexity | Worst-Case Time Complexity |
| ------------- | ------------------------- | ---------------------------- |
| Quickselect | O(n)                    | O(n²)                    |

- The **average case** is O(n) due to the efficient partitioning that focuses only on one side of the array
- The **worst case** is O(n²) which occurs if the pivot selections are poor and the array is not divided efficiently (e.g., already sorted or highly unbalanced)

## 5. Example Usage
Problem: Find the 3rd smallest element in the array `[10, 4, 5, 8, 6, 11, 26]`

1. Initial Array: `[10, 4, 5, 8, 6, 11, 26]`
2. Set `k = 2` (since we’re using zero-based indexing).
3. The 3rd smallest element is 6