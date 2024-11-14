# Recursion and Dynamic Programming

Recursion:
- a good hint that a problem is recursive is that it can be built off of subproblems
- most recursive problems follow similar patterns
- *"Design an algorithm to compute the nth..."*
- *"Write code to list the first n..."*
- *"Implement a method to compute all"*

- recursive algorithms are often memory efficient where each call adds a new layer to the call stack (O(n) for a stack depth of N)
- before diving into a recursive solution, ask how hard it would be to implement iteratively, and discuss the tradeoffs with your interviewer


Common ways of dividing problems into subproblems:
- bottom-up: start by solving for the simplest case and using each solved case to build up to the next
- top-down: breaks down the problem into smaller subproblems, solving each as needed and reusing solutions to avoid redundant work
- half-and-half: dividing the dataset in half (e.g. binary search, merge sort)


---
Dynamic Programming:

- dynamic programming in its simplified form is *taking a recursive algorithm and finding the overlapping subproblems* where these repeate results are cached for future recursive calls
- you can substitute the recursive nature of the algorithm for something iterative, so long as previous work is "cached"
- drawing recursive calls as a tree is a great way to figure out the runtime of a recursive algorithm 
