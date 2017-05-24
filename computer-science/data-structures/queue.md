Big O efficiency:

- Access: O(n)
- Search: O(n)
- Insert: O(1) at end
- Delete: O(1) at begin

A queue is a data structure that is best described as "first in, first out". A real world example of a queue is people waiting in line at the bank. As each person enters the bank, he or she is "enqueued" at the back of the line. When a teller becomes available, they are "dequeued" at the front of the line. 

Perhaps the most common use of a queue within a topcoder problem is to implement a Breadth First Search (BFS). BFS means to first explore all states that can be reached in one step, then all states that can be reached in two steps, etc. A queue assists in implementing this solution because it stores a list of all state spaces that have been visited. 

A common type of problem might be the shortest path through a maze. Starting with the point of origin, determine all possible locations that can be reached in a single step, and add them to the queue. Then, dequeue a position, and find all locations that can be reached in one more step, and enqueue those new positions. Continue this process until either a path is found, or the queue is empty (in which case there is no path). Whenever a "shortest path" or "least number of moves" is requested, there is a good chance that a BFS, using a queue, will lead to a successful solution. 

Most standard libraries, such the Java API, and the .NET framework, provide a Queue class that provides these two basic interfaces for adding and removing items from a queue (enqueue and dequeue).

BFS type problems appear frequently on challenges; on some problems, successful identification of BFS is simple and immediately, other times it is not so obvious.

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

/**
 * Next, we're going to build a queue which is complementary to stacks. The
 * difference is that this time you remove items from the start of the queue
 * rather than the end. Removing the oldest items rather than the most recent.
 *
 * Again, because this limits the amount of functionality, there are many
 * different ways of implementing it. A good way might be to use a linked list
 * which we will see later.
 */

class Queue {

  /**
   * Again, our queue is using a JavaScript array as a list rather than memory.
   */

  constructor() {
    this.list = [];
    this.length = 0;
  }

  /**
   * Similar to stacks we're going to define two functions for adding and
   * removing items from the queue. The first is "enqueue".
   *
   * This will push values to the end of the list.
   */

  enqueue(value) {
    this.length++;
    this.list.push(value);
  }

  /**
   * Next is "dequeue", instead of removing the item from the end of the list,
   * we're going to remove it from the start.
   */

  dequeue() {
    // Don't do anything if we don't have any items.
    if (this.length === 0) return;

    // Shift the first item off the start of the list and return the value.
    this.length--;
    return this.list.shift();
  }

  /**
   * Same as stacks we're going to define a "peek" function for getting the next
   * value without removing it from the queue.
   */

  peek() {
    return this.list[0];
  }
  
  isEmpty() {
    return this.length === 0;
  }
}
```

This is an implementation with linked list.

```javascript

/**
 * Next, we're going to build a queue which is complementary to stacks. The
 * difference is that this time you remove items from the start of the queue
 * rather than the end. Removing the oldest items rather than the most recent.
 *
 * Again, because this limits the amount of functionality, there are many
 * different ways of implementing it. A good way might be to use a linked list
 * which we will see later.
 */

class Queue {

  constructor() {
    this.head = null;
    this.last = null;
    this.length = 0;
  }

  enqueue(value) {
    this.length++;
    const t = { value, next: null }
    
    if(this.head === null) {
      this.head = t;
      this.last = this.head;
    } else {
      this.last.next = t;
      this.last = t;
    }
  }

  dequeue() {
    if (this.length === 0) return;

    this.length--;
    const t = this.head;
    this.head = this.head.next;
    if(length === 0) this.last = null;
    return t;
  }

  peek() {
    return this.head;
  }
}
```

*Priority Queues*
In a typical breadth first search (BFS) algorithm, a simple queue works great for keeping track of what states have been visited. Since each new state is one more operational step than the current state, adding new locations to the end of the queue is sufficient to insure that the quickest path is found first. However, the assumption here is that each operation from one state to the next is a single step. 

Let us consider another example where you are driving a car, and wish to get to your destination as quickly as possible. A typical problem statement might say that you can move one block up/down/left/right in one minute. In such a case, a simple queue-based BFS works perfectly, and is guaranteed to provide a correct result. 

But what happens if we say that the car can move forward one block in two minute, but requires three minutes to make a turn and then move one block (in a direction different from how the car was originally facing)? Depending on what type of move operation we attempt, a new state is not simply one "step" from the current state, and the "in order" nature of a simple queue is lost. 

This is where priority queues come in. Simply put, a priority queue accepts states, and internally stores them in a method such that it can quickly pull out the state that has the least cost. (Since, by the nature of a "shortest time/path" type of problem, we always want to explore the states of least cost first.) 

A real world example of a priority queue might be waiting to board an airplane. Individuals arriving at their gate earlier will tend to sit closest to the door, so that they can get in line as soon as they are called. However, those individuals with a "gold card", or who travel first class, will always be called first, regardless of when they actually arrived. 

One very simple implementation of a priority queue is just an array that searches (one by one) for the lowest cost state contained within, and appends new elements to the end. Such an implementation has a trivial time-complexity for insertions, but is painfully slow to pull objects out again. 

A special type of binary tree called a heap is typically used for priority queues. In a heap, the root node is always less than (or greater than, depending on how your value of "priority" is implemented) either of its children. Furthermore, this tree is a "complete tree" from the left. A very simple definition of a complete tree is one where no branch is n + 1 levels deep until all other branches are n levels deep. Furthermore, it is always the leftmost node(s) that are filled first. 

To extract a value from a heap, the root node (with the lowest cost or highest priority) is pulled. The deepest, rightmost leaf then becomes the new root node. If the new root node is larger than at at least one of its children, then the root is swapped with its smallest child, in order to maintain the property that the root is always less than its children. This continues downward as far as necessary. Adding a value to the heap is the reverse. The new value is added as the next leaf, and swapped upward as many times as necessary to maintain the heap property. 

A convenient property of trees that are complete from the left is that they can be stored very efficiently in a flat array. In general, element 0 of the array is the root, and elements 2k + 1 and 2k + 2 are the children of element k. The effect here is that adding the next leaf simply means appending to the array. 

Questions:
1. What are some options for implementing a priority queue? (http://www.geeksforgeeks.org/priority-queue-set-1-introduction/)
2. Implement a queue using two stacks
3. http://www.geeksforgeeks.org/deque-set-1-introduction-applications/
