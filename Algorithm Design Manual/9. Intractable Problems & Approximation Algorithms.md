#ADM 
## Problems and Reductions

**Reductions**: A fundamental technique in theoretical computer science for proving problem complexity
- involves transforming one problem into another, helping establish if a problem is as difficult as another (i.e. establishing relationships between problem complexities)
- useful for demonstrating that if a problem is solved efficiently, similar problems may also benefit from the same algorithmic solution

**Polynomial-Time Reduction**: If a problem *A* can be reduced to another problem *B* in polynomial time, solving *B* efficiently implies that *A* can also be solved efficiently 
**Example**: Reducing the *Traveling Salesman Problem** (TSP) to a different NP-Hard problem helps demonstrate the difficulty of TSP and similar optimization problems

*Q: why do we need to demonstrate the difficulty of a problem when we can just solve it*
- Demonstrating a problem's difficulty helps identify if an exact solution is feasible with current algorithms and resources
- Some problems, like TSP, are so computationally complex (requiring exponential time) that no efficient algorithm exists for solving large instances exactly
- Recognizing this complexity enables us to focus on alternative approaches, like approximation algorithms, instead of seeking exact solutions that may be impractical

## NP-Completeness
- A core concept that categorizes problems based on their solvability within polynomial time

### P vs. NP
- **P** (Polynomial Time): Problems that can be solved quickly
    - Q: what is defined as "quickly"?
        - denoted as `O(n^k)` for some constant k, where n is the input size
        - polynomial time implies a manageable growth rate, making the solution feasible for large inputs

- **NP** (Nondeterministic Polynomial Time): Problems where a proposed solution can be verified quickly 
    - *Example*: the subset-sum problem, where given a set of numbers, the goal is to determine if a subset exists that sums to a target value. Given a proposed subset, we can quickly verify if the numbers in it add up to the target, but finding that subset initially can be challenging.

- **P = NP ?**: A fundamental question in computer science asking if every problem that can be verified in polynomial time (NP) can also be solved in polynomial time *(P)*
    - P = NP would mean that any problem whose solution can be verified quickly can also be solved quickly. 
    - Currently, we know how to verify solutions to NP problems in polynomial time, but we don’t know if they can always be solved in polynomial time. 
    - This distinction is why we don’t assume that every NP problem can be solved as efficiently as it can be verified.

### NP-Complete Problems
Defined by two properties:
1. **In NP**: Solutions can be verified in polynomial time
2. **NP-Hard**: As hard as any problem in NP; any NP problem can be reduced to it
    - Q: simple example to illustrate the point

- Cook's Theorem: Proves that **Boolean Satisfiability** (SAT) is NP-Complete, establishing a foundation for demonstrating NP-completeness in other problems

### NP-Hard vs. NP-Complete
- **NP-Hard**: Problems that are at least as hard as NP problems but not necessarily in NP
    - The traveling salesman problem (TSP) is NP-complete. 
    - We can verify the length of a proposed path in polynomial time, and any NP problem can be transformed to TSP. 
    - Hence, if we had an efficient solution for TSP, we could solve any NP problem efficiently.

- **NP-Complete**: Problems in NP and NP-Hard, meaning they are among the most challenging problems 

### Common NP-Complete Problems:
- **Traveling Salesman Problem** (TSP): Finding the shortest possible route visiting each city exactly once
    - TSP is NP-complete because, given a route, we can verify the total distance quickly (in polynomial time), and any NP problem can be transformed into an instance of TSP.
- **Knapsack Problem**: Selecting items with maximum value without exceeding weight capacity
    - In the knapsack problem, we can quickly verify if a subset of items meets a weight limit while maximizing value, and any NP problem can be reduced to an instance of the knapsack problem, making it NP-complete.
- **Graph Colouring**: Assigning colours to graph vertices so no two adjacent vertices share the same colour using the minimum number of colours
    - Graph coloring is NP-complete because we can verify a coloring assignment in polynomial time, and other NP problems can be reduced to a graph coloring instance, meaning it’s as hard as any problem in NP

## Strategies for Tackling NP-Complete Problems 

### 1. Approximation Algorithms 
- Aim to produce solutions close to optimal, often within a defined approximation ratio (e.g., achieving 90% of the optimal solution)
- **Use Case**: Problems where an exact solution is impractical due to high computational complexity
- **Example**: For problems like TSP with many cities, finding an exact solution would take exponential time, which is unmanageable. Approximation algorithms offer near-optimal solutions within a fraction of the time, making them practical for large instances.

### 2. Heuristics
- Provide a quick way to find solutions without guaranteed optimality, often sufficient in practice
- **Examples**: Greedy algorithms, genetic algorithms, simulated annealing
- **Use Case**: Large of complex problems where even approximate solutions are difficult, and where a "good enough" solution is acceptable 

### 3. Average-Case Algorithms
- Aim for efficiency on typical cases rather than worst-case scenario
- Offers practical performance for many real-world cases

## Approximation Algorithms
- **Purpose**: Approximation algorithms find near-optimal solutions for problems that are computationally infeasible to solve exactly within polynomial time
- **Approximation Guarantee**:
    - Provides a performance guarantee, such as an approximation ratio, that measure how close the solution is to the optimum 
    - **Example**: An approximation algorithm within 2-approximations for TSP provides a solution no more than twice the length of the shortest possible route 
        - Q: does that mean that by 2 approximations, it could provide something that is 200% longer than the optimal path?
- **Examples of Approximation Algorithms**:
    - **Greedy Algorithms**: Use a locally optimal choice at each step to reach a solution. Common in problems like the Set Cover and Knapsack Problem
    - **Polynomial-Time Approximation Schemes (PTAS)**: Allows for tunable approximation ratio but with polynomial runtime in terms of input size for each fixed ratio


## Satisfiability (SAT): 
- A fundamental NP-complete problem that asks if there exists an assignment of true/false values to variables such that a Boolean formula is satisfied.
- **3-SAT**: A specific form of SAT where each clause has exactly three literals (e.g., (A OR NOT B OR C)), and the goal is to determine if there is an assignment that makes the formula true.
- **Importance**: Cook's Theorem established that SAT is NP-complete, and 3-SAT is often used to prove NP-completeness for other problems by reduction, as 3-SAT remains NP-complete but is easier to reduce to other problems due to its constraints on clause length.

---

**Simplified Explanation**:

SAT asks if there’s a way to assign true or false to a set of variables so that a logical formula works out to be true.

### Example:
Imagine you have three light switches (A, B, and C), each of which can be either ON (true) or OFF (false). Your goal is to find a combination of ON/OFF positions that lights up a specific bulb. The conditions for lighting up the bulb might look like this:

`(A OR NOT B OR C) AND (A OR B OR NOT C)`

This expression is in **3-SAT** form because each clause (group inside parentheses) has exactly three conditions (literals). You need to figure out if there’s a way to set A, B, and C (ON/OFF) so that this entire expression is true. If there is, then the bulb lights up, meaning the formula is "satisfiable."

In real terms, SAT problems help us solve complex, real-world issues by figuring out if certain requirements can be met simultaneously, like scheduling tasks or planning routes, but are challenging to solve for large inputs.


## Take-Home Lessons
1. Approximation Over Exact Solutions:
    - Approximation algorithms offer a practical alternative for NP-complete problems, balancing computational infeasibility with acceptance solution quality

2. Heuristics Can Be Effective:
    - Heuristics are valuable in large-scale or real-time applications where quick solutions are needed
    - Although they lack the regorous guarantees of approximation algorithms, they often perform well in practice

3. Algorithm Selection Based on Context:
    - Selecting between approximation, heuristics, or other strategies depends on problem constraints, required accuracy, and available computational resources 
