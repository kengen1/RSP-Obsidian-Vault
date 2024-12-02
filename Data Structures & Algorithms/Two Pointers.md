## 1. Overview

- used to iterate through an array, string or list using two distinct indices (pointers)
- commonly used to solve problems involving:
	- finding pairs, triplets, or subarrays that meet specific conditions
	- searching or sorting operations in linear time

* *Key patterns* : 
	* Opposite directions: pointers starting at both ends of the array and move towards each other
	* Same direction: pointers starts at the same position and one pointer lags behind the other

* Advantages:
	* Efficient in reducing time complexity from O(n^2) to O(n) in many cases.
	* Simplifies problems involving sorted arrays or sequences

## 2. Example Implementation
### Problem: Find two numbers in a sorted array that sum up to a target value
```cpp
std::pair<int, int> twoSum(const std::vector<int>& nums, int target) {
	int left = 0; // pointer starting at the beginning
	int right = nums.size() - 1; // pointer starting at the end

	while(left < right) {
		int currentSum = nums[left] + nums[right];

		if(currentSum == target) {
			return {nums[left], nums[right]};
		}
		else if(currentSum < target) {
			left++;
		}
		else {
			right--;
		}
	}
	return {-1,-1};
}
```

