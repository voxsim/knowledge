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

From GeeksforGeeks:
Binary Tree

Unlike Arrays, Linked Lists, Stack and queues, which are linear data structures, trees are hierarchical data structures.
A binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child. It is implemented mainly using Links.
Binary Tree Representation: A tree is represented by a pointer to the topmost node in tree. If the tree is empty, then value of root is NULL. A Binary Tree node contains following parts.
1. Data
2. Pointer to left child
3. Pointer to right child

A Binary Tree can be traversed in two ways:
Depth First Traversal: Inorder (Left-Root-Right), Preorder (Root-Left-Right) and Postoder (Left-Right-Root)
Breadth First Traversal: Level Order Traversal

Binary Tree Properties:

The maximum number of nodes at level ‘l’ = 2l-1.

Maximum number of nodes = 2h – 1.
Here h is height of a tree. Height is considered 
as is maximum number of nodes on root to leaf path

Minimum possible height =  ceil(Log2(n+1))   

In Binary tree, number of leaf nodes is always one 
more than nodes with two children.

Time Complexity of Tree Traversal: O(n)
Examples : One reason to use binary tree or tree in general is for the things that form a hierarchy. They are useful in File structures where each file is located in a particular directory and there is a specific hierarchy associated with files and directories. Another example where Trees are useful is storing heirarchical objects like JavaScript Document Object Model considers HTML page as a tree with nesting of tags as parent child relations.
