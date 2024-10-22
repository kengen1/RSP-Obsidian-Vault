# Insertion Sort

## Overview
- simple algorithm that builds the sorted array one element at a time
- inserts each element into its correct position relative to the previously sorted elements
- works well for small datasets and nearly sorted arrays
- inefficient for large datasets

Time Complexity: *O(n²)*

## How it Works:
1. start with the second element (first element is considered sorted)
2. compare the current element with elements in the sorted portion
3. shift elements greater than the current element to the right
4. insert the current element into the correct position

![insertion sort animation](https://upload.wikimedia.org/wikipedia/commons/9/9c/Insertion-sort-example.gif)

## Implementation

```cpp
void insertionSort(vector<int>& nums) {
    int n = nums.size();

    for(int i = 1; i < n; i++) {
        int key = nums[i];
        int j = i -1;

        // shift elements of the sorted portion to the right
        while(j >= 0 && nums[j] > key) {
            nums[j + 1] = nums[j];
            j--;
        }
        nums[j + 1] = key;      // insert the current element into its correct position
    }
}
```