# Stacks and Queues

## Key Concepts

1. **Stack Basics**: A stack is a LIFO (Last-In-First-Out) data structure with primary operations:
   - `push`: Adds an item to the top of the stack.
   - `pop`: Removes the item from the top of the stack.
   - `peek`: Returns the item at the top without removing it.
   - `isEmpty`: Checks if the stack is empty.
- Link to stack file 

2. **Queue Basics**: A queue is a FIFO (First-In-First-Out) data structure with primary operations:
   - `add`: Adds an item to the end of the queue.
   - `remove`: Removes the item from the front of the queue.
   - `peek`: Returns the item at the front without removing it.
   - `isEmpty`: Checks if the queue is empty.
- Link to queue file

## Common Interview Questions

### 1. Three in One
   - **Problem**: Describe how you could use a single array to implement three stacks.
   - **Solution**: Divide the array into three fixed sections, one for each stack, or dynamically allocate space within the array for each stack using flexible divisions.

### 2. Stack Min
   - **Problem**: Design a stack that supports `push`, `pop`, and `min` operations, all in `O(1)` time.
   - **Solution**: Use an additional stack to keep track of the minimum values or store the minimum value at each level of the stack.

### 3. Stack of Plates
   - **Problem**: Implement a stack that starts a new sub-stack once the previous stack reaches a certain threshold.
   - **Solution**: Create a SetOfStacks, where each sub-stack has a capacity limit, and handle `push` and `pop` across stacks. Implement `popAt(index)` to pop from a specific sub-stack.

### 4. Queue via Stacks
   - **Problem**: Implement a queue using two stacks.
   - **Solution**: Use two stacks, one for enqueueing (`stackNewest`) and another for dequeueing (`stackOldest`). Transfer elements between stacks as needed.

### 5. Sort Stack
   - **Problem**: Sort a stack such that the smallest items are on the top.
   - **Solution**: Use a temporary stack to hold elements in sorted order. Insert each item from the original stack into the correct position in the temporary stack.

### 6. Animal Shelter
   - **Problem**: Implement a system for an animal shelter that operates on a FIFO basis for dogs and cats, allowing adoption of either the oldest animal or the oldest animal of a specified type.
   - **Solution**: Use two separate queues for dogs and cats. Store timestamps to determine the oldest animal. For `dequeueAny`, compare the front of each queue and dequeue the oldest.