Big O efficiency:

- Access: O(n)
- Search: O(n)
- Insert: O(1) at end
- Delete: O(1) at begin

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

Questions:
1. What are some options for implementing a priority queue? (http://www.geeksforgeeks.org/priority-queue-set-1-introduction/)
2. Implement a queue using two stacks
