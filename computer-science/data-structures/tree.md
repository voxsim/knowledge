Much like real life, there are many different types of tree data structures.
- Binary Trees:
  AA Tree, AVL Tree, Binary Search Tree, Binary Tree, Cartesian Tree,
  left child/right sibling tree, order statistic tree, Pagoda, ...
- B Trees:
  B Tree, B+ Tree, B* Tree, B Sharp Tree, Dancing Tree, 2-3 Tree, ...
- Heaps:
  Heap, Binary Heap, Weak Heap, Binomial Heap, Fibonacci Heap, Leonardo
  Heap, 2-3 Heap, Soft Heap, Pairing Heap, Leftist Heap, Treap, ...
- Trees:
  Trie, Radix Tree, Suffix Tree, Suffix Array, FM-index, B-trie, ...
- Multi-way Trees:
  Ternary Tree, K-ary tree, And-or tree, (a,b)-tree, Link/Cut Tree, ...
- Space Partitioning Trees:
  Segment Tree, Interval Tree, Range Tree, Bin, Kd Tree, Quadtree,
  Octree, Z-Order, UB-Tree, R-Tree, X-Tree, Metric Tree, Cover Tree, ...
- Application-Specific Trees:
  Abstract Syntax Tree, Parse Tree, Decision Tree, Minimax Tree, ...

Little did you know you'd be studying dendrology today... and that's not even
all of them. But don't let any of this scare you, most of those don't matter
at all. There were just a lot of Computer Science PhDs who had something to
prove.

Trees are much like graphs or linked lists except they are "unidirectional".
All this means is that they can't have loops of references (DAG).

       Tree:                Not a Tree:
         A                        A
       ↙   ↘                    ↗   ↘
     B       C                B ←–––– C

If you can draw a loop between connected nodes in a tree... well, you don't
have a tree.

Trees have many different uses, they can be used to optimize searching or
sorting. They can organize programs better. They can give you a
representation that is easier to work with.

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

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
```

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

*Binary Tree vs Binary Search Tree*
Binary search tree imposes the condition that, for all nodes, the left children are less than or equal to the current node, which is less then all the right nodes.

*Balanced vs Unbalanced*
Balancing a tree implies only that the depth of subtrees will not vary by more than a certain amount. It does not mean that the left and right subtrees are exactly the same size.

*Full and Complete*
Full and complete trees are trees in which all leaves are at the bottom of the tree, and all non-leaf nodes have exactly two children. Note that full and complete trees are extremely rare, as a tree must have exactly 2^n - 1 nodes to meet this condition.

*Binary Tree Properties*
- The maximum number of nodes at level ‘l’ = 2l-1.
- Maximum number of nodes = 2h – 1. Here h is height of a tree. Height is considered  as is maximum number of nodes on root to leaf path
- Minimum possible height =  ceil(Log2(n+1))   
- In Binary tree, number of leaf nodes is always one  more than nodes with two children.

*Binary Heap*

A Binary Heap is a Binary Tree with following properties:
- It’s a complete tree (All levels are completely filled except possibly the last level and the last level has all keys as left as possible). This property of Binary Heap makes them suitable to be stored in an array.
- A Binary Heap is either Min Heap or Max Heap. In a Min Binary Heap, the key at root must be minimum among all keys present in Binary Heap. The same property must be recursively true for all nodes in Binary Tree. Max Binary Heap is similar to Min Heap. It is mainly implemented using array.

Questions:
1. Design an algorithm and write code to find the first common ancestor of two nodes in a binary tree. Avoid storing additional nodes in a data structure. NOTE: This is not necessarily a binary search tree.
2. You are given a binary tree in which each node contains a value. Design an algorithm to print all paths which sum to a given value. The path does not need to start or end at the root or a leaf, but it must go in a straight line down.
