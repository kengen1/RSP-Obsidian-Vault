# Common Interview Questions: Arrays and Strings

## Key Concepts:
1. **Array Basics**: Arrays are fixed in size, with each element stored contiguously in memory. Access time is constant *O(1)* due to the direct index-based access
	- **Tags**: #vector_amortized_time 
2. **String Basics**: Strings in many languages are immutable, meaning each modification creates a new string
    - This impacts performance in scenarios with repeated modifications, like concatenation
    - Using a structure like `std:stringstream`(in C++) or `StringBuilder`(in Java) can optimize such cases by managing a dynamic array of characters

## Common Interview Questions:

### 1. Is Unique
- **Problem**: Determine if a string has all unique characters
- **Solutions**: 
    - Use a Boolean array to mark characters you've seen before, which allows for *O(n)* time and *O(1)* space (assuming ASCII characters)
    - A hashmap (`std::unordered_map`) can store each character as a key and track its occurrences. *O(n)* for time complexity but can varying in space complexity based on hashmap implementation, averaging at *O(n)*
    - Use a bit vector if character set size allows it, or compare every character to every other character *O(n^2)* time if no additional data structures are allowed

### 2. Check Permutation
- **Problem**: Check if one string is a permutation of another
- **Solutions**:
    - Sort both strings and compare them (time complexity *O(n log n)*)
    - Count character occurrences in both strings, ensuring they match (time complexity *O(n)*)

### 3. URLify
- **Problem**: Replace spaces in a string with `%20`. Assume the string has enough space at the end for additional characters
- **Solution**: Start from the end of the string and move backwards, replacing spaces as you encounter them. This approach avoids overwriting characters

### 4. Palindrome Permutation
- **Problem**: Check if a string is a permutation of a palindrome 
- **Solution**: Count character frequencies. For a palindrome permutation, no more than one character should have an off frequency count

### 5. One Away
- **Problem**: Determine if two strings are one edit (insert, remove, or replace a character) away
- **Solution**: Compare lengths first, if the lengths differ by more than 1, return false. Use pointer-based checks to identify single edits

### 6. String Compression
- **Problem**: Compress strings by replacing consecutive characters with their count (e.g., "aabcccccaaa" becomes "a2b1c5a3")
- **Solution**: Traverse the string, count consecutive characters, and build a compressed string. Only return the compressed string if it's shorter than the original

### 7. Rotate Matrix 
- **Problem**: Rotate an `N x N` matrix by 90 degrees
- **Solution** Rotate each layer of the matrix from outermost to innermost by moving elements in groups of four

### 8. Zero Matrix
- **Problem**: If an element in an `M x M` matrix is 0, its entire row and column are set to 0
- **Solution**: Use flags; use the first row and column as markers to identify rows and columns that should be zeroed, then update the matrix accordingly, finally zeroing the first row and column if needed

### 9. String Rotation
- **Problem**: Check if one string is a rotation of another (e.g., "waterbottle" is a rotation of "erbottlewat") using only one call to a substring check function
- **Solution**: Concatenate the original string to itself and check if the second string is a substring of this new string

## Additional Tips
- **Use Bit Manipulation**: In questions where you only have lowercase letters, use bitwise operators to track occurrences efficiently
- **Amortized Analysis for Dynamic Arrays**: Dynamic arrays like `vectors` double in size when full, resulting in amortized time *O(1)* insertion time 
- **Optimization with StringBuilder**: When concatenating strings, use `std::stringstream` to avoid *O(n^2)* time complexity due to repeated allocations 