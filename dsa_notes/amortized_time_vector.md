# Vector Amortized Time

## 1. Overview
- **Dynamic arrays** (like `std::vector`) automatically resize when they run out of space 
- When a `vector` resizes, it typically **doubles it capacity** to accommodate more elements
- Amortized analysis helps us understand the cost of such resizing operations spread over multiple insertions
- While some individual operations are expensive, the average insertion cost is low

**What is amortized time?**: the average time per operation over a sequence of operations, taking into account occasional expensive operations that are offset by many cheap ones.

## 2. How Resizing Works in `std::vector`
- When a `vector` reaches its capacity limit:
    1. A new, larger array (usually double the previous capacity) is allocated
    2. The existing elements are copied to the new array
    3. The old array is deallocated, and new elements can be added without resizing until the capacity is reached again

**Example**
If a vector has a capacity of `4` and is full, inserting one more element will:
- Allocate a new array with a capacity of `8`
- Copy the 4 existing elements to the new array
- Insert the new element

## 3. Amortized Analysis of Insertion
When analyzing the cost of repeatedly inserting elements into a vector, let's assume we start with an empty vector and add `n` elements

1. Most Insertion (**O(1) Cost**) : *For each element that fits within the current capacity, insertion is `O(1)`
2. Costly Insertion (**O(n) Cost**) :
    - when resizing occurs, the insertion can become `O(n)` because all existing elements are copied to new array
    - however, the number of resizing operations grows **logarithmically** relative to the number of elements
3. Amortized Cost Calculation:
    - over `n` insertions, each element only requires `O(1)` cost on average due to the doubling strategy 
    - this is because each element is only copied a limited number of time (once for each capacity doubling)

Thus, the **amortized time complexity** per insertion is `O(1)`

**Example**: Logarithmic resizing

1. **Starting Conditions**:
   - Assume we start with an empty `vector` with an initial capacity of `1`.
   - Each time the vector reaches its capacity, it doubles.

2. **Insertions and Resizing**:
   - **Insert 1st element**: Capacity is `1`, no resize needed.
   - **Insert 2nd element**: Capacity reached. Resize to `2`.
   - **Insert 3rd element**: Capacity reached. Resize to `4`.
   - **Insert 5th element**: Capacity reached. Resize to `8`.
   - **Insert 9th element**: Capacity reached. Resize to `16`.
   
   Notice the pattern: resizing happens at `1, 2, 4, 8, 16...`, doubling each time.

3. **Logarithmic Growth**:
   - If we continue this pattern up to `n` elements, the **number of times we double the capacity** grows as `log(n)`.
   - For example, to reach `16` elements, we resized `4` times (logarithmic in base `2`), and to reach `32` elements, we resized `5` times.

**Key Takeaway**
- Even though we perform many insertions, we only resize about `log(n)` times for `n` elements.
- Each resize operation affects all current elements but becomes **less frequent** as the capacity grows, averaging out the cost of resizing over all insertions.