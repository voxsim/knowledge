## Data Structure Basics

###**Array**
####Definition:
- Stores data elements based on an sequential, most commonly 0 based, index.
- Based on tuples from set theory.
- They are one of the oldest, most commonly used data structures.

####What you need to know:
- Optimal for indexing; bad at searching, inserting, and deleting (except at the end).
- **Linear arrays**, or one dimensional arrays, are the most basic.
  - Are static in size, meaning that they are declared with a fixed size.
- **Dynamic arrays** are like one dimensional arrays, but have reserved space for additional elements.
  - If a dynamic array is full, it copies it's contents to a larger array.
- **Two dimensional arrays** have x and y indices like a grid or nested arrays.

####Big O efficiency:
- Indexing:         Linear array: O(1),      Dynamic array: O(1)
- Search:           Linear array: O(n),      Dynamic array: O(n)
- Optimized Search: Linear array: O(log n),  Dynamic array: O(log n)
- Insertion:        Linear array: n/a        Dynamic array: O(n)

###**Linked List**
####Definition: 
- Stores data with **nodes** that point to other nodes.
  - Nodes, at its most basic it has one datum and one reference (another node).
  - A linked list _chains_ nodes together by pointing one node's reference towards another node.

####What you need to know:
- Designed to optimize insertion and deletion, slow at indexing and searching.
- **Doubly linked list** has nodes that reference the previous node.
- **Circularly linked list** is simple linked list whose **tail**, the last node, references the **head**, the first node.
- **Stack**, commonly implemented with linked lists but can be made from arrays too.
  - Stacks are **last in, first out** (LIFO) data structures.
  - Made with a linked list by having the head be the only place for insertion and removal.
- **Queues**, too can be implemented with a linked list or an array.
  - Queues are a **first in, first out** (FIFO) data structure.
  - Made with a doubly linked list that only removes from head and adds to tail.

####Big O efficiency:
- Indexing:         Linked Lists: O(n)
- Search:           Linked Lists: O(n)
- Optimized Search: Linked Lists: O(n)
- Insertion:        Linked Lists: O(1)

###**Hash Table or Hash Map**
####Definition: 
- Stores data with key value pairs.
- **Hash functions** accept a key and return an output unique only to that specific key.
  - This is known as **hashing**, which is the concept that an input and an output have a one-to-one correspondence to map information.
  - Hash functions return a unique address in memory for that data.

####What you need to know:
- Designed to optimize searching, insertion, and deletion.
- **Hash collisions** are when a hash function returns the same output for two distinct inputs.
  - All hash functions have this problem.
  - This is often accommodated for by having the hash tables be very large.
- Hashes are important for associative arrays and database indexing.

####Big O efficiency:
- Indexing:         Hash Tables: O(1)
- Search:           Hash Tables: O(1)
- Insertion:        Hash Tables: O(1)

###**Binary Tree**
####Definition: 
- Is a tree like data structure where every node has at most two children.
  - There is one left and right child node.

####What you need to know:
- Designed to optimize searching and sorting.
- A **degenerate tree** is an unbalanced tree, which if entirely one-sided is a essentially a linked list.
- They are comparably simple to implement than other data structures.
- Used to make **binary search trees**.
  - A binary tree that uses comparable keys to assign which direction a child is.
  - Left child has a key smaller than it's parent node.
  - Right child has a key greater than it's parent node.
  - There can be no duplicate node.
  - Because of the above it is more likely to be used as a data structure than a binary tree.

####Big O efficiency:
- Indexing:  Binary Search Tree: O(log n)
- Search:    Binary Search Tree: O(log n)
- Insertion: Binary Search Tree: O(log n)
