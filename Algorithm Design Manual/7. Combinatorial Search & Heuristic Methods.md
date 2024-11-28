#ADM #Backtracking #Pruning #Heuristics

- Combinatorial Search methods like backtracking and pruning are powerful for problems requiring exhaustive search but can become computationally expensive.
- Heuristic Methods provide feasible solutions for large or complex search spaces by focusing on "good enough" solutions rather than guaranteed optimality.

## Combinatorial Search Methods
- Involves exploring a **solution space** to identify configurations that meet problem constraints or optimize certain criteria
- These methods often require **systematic exploration** of all possible solutions, making them computationally intensive but guaranteed to find optimal results if exhaustive search if feasible

### Why do we need combinatorial search?
- essential for solving problems where all possible configurations must be considered to find an optimal or valid solution
- these problems have a large solution space that cannot be navigated directly 
- combinatorial search helps us systematically explore configurations, especially for problems with strict constraints
### Key Concepts
1. **Solution Space Representation**: Represents all potential configurations for the problem
2. **Cost Function**: Evaluates each configuration's quality or suitability
3. **Search Pruning**: Reduces necessary exploration exploration by discarding configurations that cannot yield optimal solutions

## 7.1 Backtracking
Backtracking is a **systemic way to iterate through all possible configurations** of a search space. These configurations may represent:
- All possible **arrangements of objects** (permutations)
- All possible ways of building a **collection of objects** (subjects)
- **Enumerating all spanning trees** of a graph, all paths between vertices, or all ways to **partition vertices** into colour classes
### Steps:
1. **Start with an Empty or Partial Solution**: Begin with a solution that meets initial conditions but is incomplete.
2. **Extend the Solution**: Add elements to the partial solution and proceed down the search tree.
3. **Check Constraints**: If the solution violates any constraints, **backtrack** by removing the last added element.
4. **Try Alternatives**: After backtracking, attempt the next possible extension until all alternatives are explored.
5. **Complete Solution**: If a configuration meets all constraints, record or output the solution.

### Example Applications of Backtracking
- **n-Queens Problem**: Place n queens on an n × n chessboard so that no two queens threaten each other.
- **Pathfinding in Mazes**: Find all possible paths from a start point to an endpoint, backtracking when a path hits a dead end.
- **Subset Sum Problem**: Find subsets of a set that add up to a target sum by including or excluding each element.

### Pseudocode
```
function BACKTRACK(solution):
    if solution is a complete solution:
        process(solution)     # Record or output the solution
        return

    for each option in choices:
        if option is valid (does not violate constraints):
            add option to solution
            BACKTRACK(solution)    # Recursive call to extend the solution
            remove option from solution  # Undo the choice (backtrack)
```

## 7.2 Search Pruning
Search pruning enhances backtracking by **eliminating infeasible paths early**, reducing the number of configurations that need to be exploring

**Example**:
- In the Traveling Salesman Problem, if a partial path already exceeds the length of the shortest known complete path, it can be pruned

**Benefits**:
- *Efficiency*: Reduces unnecessary calculations, speeding up search time
- *Applicability*: Especially useful in optimization problems where some configurations are evidently suboptimal

## Heuristic Search Methods
- Heuristic search methods are designed to find **"good enough"** solutions for complex combinatorial problems where exhaustive search is impractical 
- Rather than systematically exploring every possibility, heuristic methods use **rules or strategies** to find reasonably optimal solutions within a feasible time frame
- Heuristic search methods prioritize efficiency over guaranteed optimality

### Random Sampling (Monte Carlo)
- **Approach** : Generates random configurations and evaluates each to find a suitable solution
- **Application** : Effective when a good solution can be found through sampling rather than exhaustive search
- **Trade-off** : May not always find the optimal solution but is fast and scalable 

### Simulated Annealing
- **Inspiration** : Modeled after the physical process of annealing, where materials are heated and slowly cooled to reach a stable state
- **Mechanism** : Evaluates neighbouring configurations and moves to a better one if available. The process repeats until until no better neighbours are found
- **Application** : Useful for problems where neighbouring configurations are computationally easy to generate and evaluate, such as optimization in scheduling or routing 

### Local Search
- **Approach** : Iteratively improves the current configuration by exploring neighbouring solutions 
- **Mechanism** : Evaluates neighbouring configurations and moves to a better one if available. The process repeats until no better neighbours are found
- **Application** : Useful for problems where neighbouring configurations are computationally easy to generate and evaluate, such as optimization in scheduling or routing 
