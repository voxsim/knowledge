Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

/**
 * The remaining two data structures we are going to cover are both in the
 * "tree" family.
 *
 * Much like real life, there are many different types of tree data structures.
 *
 *     Binary Trees:
 *       AA Tree, AVL Tree, Binary Search Tree, Binary Tree, Cartesian Tree,
 *       left child/right sibling tree, order statistic tree, Pagoda, ...
 *
 *     B Trees:
 *       B Tree, B+ Tree, B* Tree, B Sharp Tree, Dancing Tree, 2-3 Tree, ...
 *
 *     Heaps:
 *       Heap, Binary Heap, Weak Heap, Binomial Heap, Fibonacci Heap, Leonardo
 *       Heap, 2-3 Heap, Soft Heap, Pairing Heap, Leftist Heap, Treap, ...
 *
 *     Trees:
 *       Trie, Radix Tree, Suffix Tree, Suffix Array, FM-index, B-trie, ...
 *
 *     Multi-way Trees:
 *       Ternary Tree, K-ary tree, And-or tree, (a,b)-tree, Link/Cut Tree, ...
 *
 *     Space Partitioning Trees:
 *       Segment Tree, Interval Tree, Range Tree, Bin, Kd Tree, Quadtree,
 *       Octree, Z-Order, UB-Tree, R-Tree, X-Tree, Metric Tree, Cover Tree, ...
 *
 *     Application-Specific Trees:
 *       Abstract Syntax Tree, Parse Tree, Decision Tree, Minimax Tree, ...
 *
 * Little did you know you'd be studying dendrology today... and that's not even
 * all of them. But don't let any of this scare you, most of those don't matter
 * at all. There were just a lot of Computer Science PhDs who had something to
 * prove.
 *
 * Trees are much like graphs or linked lists except they are "unidirectional".
 * All this means is that they can't have loops of references.
 *
 *        Tree:                Not a Tree:
 *
 *          A                        A
 *        ↙   ↘                    ↗   ↘
 *      B       C                B ←–––– C
 *
 * If you can draw a loop between connected nodes in a tree... well, you don't
 * have a tree.
 *
 * Trees have many different uses, they can be used to optimize searching or
 * sorting. They can organize programs better. They can give you a
 * representation that is easier to work with.
 */

/*** ===================================================================== ***\
 ** - TREES --------------------------------------------------------------- **
 * ========================================================================= *
 *            ccee88oo             \ | /                                     *
 *          C8O8O8Q8PoOb o8oo    '-.;;;.-,   ooooO8O8QOb o8bDbo              *
 *        dOB69QO8PdUOpugoO9bD  -==;;;;;==-aadOB69QO8PdUOpugoO9bD            *
 *       CgggbU8OU qOp qOdoUOdcb .-';;;'-.  CgggOU ddqOp qOdoUOdcb           *
 *           6OuU  /p u gcoUodpP   / | \ jgs  ooSec cdac pdadfoof            *
 *             \\\//  /douUP         '         \\\d\\\dp/pddoo               *
 *               \\\////                         \\ \\////                   *
 *                |||/\                           \\///                      *
 *                |||\/                           ||||                       *
 *                |||||                          /|||                        *
 ** .............//||||\.......................//|||\\..................... **
\*** ===================================================================== ***/

/**
 * We'll start off with an extremely simple tree structure. It doesn't have any
 * special rules to it and looks something like this:
 *
 *     Tree {
 *       root: {
 *         value: 1,
 *         children: [{
 *           value: 2,
 *           children: [...]
 *         }, {
 *           value: 3,
 *           children: [...]
 *         }]
 *       }
 *     }
 */

class Tree {

  /**
   * The tree has to start with a single parent, the "root" of the tree.
   */

  constructor() {
    this.root = null;
  }

  /**
   * We need a way to traverse our tree and call a function on each node in the
   * tree.
   */

  traverse(callback) {
    // We'll define a walk function that we can call recursively on every node
    // in the tree.
    function walk(node) {
      // First call the callback on the node.
      callback(node);
      // Then recursively call the walk function on all of its children.
      node.children.forEach(walk);
    }

    // Now kick the traversal process off.
    walk(this.root);
  }

  /**
   * Next we need a way to add nodes to our tree.
   */

  add(value, parentValue) {
    let newNode = { value, children: [] };

    // If there is no root, just set it to the new node.
    if (this.root === null) {
      this.root = newNode;
      return;
    }

    // Otherwise traverse the entire tree and find a node with a matching value
    // and add the new node to its children.
    this.traverse(node => {
      if (node.value === parentValue) {
        node.children.push(newNode);
      }
    });
  }
}

/**
 * This is one of the most basic trees you could have and is probably only
 * useful if the data you are representing actually resembles a tree.
 *
 * But with some extra rules a tree can serve a lot of different purposes.
 */

/*** ===================================================================== ***\
 ** - BINARY SEARCH TREES ------------------------------------------------- **
 * ========================================================================= *
 * 0 0 1 0 1 0 0 1 0 1 1 1 0 1  ,@@@@@@@@@@@@@@,   0 0 1 0 1 0 0 1 0 1 1 1 0 *
 * 0 1 0 1 0 1 0 1 1 0 1 1 0  @@`              '@@   0 1 0 1 0 1 1 0 1 0 1 0 *
 * 1 1 0 0 0 1 0 0 1 1 1 0  @@`   8O8PoOb o8o    '@@   0 0 1 0 0 1 0 0 1 1 1 *
 * 0 0 1 1 0 1 0 1 0 0 0  @@   dOB69QO8PdUgoO9bD    @@   1 0 1 1 0 1 0 1 0 0 *
 * ===================== @@   CgbU8OU qOp qOdOdcb    @@  0 1 1 0 1 0 1 0 1 0 *
 *                       @@      6OU /p u gcoUpP     @@  1 0 1 1 0 1 0 0 1 1 *
 * ===================== @@         \\// /doP        @@  0 1 1 0 0 1 0 0 1 0 *
 * 1 1 0 0 1 1 0 1 1 0 0  @@         \\//           @@   1 0 1 0 0 1 1 0 1 1 *
 * 0 1 1 0 1 0 1 1 0 1 1 0  @@,      |||          ,@@  0 1 1 0 1 1 0 0 1 0 1 *
 * 1 0 1 0 1 1 0 0 1 0 0 1 0  @@,   //|\       ,@@   0 1 0 1 0 1 1 0 0 1 1 0 *
 **  1 0 1 0 0 1 1 0 1 0 1 0 1  `@@@@@@@@@@@@@@'   0 1 1 1 0 0 1 0 1 0 1 1  **
\*** ===================================================================== ***/

/**
 * Binary search trees are a fairly common form of tree for their ability to
 * efficiently access, search, insert, and delete values all while keeping them
 * in a sorted order.
 *
 * Imagine taking a sequence of numbers:
 *
 *     1  2  3  4  5  6  7
 *
 * And turning it into a tree starting from the center.
 *
 *              4
 *           /     \
 *        2           6
 *      /   \       /   \
 *     1     3     5     7
 *    -^--^--^--^--^--^--^-
 *     1  2  3  4  5  6  7
 *
 * This is how a binary tree works. Each node can have two children:
 *
 *     - Left: Less than parent node's value.
 *     - Right: Greater than parent node's value.
 *
 * > Note: In order to make this work all values must be unique in the tree.
 *
 * This makes the traversal to find a value very efficient. Say we're trying to
 * find the number 5 in our tree:
 *
 *             (4)         <--- 5 > 4, so move right.
 *           /     \
 *        2         (6)    <--- 5 < 6, so move left.
 *      /   \       /   \
 *     1     3    (5)    7 <--- We've reached 5!
 *
 * Notice how we only had to do 3 checks to reach the number 5. If we were to
 * expand this tree to 1000 items. We'd go:
 *
 *   500 -> 250 -> 125 -> 62 -> 31 -> 15 -> 7 -> 3 -> 4 -> 5
 *
 * Only 10 checks for 1000 items!
 *
 * The other important thing about binary search trees is that they are similar
 * to linked lists in the sense that you only need to update the immediately
 * surrounding items when adding or removing a value.
 */

class BinarySearchTree {

  /**
   * Same as the previous Tree, we need to have a "root" of the binary search
   * tree.
   */

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

A tree is a DAG (Directed Acyclic Graph). 

*Binary Tree vs Binary Search Tree*
Binary search tree imposes the condition that, for all nodes, the left children are less than or equal to the current node, which is less then all the right nodes.

*Balanced vs Unbalanced*
Balancing a tree implies only that the depth of subtrees will not vary by more than a certain amount. It does not mean that the left and right subtrees are exactly the same size.

*Full and Complete*
Full and complete trees are trees in which all leaves are at the bottom of the tree, and all non-leaf nodes have exactly two children. Note that full and complete trees are extremely rare, as a tree must have exactly 2^n - 1 nodes to meet this condition.

*Types of traversal*
Pre-order:
1. Check if the current node is empty / null.
2. Display the data part of the root (or current node) or do an operation.
3. Traverse the left subtree by recursively calling the pre-order function.
4. Traverse the right subtree by recursively calling the pre-order function.

In-order:
1. Check if the current node is empty / null.
2. Traverse the left subtree by recursively calling the in-order function.
3. Display the data part of the root (or current node) or do an operation.
4. Traverse the right subtree by recursively calling the in-order function.

Post-order:
1. Check if the current node is empty / null.
2. Traverse the left subtree by recursively calling the post-order function.
3. Traverse the right subtree by recursively calling the post-order function.
4. Display the data part of the root (or current node) or do an operation.

From TopCoder:
Trees are a data structure consisting of one or more data nodes. The first node is called the "root", and each node has zero or more "child nodes". The maximum number of children of a single node, and the maximum depth of children are limited in some cases by the exact type of data represented by the tree. 

One of the most common examples of a tree is an XML document. The top-level document element is the root node, and each tag found within that is a child. Each of those tags may have children, and so on. At each node, the type of tag, and any attributes, constitutes the data for that node. In such a tree, the hierarchy and order of the nodes is well defined, and an important part of the data itself. Another good example of a tree is a written outline. The entire outline itself is a root node containing each of the top-level bullet points, each of which may contain one or more sub-bullets, and so on. The file storage system on most disks is also a tree structure. 

Corporate structures also lend themselves well to trees. In a classical management hierarchy, a President may have one or more vice presidents, each of whom is in charge of several managers, each of whom presides over several employees. 

A special type of tree is a binary tree. A binary tree also happens to be one of the most efficient ways to store and read a set of records that can be indexed by a key value in some way. The idea behind a binary tree is that each node has, at most, two children. 

In the most typical implementations, the key value of the left node is less than that of its parent, and the key value of the right node is greater than that of its parent. Thus, the data stored in a binary tree is always indexed by a key value. When traversing a binary tree, it is simple to determine which child node to traverse when looking for a given key value. 

One might ask why a binary tree is preferable to an array of values that has been sorted. In either case, finding a given key value (by traversing a binary tree, or by performing a binary search on a sorted array) carries a time complexity of O(log n). However, adding a new item to a binary tree is an equally simple operation. In contrast, adding an arbitrary item to a sorted array requires some time-consuming reorganization of the existing data in order to maintain the desired ordering. 

If you have ever used a field guide to attempt to identify a leaf that you find in the wild, then this is a good way to understand how data is found in a binary tree. To use a field guide, you start at the beginning, and answer a series of questions like "is the leaf jagged, or smooth?" that have only two possible answers. Based upon your answer, you are directed to another page, which asks another question, and so on. After several questions have sufficiently narrowed down the details, you are presented with the name, and perhaps some further information about your leaf. If one were the editor of such a field guide, newly cataloged species could be added to field guide in much the same manner, by traversing through the questions, and finally at the end, inserting a new question that differentiates the new leaf from any other similar leaves. In the case of a computer, the question asked at each node is simply "are you less than or greater than X?" 

Questions:
1. Implement a function to check if a binary tree is balanced. The tree is balanced if the heights of the two subtrees of any node never differ by more than one.
2. Given a sorted array with unique integers, write an algorithm to create a binary search tree with miniaml height.
3. Implement a function to check if a binary tree is a binary search tree
4. Design an algorithm and write code to find the first common ancestor of two nodes in a binary tree. Avoid storing additional nodes in a data structure. NOTE: This is not necessarily a binary search tree.
5. You are given a binary tree in which each node contains a value. Design an algorithm to print all paths which sum to a given value. The path does not need to start or end at the root or a leaf, but it must go in a straight line down.
6. https://www.topcoder.com/community/data-science/data-science-tutorials/an-introduction-to-binary-search-and-red-black-trees/
Implement:
- [ ] insert    // insert value into tree
- [ ] get_node_count // get count of values stored
- [ ] print_values // prints the values in the tree, from min to max
- [ ] delete_tree
- [ ] is_in_tree // returns true if given value exists in the tree
- [ ] get_height // returns the height in nodes (single node's height is 1)
- [ ] get_min   // returns the minimum value stored in the tree
- [ ] get_max   // returns the maximum value stored in the tree
- [ ] is_binary_search_tree
- [ ] delete_value
- [ ] get_successor // returns next-highest value in tree after given value, -1 if none
