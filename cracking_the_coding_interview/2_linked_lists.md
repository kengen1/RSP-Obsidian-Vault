# Linked Lists

## Key Concepts
- TODO: create section for "The Runner Technique"
- TODO: point to linked list file for creation of a linked list 
- TODO: point to linked list file for deletion of a node in a linked list
1. **Linked List Basics**: A linked list is a sequence of nodes where each node points to the next. Linked lists allow efficient insertion and deletion but require sequential access.
2. **Types**: Singly linked lists allow traversal in one direction, while doubly linked lists allow traversal in both directions by having pointers to both the next and previous nodes.

## Common Interview Questions

### 1. Remove Duplicates
   - **Problem**: Remove duplicates from an unsorted linked list.
   - **Solutions**:
     - **With Buffer**: Use a hash set to track seen values as you iterate through the list, removing duplicates when found. `O(N)` time and `O(N)` space.
     - **Without Buffer**: Use two pointers, one iterating over each node and another checking subsequent nodes for duplicates. `O(N^2)` time and `O(1)` space.

### 2. Return Kth to Last
   - **Problem**: Find the kth to last element in a singly linked list.
   - **Solution**: Use two pointers; move the first pointer `k` nodes ahead, then move both pointers until the first pointer reaches the end. The second pointer will now be at the kth to last element. `O(N)` time and `O(1)` space.

### 3. Delete Middle Node
   - **Problem**: Given access to a node in the middle of a singly linked list (but not the head), delete this node.
   - **Solution**: Copy data from the next node into the current node, then delete the next node. Only works if the node is not the last one.

### 4. Partition List
   - **Problem**: Partition a linked list around a value `x` so that all nodes less than `x` come before all nodes greater than or equal to `x`.
   - **Solution**: Create two separate linked lists: one for nodes less than `x` and one for nodes greater than or equal to `x`. Append the "greater" list to the "less" list. `O(N)` time.

### 5. Sum Lists
   - **Problem**: Given two linked lists representing numbers (digits stored in reverse order), add them and return the sum as a linked list.
   - **Solution**: Traverse both lists, adding corresponding digits and tracking carry. Treat missing nodes as 0 for unequal lengths. `O(N)` time.

### 6. Palindrome Check
   - **Problem**: Determine if a linked list is a palindrome.
   - **Solutions**:
     - **Reverse and Compare**: Reverse the linked list and compare with the original. `O(N)` time and space.
     - **Stack-based**: Use a fast and slow pointer; push the first half onto a stack, then compare with the second half. `O(N)` time and `O(N)` space.

### 7. Intersection
   - **Problem**: Determine if two singly linked lists intersect and return the intersecting node.
   - **Solution**: Get both list lengths, align their starts, and traverse until nodes match. `O(N)` time.

### 8. Loop Detection
   - **Problem**: Detect if a linked list has a cycle, and return the node where the cycle begins.
   - **Solution**: Use Floyd’s cycle-finding algorithm (tortoise and hare). If a cycle is detected, reset one pointer to the head, and move both pointers until they meet again; this meeting point is the start of the loop.