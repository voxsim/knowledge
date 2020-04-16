# Coding Patterns
1. Sliding Window
2. Two Pointers
3. Fast & Slow pointers
4. Merge Intervals
5. Cyclic Sort
6. In-place Reversal of a LinkedList
7. Tree Breadth First Search
8. Tree Depth First Search
9. Two Heaps
10. Subsets
11. Modified Binary Search
12. Bitwise XOR
13. Top 'K' Elements
14. K-way merge
15. 0/1 Knapsack (Dynamic Programming)
16. Topological Sort (Graph)

## Sliding Window
In many problems dealing with an array (or a LinkedList), we are asked to find or calculate something among all the contiguous subarrays (or sublists) of a given size.
For example:

```
Given an array, find the average of all contiguous subarrays of size ‘K’ in it.
```

And in this situation *Sliding Window* approach can help.

## Two Pointers
In problems where we deal with sorted arrays (or LinkedLists) and need to find a set of elements that fulfill certain constraints, the Two Pointers approach becomes quite useful. The set of elements could be a pair, a triplet or even a subarray. For example, take a look at the following problem:

```
Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.
```

It is also useful in case we need to find unique subset of elements or contiguous subarray.
In case we need to find unique subset we can sort the array, while for contiguous subarray we can start the two pointer from 0 (while in a normal case the left is from the end of the array).

## Fast & Slow pointers
The Fast & Slow pointer approach, also known as the Hare & Tortoise algorithm, is a pointer algorithm that uses two pointers which move through the array (or sequence/LinkedList) at different speeds. This approach is quite useful when dealing with cyclic LinkedLists or arrays.

By moving at different speeds (say, in a cyclic LinkedList), the algorithm proves that the two pointers are bound to meet. The fast pointer should catch the slow pointer once both the pointers are in a cyclic loop.


## Merge Interval
This pattern describes an efficient technique to deal with overlapping intervals. In a lot of problems involving intervals, we either need to find overlapping intervals or merge intervals if they overlap.


## Cyclic sort
This pattern describes an interesting approach to deal with problems involving arrays containing numbers in a given range. For example, take the following problem:

```
You are given an unsorted array containing numbers taken from the range 1 to ‘n’. The array can have duplicates, which means that some numbers will be missing. Find all the missing numbers.
```

To efficiently solve this problem, we can use the fact that the input array contains numbers in the range of 1 to ‘n’. For example, to efficiently sort the array, we can try placing each number in its correct place, i.e., placing ‘1’ at index ‘0’, placing ‘2’ at index ‘1’, and so on. Once we are done with the sorting, we can iterate the array to find all indices that are missing the correct numbers. These will be our required numbers.
