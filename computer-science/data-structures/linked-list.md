Big O efficiency:
- Access: O(n)
- Search: O(n)
- Insert: O(1)
- Delete: O(1)

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

/**
 * Next we're going to see how a graph-like structure can help optimize ordered
 * lists of data.
 *
 * Linked lists are a very common data structure that is often used to
 * implement other data structures because of its ability to efficiently add
 * items to the start, middle, and end.
 *
 * The basic idea of a linked list is similar to a graph. You have nodes that
 * point to other nodes. They look sorta like this:
 *
 *     1 -> 2 -> 3 -> 4 -> 5
 *
 * Visualizing them as a JSON-like structure looks like this:
 *
 *     {
 *       value: 1,
 *       next: {
 *         value: 2,
 *         next: {
 *           value: 3,
 *           next: {...}
 *         }
 *       }
 *     }
 */

class LinkedList {

  /**
   * Unlike a graph, a linked list has a single node that starts off the entire
   * chain. This is known as the "head" of the linked list.
   *
   * We're also going to track the length.
   */

  constructor() {
    this.head = null;
    this.length = 0;
  }

  /**
   * First we need a way to retrieve a value in a given position.
   *
   * This works differently than normal lists as we can't just jump to the
   * correct position. Instead we need to move through the individual nodes.
   */

  get(position) {
    // Throw an error if position is greater than the length of the LinkedList
    if (position >= this.length) {
      throw new Error('Position outside of list range');
    }

    // Start with the head of the list.
    let current = this.head;

    // Slide through all of the items using node.next until we reach the
    // specified position.
    for (let index = 0; index < position; index++) {
      current = current.next;
    }

    // Return the node we found.
    return current;
  }

  /**
   * Next we need a way to add nodes to the specified position.
   *
   * We're going for a generic add method that accepts a value and a position.
   */

  add(value, position) {
    // First create a node to hold our value.
    let node = { value, next: null };

    // We need to have a special case for nodes being inserted at the head.
    // We'll set the "next" field to the current head and then replace it with
    // our new node.
    if (position === 0) {
      node.next = this.head;
      this.head = node;

    // If we're adding a node in any other position we need to splice it in
    // between the current node and the previous node.
    } else {
      // First, find the previous node and the current node.
      let prev = this.get(position - 1);
      let current = prev.next;
      // Then insert the new node in between them by setting its "next" field
      // to the current node and updating the previous node's "next" field to
      // the new one.
      node.next = current;
      prev.next = node;
    }

    // Finally just increment the length.
    this.length++;
  }

  /**
   * The last method we need is a remove method. We're just going to look up a
   * node by its position and splice it out of the chain.
   */

  remove(position) {
    // We should not be able to remove from an empty list
    if (!this.head) {
      throw new Error('Removing from empty list')
    }
    // If we're removing the first node we simply need to set the head to the
    // next node in the chain
    if (position === 0) {
      this.head = this.head.next;

    // For any other position we need to look up the previous node and set it
    // to the node after the current position.
    } else {
      let prev = this.get(position - 1);
      prev.next = prev.next.next;
    }

    // Then we just decrement the length.
    this.length--;
  }
}
```

Designed to optimize insertion and deletion, slow at indexing and searching. Remember:
- *Doubly linked list* has nodes that reference the previous node.
- *Circularly linked list* is simple linked list whose *tail*, the last node, references the *head*, the first node.

Questions:
1. Write code to remove duplicates from an unsorted linked list
2. How you would solve (1) if a temporary buffer is not allowed?
3. Implement an algorithm to find kth to last element of a single linked list
4. Implement an algorithm to delete a node in the middle of a singly linked list, given only access to that node.
5. Write a code to partition a linked list around a value x, such that all nodes less than x come before all nodes greater than or equal to x
6. You have two numbers represented by a linked list, where each node is a single digit. THe digits are stored in reverse order, such that 7 -> 1 -> 6 is 617. Write a function that adds two numbers and return the sum as linked list.
7. Do the same of (6), but the digits are stored in forward order, e.g. 6 -> 1 -> 7 is 617.
8. Implement a function to check if a linked list is palindrome.
9. Write push_front(value) - adds an item to the front of the list
10. Write pop_front() - remove front item and return its value
11. Write push_back(value) - adds an item at the end
12. Write pop_back() - removes end item and returns its value
13. Write front() - get value of front item
14. Write back() - get value of end item
15. Write reverse() - reverses the list
