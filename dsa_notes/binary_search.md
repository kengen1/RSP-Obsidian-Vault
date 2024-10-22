# Binary Search

## Overview
- a **divide-and-conquer** algorithm that finds the position of a target element within a **sorted array**
- it works by repeatedly dividing the search interval in half
- logarithmic (*O(log n)*) in time complexity

## How it Works:
1. start with left and right pointers and the beginning and end of the array
2. find the middle element `left + (right - left) / 2` 
3. if the target is equal to the middle, return the index
4. if the target is smaller than the middle, search the left half
5. if the target is larger than the middle, search the right half
6. repeat untilt he target is found or the list is empty

*the calculation of the mid point `left + (right - left) / 2` is done so prevent **integer overflow***
    - if left and right are very large integers, their sum might exceed the maximum value an `integer` datatype can hold

## Implementation
```cpp

int binarySearch(const vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;  // Avoid overflow

        if (arr[mid] == target)
            return mid;  // Target found

        if (arr[mid] < target)
            left = mid + 1;  // Search the right half
        else
            right = mid - 1;  // Search the left half
    }

    return -1;  // Target not found
}

```