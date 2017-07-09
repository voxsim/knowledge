## Text
You are given a m x n 2D grid initialized with these three possible values.
- -1 -> A wall or an obstacle.
- 0 -> A gate.
- INF - Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

For example, given the 2D grid:
```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
0  -1 INF INF
```

After running your function, the 2D grid should be:
```
3  -1   0   1
2   2   1  -1
1  -1   2  -1
0  -1   3   4
```

## Solution
```javascript
function wallsAndGates(grid) {
  function fill(i, j, depth) {
    if(i < 0 || i === grid.length) return;
    if(j < 0 || j === grid[i].length) return;
    if(/* isAnObstacle */ grid[i][j] === -1) return;
    if(/* isAlreadyVisited */ depth > grid[i][j]) return;
    
    grid[i][j] = Math.min(grid[i][j], depth);
    
    fill(i+1, j, depth+1);
    fill(i-1, j, depth+1);
    fill(i, j+1, depth+1);
    fill(i, j-1, depth+1);
  }
  
  for(let i=0; i<grid.length; i++) {
    for(let j=0; j<grid[i].length; j++) {
      if(/* isAGate */ grid[i][j] === 0) {
        fill(i+1, j, 1);
        fill(i-1, j, 1);
        fill(i, j+1, 1);
        fill(i, j-1, 1);
      }
    }
  }
  
  return grid;
}
```

## Explaining

## Testcase
- wallsAndGates([[Infinity, -1, 0, Infinity], [Infinity, Infinity, Infinity, -1], [Infinity, -1, Infinity, -1], [0, -1, Infinity, Infinity]])

## Complexity

