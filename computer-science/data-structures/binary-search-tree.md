Big O efficiency:
- Access: O(log(n))
- Search: O(log(n))
- Insertion: O(log(n))
- Delete: O(log(n))

Binary search tree imposes the condition that, for all nodes, the left children are less than or equal to the current node, which is less then all the right nodes.
Binary search trees are a fairly common form of tree for their ability to
efficiently access, search, insert, and delete values all while keeping them
in a sorted order.

Imagine taking a sequence of numbers:

    1  2  3  4  5  6  7

And turning it into a tree starting from the center.

             4
          /     \
       2           6
     /   \       /   \
    1     3     5     7
   -^--^--^--^--^--^--^-
    1  2  3  4  5  6  7

This is how a binary tree works. Each node can have two children:

- Left: Less than parent node's value.
- Right: Greater than parent node's value.

> Note: In order to make this work all values must be unique in the tree.

This makes the traversal to find a value very efficient. Say we're trying to
find the number 5 in our tree:

            (4)         <--- 5 > 4, so move right.
          /     \
       2         (6)    <--- 5 < 6, so move left.
     /   \       /   \
    1     3    (5)    7 <--- We've reached 5!

Notice how we only had to do 3 checks to reach the number 5. If we were to
expand this tree to 1000 items. We'd go:

  500 -> 250 -> 125 -> 62 -> 31 -> 15 -> 7 -> 3 -> 4 -> 5

Only 10 checks for 1000 items!

The other important thing about binary search trees is that they are similar
to linked lists in the sense that you only need to update the immediately
surrounding items when adding or removing a value.

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

/**

class BinarySearchTree {

  constructor() {
    this.root = null;
  }

  /**
   * In order to test if the value exists in the tree, we first need to search
   * through the tree.
   */

  contains(value) {
    // We start at the root.
    let current = this.root;

    // We're going to keep running as long as we have another node to visit.
    // If we reach a `left` or `right` that is `null` then this loop ends.
    while (current) {

      // If the value is greater than the current.value we move to the right
      if (value > current.value) {
        current = current.right;

      // If the value is less than the current.value we move to the left.
      } else if (value < current.value) {
        current = current.left;

      // Otherwise we must be equal values and we return true.
      } else {
        return true;
      }
    }

    // If we haven't matched anything then we return false.
    return false;
  }

  /**
   * In order to add items to this tree we are going to do the same traversal
   * as before, bouncing between left and right nodes depending on them being
   * less than or greater than the value we're adding.
   *
   * However, this time when we reach a `left` or `right` that is `null` we're
   * going to add a new node in that position.
   */

  add(value) {
    // First let's setup our node.
    let node = {
      value: value,
      left: null,
      right: null
    };

    // Special case for when there isn't any root node and we just need to add
    // one.
    if (this.root === null) {
      this.root = node;
      return;
    }

    // We start at the root.
    let current = this.root;

    // We're going to loop until we've either added our item or discovered it
    // already exists in the tree.
    while (true) {

      // If the value is greater than the current.value we move to the right.
      if (value > current.value) {

        // If `right` does not exist, set it to our node, and stop traversing.
        if (!current.right) {
          current.right = node;
          break;
        }

        // Otherwise just move on to the right node.
        current = current.right;

      // If the value is less than the current.value we move to the left.
      } else if (value < current.value) {

        // If `left` does not exist, set it to our node, and stop traversing.
        if (!current.left) {
          current.left = node;
          break;
        }

        // Otherwise just move on to the left node.
        current = current.left;

      // If the number isn't less than or greater, then it must be the same and
      // we don't do anything.
      } else {
        break;
      }
    }
  }
}
```
