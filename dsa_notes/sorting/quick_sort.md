# Quick Sort

## Overview

- **divide and conquer** algorithm that selects a pivot element and partitions the array around pivot
- it recursively sorts the elements on the left and right of the pivot
- **in-place-sorting** algorithm, meaning it sorts without requiring extra memory (beyond the recursion stack)
- best used when average-case perofrmance matters

  Average Case Time Complexity : *O(n log n)*
  Worst Case Time Complexity : *O(n²)*

Note:

- quick sort is sensitive to the pivot choice
- performance can degrade to *O(n²)* if a bad pivot is consistently chosen

## How it Works:

1. Choose a pivot : select a pivot element from the array
2. Partition the array : rearrange the elements such that:
   - elements smaller than the pivot go on the left
   - elements large than the element go on the right
3. recursively sort the left and right partitions

![quick sort animation](https://www.tutorialspoint.com/data_structures_algorithms/images/quick_sort_partition_animation.gif)

## Video Explanation

<iframe width="560" height="315" src="https://www.youtube.com/embed/Vtckgz38QHs" 
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; 
clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Implementation
```cpp
// Partition function: rearranges the array around the pivot
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Select the last element as pivot
    int i = low - 1;       // Index of smaller element

    for (int j = low; j < high; ++j) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]); // Swap elements smaller than the pivot
        }
    }
    swap(arr[i + 1], arr[high]); // Place pivot in the correct position
    return i + 1;
}

// Recursive Quick Sort function
void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); // Partition index

        // Recursively sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```