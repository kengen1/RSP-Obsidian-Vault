# Chapter 10: How to Design Algorithms

## Key Concepts

### 1. Asking the Right Questions

**Effective algorithm design begins with clear, guiding questions**;

- "What is the nature of the problem? Is it well-defined?"
- "Can the problem be simplified or broken down into smaller parts?"
- "What existing techniques might apply here?"

### 2. Problem Decomposition

- **Divide and Conquer**: Break down complex problems into smaller subproblems that are easier to solve
- **Problem Modeling**: Identify the core elements of the problem and think about how they interact
- **Focus on Constraints**: Consider specific limits or requirements that can influence the solution's design and performance

### 3. Solution Exploration

- **Heuristics**: Use experience or rules of thumb for initial exploration
- **Brute Force**: Try exhaustive methods on small data to understand limitations
- **Greedy Techniques**: Aim for locally optimal solutions as stepping stones
- **Dynamic Programming and Memorization**: Consider caching solutions to subproblems when facing overlapping subproblems

## Structure of an Algorithm Design Process

1. **Problem Understanding** : Clearly define what the problem is and what it is not. Document requirements and constraints
2. **Select and Approach**: Evaluate which algorithmic strategies (greedy, dynamic programming, backtracking, etc.) might best fit the problem
3. **Implement and Test**: Begin coding an initial version, iterating as necessary
4. **Optimize and Refine**: Seek opportunities to improve the algorithm's efficiency or scalability
5. **Analyze Complexity**: Assess the algorithm's time and space complexity, aiming for improvements where possible

## Example Techniques in Algorithm Design

### Heuristic Approach

- **Greedy Algorithms** : Make the best local choice at each step with the aim of finding a global optimum
- **Hill Climbing** : Start with a solution and iteratively improve it based on a predefined rule
- **Simulated Annealing**: Begin with a potential solution and introduce controlled random changes, gradually refining towards a better solution

### Exhaustive Approach

- Suitable for small datasets or problems where precision is more important than speed
- Backtracking and recursion are often used to explore all possibilities

### Approximation Algorithms

- For NP-Hard problems where exact solutions are impractical, approximation algorithms problem near-optimal solutions
- They can offer performance guarantees within a known ratio of the optimal solution, making them practical for large-scale problems

---

# Practical Algorithm Design Checklist

*this is the checklist taken directly from the chapter contents*

### 1. Do I really understand the problem?
   - **(a)** What exactly does the input consist of?
   - **(b)** What exactly are the desired results or output?
   - **(c)** Can I construct an input example small enough to solve by hand? What happens when I try to solve it?
   - **(d)** How important is it to my application that I always find the optimal answer? Can I settle for something close to the optimal answer?
   - **(e)** How large is a typical instance of my problem? Will I be working on 10 items? 1,000 items? 1,000,000 items?
   - **(f)** How important is speed in my application? Must the problem be solved within one second? One minute? One hour? One day?
   - **(g)** How much time and effort can I invest in implementation? Will I be limited to simple algorithms that can be coded up in a day, or do I have the freedom to experiment with a couple of approaches and see which is best?
   - **(h)** Am I trying to solve a numerical problem? A graph algorithm problem? A geometric problem? A string problem? A set problem? Which formulation seems easiest?

### 2. Can I find a simple algorithm or heuristic for my problem?
   - **(a)** Will brute force solve my problem correctly by searching through all subsets or arrangements and picking the best one?
      - **i.** If so, why am I sure that this algorithm always gives the correct answer?
      - **ii.** How do I measure the quality of a solution once I construct it?
      - **iii.** Does this simple, slow solution run in polynomial or exponential time? Is my problem small enough that this brute-force solution will suffice?
      - **iv.** Am I certain that my problem is sufficiently well-defined to actually have a correct solution?
   - **(b)** Can I solve my problem by repeatedly trying some simple rule, like picking the biggest item first? The smallest item first? A random item first?
      - **i.** If so, on what types of inputs does this heuristic work well? Do these correspond to the data that might arise in my application?
      - **ii.** On what types of inputs does this heuristic work badly? If no such examples can be found, can I show that it always works well?
      - **iii.** How fast does my heuristic come up with an answer? Does it have a simple implementation?

### 3. Is my problem in the catalog of algorithmic problems in the back of this book?
   - **(a)** What is known about the problem? Is there an implementation available that I can use?
   - **(b)** Did I look in the right place for my problem? Did I browse through all pictures? Did I look in the index under all possible keywords?
   - **(c)** Are there relevant resources available on the World Wide Web? Did I do a Google web and Google Scholar search? Did I go to the page associated with this book, http://www.cs.sunysb.edu/~algorith?

### 4. Are there special cases of the problem that I know how to solve?
   - **(a)** Can I solve the problem efficiently when I ignore some of the input parameters?
   - **(b)** Does the problem become easier to solve when I set some of the input parameters to trivial values, such as 0 or 1?
   - **(c)** Can I simplify the problem to the point where I can solve it efficiently?
   - **(d)** Why can’t this special-case algorithm be generalized to a wider class of inputs?
   - **(e)** Is my problem a special case of a more general problem in the catalog?

### 5. Which of the standard algorithm design paradigms are most relevant to my problem?
   - **(a)** Is there a set of items that can be sorted by size or some key? Does this sorted order make it easier to find the answer?
   - **(b)** Is there a way to split the problem in two smaller problems, perhaps by doing a binary search? How about partitioning the elements into big and small, or left and right? Does this suggest a divide-and-conquer algorithm?
   - **(c)** Do the input objects or desired solution have a natural left-to-right order, such as characters in a string, elements of a permutation, or leaves of a tree? Can I use dynamic programming to exploit this order?
   - **(d)** Are there certain operations being done repeatedly, such as searching, or finding the largest/smallest element? Can I use a data structure to speed up these queries? What about a dictionary/hash table or a heap/priority queue?
   - **(e)** Can I use random sampling to select which object to pick next? What about constructing many random configurations and picking the best one? Can I use some kind of directed randomness like simulated annealing to zoom in on the best solution?
   - **(f)** Can I formulate my problem as a linear program? How about an integer program?
   - **(g)** Does my problem seem something like satisfiability, the traveling salesman problem, or some other NP-complete problem? Might the problem be NP-complete and thus not have an efficient algorithm? Is it in the problem list in the back of Garey and Johnson [GJ79]?

### 6. Am I still stumped?
   - **(a)** Am I willing to spend money to hire an expert to tell me what to do? If so, check out the professional consulting services mentioned in Section 19.4 (page 664).
   - **(b)** Why don’t I go back to the beginning and work through these questions again? Did any of my answers change during my latest trip through the list?
