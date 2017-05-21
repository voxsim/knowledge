BFS vs DFS
- The simple answer to this question is that it depends on the size and shape of the tree.
- For wide, shallow trees use Breadth First Search
- For deep, narrow trees use Depth First Search

More info:
- Because BFS uses queues to store information about the nodes and its children, it could use more memory than is available on your computer.  (But you probably won't have to worry about this.)
- If using a DFS on a tree that is very deep you might go unnecessarily deep in the search.
- Breadth First Search tends to be a looping algorithm.
- Depth First Search tends to be a recursive algorithm.
