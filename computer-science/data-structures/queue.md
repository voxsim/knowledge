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

From TopCoder:
A queue is a data structure that is best described as "first in, first out". A real world example of a queue is people waiting in line at the bank. As each person enters the bank, he or she is "enqueued" at the back of the line. When a teller becomes available, they are "dequeued" at the front of the line. 

Perhaps the most common use of a queue within a topcoder problem is to implement a Breadth First Search (BFS). BFS means to first explore all states that can be reached in one step, then all states that can be reached in two steps, etc. A queue assists in implementing this solution because it stores a list of all state spaces that have been visited. 

A common type of problem might be the shortest path through a maze. Starting with the point of origin, determine all possible locations that can be reached in a single step, and add them to the queue. Then, dequeue a position, and find all locations that can be reached in one more step, and enqueue those new positions. Continue this process until either a path is found, or the queue is empty (in which case there is no path). Whenever a "shortest path" or "least number of moves" is requested, there is a good chance that a BFS, using a queue, will lead to a successful solution. 

Most standard libraries, such the Java API, and the .NET framework, provide a Queue class that provides these two basic interfaces for adding and removing items from a queue. 

BFS type problems appear frequently on challenges; on some problems, successful identification of BFS is simple and immediately, other times it is not so obvious. 

A queue implementation may be as simple as an array, and a pointer to the current position within the array. For instance, if you know that you are trying to get from point A to point B on a 50×50 grid, and have determined that the direction you are facing (or any other details) are not relevant, then you know that there are no more than 2,500 "states" to visit. Thus, your queue is programmed like so:

class StateNode {
   int xPos;
   int yPos;
   int moveCount;
}

class MyQueue {
   StateNode[] queueData = new StateNode[2500];
   int queueFront = 0;
   int queueBack = 0;

   void Enqueue(StateNode node) {
      queueData[queueBack] = node;
      queueBack++;
   }

   StateNode Dequeue() {
      StateNode returnValue = null;
      if (queueBack > queueFront) {
      returnValue = queueData[queueFront];
      QueueFront++;
   }
   return returnValue;
   }

   boolean isNotEmpty() {
      return (queueBack > queueFront);
   }
}
Then, the main code of your solution looks something like this. (Note that if our queue runs out of possible states, and we still haven’t reached our destination, then it must be impossible to get there, hence we return the typical "-1" value.)

MyQueue queue = new MyQueue();
queue.Enqueue(initialState);
while (queue.isNotEmpty()) {
   StateNode curState = queue.Dequeue();
   if (curState == destState)
return curState.moveCount;
   for (int dir = 0; dir < 3; dir++) {
      if (CanMove(curState, dir))
         queue.Enqueue(MoveState(curState, dir));
   }
}

Questions:
1. What are some options for implementing a priority queue? (http://www.geeksforgeeks.org/priority-queue-set-1-introduction/)
2. Implement a queue using two stacks
3. http://www.geeksforgeeks.org/deque-set-1-introduction-applications/
