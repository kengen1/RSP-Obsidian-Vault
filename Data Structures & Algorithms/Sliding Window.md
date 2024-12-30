
## 1. Overview

- Uses #Two-Pointers  to define a "window" over a dataset
-  Reduces complexity from O(n^2) to O(n) in many cases
- Two types:
	- Fixed-size window: Window size remains constant
	- Variable-size window: Window size adjust dynamically

* Commonly used when we need to find subarrays or substrings according to a given set of conditions


![sliding window](https://media.geeksforgeeks.org/wp-content/uploads/20240306112450/sliding-window-technique-2.webp)


## 2. Example Implementation
### Problem: Find the maximum sum of a subarray of size k

### Steps:

1. Initialize `start` pointer to 0 and `currentSum` to 0.
2. Loop through the array with the `end` pointer:
    - Add `nums[end]` to `currentSum`.
    - If window size equals k:
        - Update `maxSum`.
        - Slide the window by subtracting `nums[start]` and incrementing `start`.
3. Return the `maxSum` after processing the array.

### Code:

```cpp
int maxSumSubarray(const std::vector<int>& nums, int k) {
	int maxSum = INT_MIN;
	int currentSum = 0;
	int start = 0;

	for(int end = 0; end < nums.size(); end++){
		// add current element to the sum
		currentSum += nums[end];

		// when the window reaches size k
		if(end - start + 1 == k) {
			maxSum = max(maxSum, currentSum); // update maxSum
			currentSum -= nums[start]; // remove the first element of the window
			start++;
		}
	}
	return maxSum;
}
```
