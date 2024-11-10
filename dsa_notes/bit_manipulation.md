# Bit Manipulation

## 1. Overview

- Bit manipulation uses binary operations (AND, OR, XOR, NOT) directly on bits to perform tasks
- **Advantages**:

  - **Efficiency:** Faster than conventionally arithmetic operations
  - **Low Memory Usage:** Directly working with bits requires fewer resources
- **Applications**:

  - **Power of Two Checks**: Quick check if a number is a power of two
  - **Swapping Bits:** Efficient swapping of values without temporary storage
  - **Setting/Clearing/Flipping Bits:** Manipulating individual bits for control flags
  - **Optimizations:** Can be used in low-level optimizations and certain cryptographic algorithms

## 2. Bitwise Operations

| **Operation** | **Symbol** | **Description**                               | **Example**                    |
|---------------|------------|-----------------------------------------------|--------------------------------|
| AND           | `&`        | Sets each bit to 1 if both bits are 1         | `a & b`                        |
| OR            | `\|`       | Sets each bit to 1 if at least one bit is 1   | `a \| b`                       |
| XOR           | `^`        | Sets each bit to 1 if only one bit is 1       | `a ^ b`                        |
| NOT           | `~`        | Inverts all bits                              | `~a`                           |
| Left Shift    | `<<`       | Shifts bits left, filling with 0 on the right | `a << 1` (multiplies by 2)     |
| Right Shift   | `>>`       | Shifts bits right, discarding right-most bits | `a >> 1` (divides by 2)        |

## 3. Key Bit Manipulation Techniques

### Checking if a Number is Odd or Even
*if the least significant bit(rightmost bit) is `1`, then the number is odd, otherwise, its even*
```cpp
bool isOdd(int n) {
    return (n & 1) == 1;
}
```

### Checking if a Number is a Power of Two
*for numbers that are powers of two, only a single bit is set (e.g., `2=10`, `4=100`)*
*subtracting `1` flips all lower bits, so `n & (n - 1)` results in `0`*
```cpp
bool isPowerOfTwo(int n) {
    return (n > 0) && ((n & (n - 1)) == 0);
}
```

### Counting the Number of Set Bits (Hamming Weight)
*The operation checks each bit and counts those that are `1`*
```cpp
int countSetBits(int n) {
    int count = 0;
    while (n > 0) {
        count += (n & 1);
        n >>= 1;
    }
    return count;
}
```

### Swapping Two Numbers Without a Temporary Variable
*XOR operations cancel out when applied in this specific sequence, allowing swapping without extra storage*
```cpp
void swap(int &a, int &b) {
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
}
```

### Setting, Clearing and Toggling Specific Bits

#### Setting the **k-th** Bit (turn on a specific bit):
```cpp
int setBit(int n, int k) {
    return n | (1 << k);
}
```

#### Clearing the k-th Bit (turn off a specific bit):
```cpp
int clearBit(int n, int k) {
    return n & ~(1 << k);
}
```

#### Toggling the k-th Bit (flip a specific bit):
```cpp
int toggleBit(int n, int k) {
    return n ^ (1 << k);
}
```

## Advanced Applications 

#### Finding the Single Non-Repeating Element
*In an array where every element appears twice except one, find the unique element*
***Explanation***: *XORing all elements results in the unique element, as duplicate elements cancel each other out*
```cpp
int singleNonRepeating(vector<int>& nums) {
    int result = 0;
    for(int num : nums) {
        result ^= nums;
    }
    return result;
}
```

#### Finding the Missing Number
*In an array containing numbers from `0` to `n` with one missing, find the missing number*
***Explanation***: *XORing all indices and elements results in the missing number, as all pair elements cancel out*
```cpp
int missingNumber(vector<int>& nums) {
    int n = nums.size();
    int result = n;
    for(int i=0; i < n; i++) {
        result ^= i ^ nums[i];
    }
    return result;
}
```