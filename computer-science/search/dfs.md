An algorithm that searches a tree (or graph) by searching depth of the tree first.

Algorithm:
- Starting at the root.
- It traverses left down a tree until it cannot go further.
- Once it reaches the end of a branch it traverses back up trying the right child of nodes on that branch, and if possible left from the right children.
- When finished examining a branch it moves to the node right of the root then tries to go left on all it's children until it reaches the bottom.
- The right most node is evaluated last (the node that is right of all it's ancestors).

What you need to know:
- Optimal for searching a tree that is deeper than it is wide.
- Uses a stack to push nodes onto.
- Because a stack is LIFO it does not need to keep track of the nodes pointers and is therefore less memory intensive than breadth first search.
- Once it cannot go further left it begins evaluating the stack.

Big O efficiency:
- Search: Depth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices

```javascript
function dfs(root, callback) {
  if(!root) return;
  callback(root);
  root.visited = true;
  
  if(!root.adjacents) return;
  for(const n of root.adjacents) {
    if(!n.visited) {
      dfs(n, callback);
    }
  }
}
```

1. https://www.topcoder.com/community/data-science/data-science-tutorials/introduction-to-graphs-and-their-data-structures-section-2/ -> DFS Implemented with a stack
