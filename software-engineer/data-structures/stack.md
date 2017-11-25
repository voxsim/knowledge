Big O efficiency:
- Access: O(n)
- Search: O(n)
- Insert: O(1) at end
- Delete: O(1) at end

Stacks are similar to lists in that they have an order, but they limit you
to only pushing and popping values at the end of the list, which as we saw
before are very fast operations when mapping directly to memory.
 
However, Stacks can also be implemented with other data structures in order
to add functionality to them.
 
The most common usage of stacks is places where you have one process adding
items to the stack and another process removing them from the end, i.e. prioritizing items added most recently.

Stacks are, in a sense, the opposite of queues, in that they are described as "last in, first out". The classic example is the pile of plates at the local buffet. The workers can continue to add clean plates to the stack indefinitely, but every time, a visitor will remove from the stack the top plate, which is the last one that was added. 

While it may seem that stacks are rarely implemented explicitly, a solid understanding of how they work, and how they are used implicitly, is worthwhile education. Those who have been programming for a while are intimately familiar with the way the stack is used every time a subroutine is called from within a program. Any parameters, and usually any local variables, are allocated out of space on the stack. Then, after the subroutine has finished, the local variables are removed, and the return address is "popped" from the stack, so that program execution can continue where it left off before calling the subroutine. 

An understanding of what this implies becomes more important as functions call other functions, which in turn call other functions. Each function call increases the "nesting level" (the depth of function calls, if you will) of the execution, and uses increasingly more space on the stack. Of paramount importance is the case of a recursive function. When a recursive function continually calls itself, stack space is quickly used as the depth of recursion increases. Nearly every seasoned programmer has made the mistake of writing a recursive function that never properly returns, and calls itself until the system throws up an "out of stack space" type of error. 

Nevertheless, all of this talk about the depth of recursion is important, because stacks, even when not used explicitly, are at the heart of a depth first search. A depth first search is typical when traversing through a tree, for instance looking for a particular node in an XML document. The stack is responsible for maintaining, in a sense, a trail of what path was taken to get to the current node, so that the program can "backtrack" (e.g. return from a recursive function call without having found the desired node) and proceed to the next adjacent node.

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

class Stack {

  /**
   * We're going to again be backed by a JavaScript array, but this time it
   * represents a list like we implemented before rather than memory.
   */

  constructor() {
    this.list = [];
    this.length = 0;
  }

  /**
   * We're going to implement two of the functions from list's "push" and "pop"
   * which are going to be identical in terms of functionality.
   */

  /**
   * Push to add items to the top of the stack.
   */

  push(value) {
    this.length++;
    this.list.push(value);
  }

  /**
   * And pop to remove items from the top of the stack.
   */

  pop() {
    // Don't do anything if we don't have any items.
    if (this.length === 0) return;

    // Pop the last item off the end of the list and return the value.
    this.length--;
    return this.list.pop();
  }

  /**
   * We're also going to add a function in order to view the item at the top of
   * the stack without removing it from the stack.
   */

  peek() {
    // Return the last item in "items" without removing it.
    return this.list[this.length - 1];
  }
}
```

This is a version with linked list.


```javascript
class Stack {

  constructor() {
    this.head = null;
    this.length = 0;
  }

  push(value) {
    const t = { value, next: this.head };
    this.head = t;
  }

  pop() {
    if(this.head !== null) {
      const t = this.head;
      this.head = this.head.next;
      return t.value;
    }
    return null;
  }

  peek() {
    return this.head.value;
  }
}
```
