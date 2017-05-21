Big O efficiency:
- Access: O(n)
- Search: O(n)
- Insert: O(1) at end
- Delete: O(1) at end


Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

/**
 * Stacks are similar to lists in that they have an order, but they limit you
 * to only pushing and popping values at the end of the list, which as we saw
 * before are very fast operations when mapping directly to memory.
 *
 * However, Stacks can also be implemented with other data structures in order
 * to add functionality to them.
 *
 * The most common usage of stacks is places where you have one process adding
 * items to the stack and another process removing them from the end–
 * prioritizing items added most recently.
 */

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
