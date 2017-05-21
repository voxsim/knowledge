## Search Basics

###**Breadth First Search**
####Definition:
- An algorithm that searches a tree (or graph) by searching levels of the tree first, starting at the root.
- It finds every node on the same level, most often moving left to right.
- While doing this it tracks the children nodes of the nodes on the current level.
- When finished examining a level it moves to the left most node on the next level.
- The bottom-right most node is evaluated last (the node that is deepest and is farthest right of it's level).
####What you need to know:
- Optimal for searching a tree that is wider than it is deep.
- Uses a queue to store information about the tree while it traverses a tree.
- Because it uses a queue it is more memory intensive than **depth first search**.
- The queue uses more memory because it needs to stores pointers

####Big O efficiency:
- Search: Breadth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices

###**Depth First Search**
####Definition:
- An algorithm that searches a tree (or graph) by searching depth of the tree first, starting at the root.
- It traverses left down a tree until it cannot go further.
- Once it reaches the end of a branch it traverses back up trying the right child of nodes on that branch, and if possible left from the right children.
- When finished examining a branch it moves to the node right of the root then tries to go left on all it's children until it reaches the bottom.
- The right most node is evaluated last (the node that is right of all it's ancestors).

####What you need to know:
- Optimal for searching a tree that is deeper than it is wide.
- Uses a stack to push nodes onto.
- Because a stack is LIFO it does not need to keep track of the nodes pointers and is therefore less memory intensive than breadth first search.
- Once it cannot go further left it begins evaluating the stack.

####Big O efficiency:
- Search: Depth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices

####Breadth First Search Vs. Depth First Search
- The simple answer to this question is that it depends on the size and shape of the tree.
- For wide, shallow trees use Breadth First Search
- For deep, narrow trees use Depth First Search

####Nuances:
- Because BFS uses queues to store information about the nodes and its children, it could use more memory than is available on your computer.  (But you probably won't have to worry about this.)
- If using a DFS on a tree that is very deep you might go unnecessarily deep in the search.
- Breadth First Search tends to be a looping algorithm.
- Depth First Search tends to be a recursive algorithm.
