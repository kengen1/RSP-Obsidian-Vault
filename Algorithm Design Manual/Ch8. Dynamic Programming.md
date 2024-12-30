#ADM #Dynamic-Programming 

- Dynamic Programming (DP) is a fundamental optimization technique
- It leverages a trade-off between computation and memory
- DP optimizes algorithms by systematically storing and reusing the results of subproblems, avoiding redundant computations
- DP is particularly useful for problems with overlapping subproblems and optimal substructure

## Key Concepts

### 1. Memorization / Caching
- Memorization stores the results of expensive function calls and reuses them when identical calls are encountered.
- Avoids recalculating the same subproblems repeatedly
- **Memory Usage in Dynamic Programming**: 
    - We can generally store results in **arrays, tables or dictionaries** to cache solutions of subproblems
    - The amount of memory needed depends on the number of subproblems and the complexity of each subproblem result

### 2. Bottom-Up Approach
- Iteratively builds up a solution starting from the base case
- Avoids the need for recursion
    - In recursive DP, each recursive call stores its state on the call stack, which can lead to stack overflow for deep recursion
    - Bottom-up approach computes values in a structured loop or sequence
    - Good for problems that require large numbers of recursive calls
- Reduces stack usage and can improve efficiency in iterative DP implementations

### 3. Optimal Substructure
- DP relies on problems where an optimal solution can be constructed from optimal solutions for overlapping subproblems
- This characteristic ensures that subproblem solutions combine correctly to form the main solution 
    
### 4. Overlapping Subproblems
- Overlapping subproblems refers to the property that subproblems recur within the main problem's solution process
- DP applies when subproblems recur within the solution process
- This property allows the algorithm to save and reuse results, significantly reducing computational time
---

## Structure of a Dynamic Programming Solution

1. **Define Subproblems**: Break down the main problem into smaller, manageable subproblems that collectively build toward the overall solution

2. **Formulate Recurrence Relation**: Establish how each subproblem relates to its smaller subproblems

3. **Set Up Base Cases**: Define initial values for the simplest subproblems to anchor the recurrence relation

4. **Choose Memorization or Bottom-up Approach**:
- **Memorization**: Store and reuse subproblem solutions as they are computed
- **Bottom-Up**: Build up from base cases to the final solution iteratively, avoiding recursive overhead

## Example Dynamic Programming Problems

### 1. Fibonacci Numbers

- **Problem**: Compute the *n*th Fibonacci number

- **Approach**: Use memorization or a bottom-up approach to store previous Fibonacci numbers and use them to compute subsequent numbers

- **Time Complexity**: *O(n)*, as each Fibonacci number is computed once

---

### 2. Longest Common Subsequence (LCS)

- **Problem**: Given two sequences, find the lengthof their longest subsequence that appears in both sequences

- **Approach**: Define a 2D table to store results of subproblems and solve iteratively or recursively with memorization

- **Time Complexity**: *O(m x n)* , where *m* and *n* are the lengths of the two sequences

---

### 3. Knapsack Problem

- **Problem**: Given a set of items with weights and values, maximize the value that fits within a weight limit

- **Approach**: Use a table to store maximum values achievable for each weight limit, considering each item's inclusion or exclusino

- Time Complexity: 𝑂(𝑛 × 𝑊), where 𝑛 is the number of items and 𝑊 is the knapsack’s weight capacity.

---

## Take Home Lessons
- **Memorisation Optimizes Recursion**: By storing and reusing subproblem results, memorisation significantly reduces the computation for problems with overlapping subproblems
- **Iterative DP Minimizes Overhead**: A bottom-up, iterative approach often reduces the call stack usage and memory overhead, making it preferable for certain problems
- **Ensure Optimal Substructure**: DP is effective only if the problem has an optimal substructure; that is, the overall solution can be correctly built from solutions to smaller subproblems 