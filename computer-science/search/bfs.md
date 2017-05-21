An algorithm that searches a tree (or graph) by searching levels of the tree first.

Operations:
- Starting at the root.
- It finds every node on the same level, most often moving left to right.
- While doing this it tracks the children nodes of the nodes on the current level.
- When finished examining a level it moves to the left most node on the next level.
- The bottom-right most node is evaluated last (the node that is deepest and is farthest right of it's level).

What you need to know:
- Optimal for searching a tree that is wider than it is deep.
- Uses a queue to store information about the tree while it traverses a tree.
- Because it uses a queue it is more memory intensive than *depth first search*.
- The queue uses more memory because it needs to stores pointers

Big O efficiency:
- Search: Breadth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices

```javascript
function bfs(root, callback) {
  const queue = new Queue();
  callback(root);
  root.visited = true;
  queue.enqueue(root);
  
  for(; !queue.isEmpty();) {
     let r = queue.dequeue();
     if(r.adjacents) {
       for(n of r.adjacents) {
          if(!n.visited) {
            callback(n);
            n.visited = true;
            queue.enqueue(n);
          }
       }
     }
  }
}
```

Problems that use BFS usually ask to find the fewest number of steps (or the shortest path) needed to reach a certain end point (state) from the starting one. Besides this, certain ways of passing from one point to another are offered, all of them having the same cost of 1 (sometimes it may be equal to another number). Often there is given a N x M table (formed of N lines and M columns) where certain cells are passable and others are impassable, and the target of the problem is to find the shortest time/path needed to reach the end point from the start one. Such tables may represent mazes, maps, cities, and other similar things. These may be considered as classical BFS problems. Because BFS complexity is in most cases linear (sometimes quadratic, or N logN), constraints of N (or M) could be high – even up to 1 million.
