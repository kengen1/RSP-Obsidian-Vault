# Chapter 2 : Algorithm Analysis

### RAM Model of Computation

* stands for **Random Access Machine**
* the RAM model assumes every basic operation (addition, multiplication, comparisons) takes **constant time**
* memory access takes constant time, regardless of where data is located
* while this model simplifies assumptions, it provides a practical abstraction to predict algorithm performance accurately

### Big O Notation

* **Big O**: Describes the upper bound of an algorithm growth rate
  * it reflects the worst-case performance
  * it ignores constant factors and lower-order terms
* **Ω (Omega)**: Represents the lower bound of performance
* **Θ (Theta)** : Describes tight bounds, where an algorithm performs within a narrow range of efficiency for all inputs

### Types of Algorithm Analysis

* Best Case Complexity

  * The minimum time required for an algorithm
  * e.g. if the first element is the target in a search
* Worst Case Complexity

  * The maximum number of steps an algorithm might take
  * Acts as a guarantee on performance
* Average Case Complexity

  * Expected time over all possible inputs
  * Often harder to compute accurately

### Growth Rates and Dominance Relations

* The efficiency of algorithms depends heavily on growth rates
* Growth rates refer to how quickly the runtime or resource usage of an algorithm increases with the size of an input
* Dominance relations help us compare two algorithms and predict which will perform better as the input size grows

#### Common Types of Growth Rates


| **Order**        | **Big O Notation** | **Meaning**                              | **Example**                      |
| ------------------ | -------------------- | ------------------------------------------ | ---------------------------------- |
| Constant Time    | O(1)               | Time is independent of input size        | Accessing an element in an array |
| Logarithmic Time | O(log n)           | Time grows slowly as input size doubles  | Binary search                    |
| Linear Time      | O(n)               | Time grows directly with input size      | Iterating through an array       |
| Log-Linear Time  | O(n log n)         | Common in sorting, faster than quadratic | Merge sort, Heap sort            |
| Quadratic Time   | O(n²)             | Time grows with the square of input size | Bubble sort with nested loops    |
| Exponential Time | O(2ⁿ)             | Time doubles for each additional input   | Recursive Fibonacci sequence     |
| Factorial Time   | O(n!)              | Time grows dramatically with input size  | Traveling Salesman Problem       |

#### Growth Rates Measured in Nanoseconds


| n             | lg n      | n        | n lg n    | n²        | 2ⁿ        | n!                |
| --------------- | ----------- | ---------- | ----------- | ------------ | ------------ | ------------------- |
| 10            | 0.003 μs | 0.01 μs | 0.033 μs | 0.1 μs    | 1 μs      | 3.63 ms           |
| 20            | 0.004 μs | 0.02 μs | 0.086 μs | 0.4 μs    | 1 ms       | 77.1 years        |
| 30            | 0.005 μs | 0.03 μs | 0.147 μs | 0.9 μs    | 1 sec      | 8.4 × 10¹⁵ yrs |
| 40            | 0.005 μs | 0.04 μs | 0.213 μs | 1.6 μs    | 18.3 min   | -                 |
| 50            | 0.006 μs | 0.05 μs | 0.282 μs | 2.5 μs    | 13 days    | -                 |
| 100           | 0.007 μs | 0.1 μs  | 0.644 μs | 10 μs     | 10³² yrs | -                 |
| 1,000         | 0.010 μs | 1.00 μs | 9.66 μs  | 1 ms       | -          | -                 |
| 10,000        | 0.013 μs | 10 μs   | 130 μs   | 100 ms     | -          | -                 |
| 100,000       | 0.017 μs | 0.10 ms  | 1.67 ms   | 10 sec     | -          | -                 |
| 1,000,000     | 0.020 μs | 1 ms     | 19.93 ms  | 16.7 min   | -          | -                 |
| 10,000,000    | 0.023 μs | 10 ms    | 0.23 sec  | 11.6 days  | -          | -                 |
| 100,000,000   | 0.027 μs | 0.10 sec | 2.66 sec  | 115.7 days | -          | -                 |
| 1,000,000,000 | 0.030 μs | 1 sec    | 29.90 sec | 31.7 years | -          | -                 |

#### Dominance Relations for Common Growth Rates

**#### Dominance Relations for Common Growth Rates**

n! ≫ 2ⁿ ≫ n³ ≫ n² ≫ n log n ≫ n ≫ log n ≫ 

$$
n! \gg 2^n \gg n^3 \gg n^2 \gg n \log n \gg n \gg \log n \gg 1

$$


### Take-Home Lessons

- Big O notation simplifies analysis
  - it provides a way to ignore constant factors and focus on how algorithms scale


- Worst-case analysis is crucial
  - while best-case scenarios are ideal, real-world usage demands reliability even in unfavorable cases


- dominance relations
  - algorithms with lower growth rates dominate those with higher rates as input size grows


- trade-offs in algorithm choice
  - some algorithms with better growth rate might have more implementation complexity
  - choosing the right algorithm involves balancing complexity and efficiency
