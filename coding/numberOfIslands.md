## Text
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Solution
```javascript
function is_land(place) {
  return place === 1;
}

function is_water(place) {
  return place === 0;
}

function visit(island_visited, island, i, j) {
  console.log('visit', i, j);
  if(i === island.length || j === island[i].length || is_water(island[i][j]) || island_visited[i][j]) {
    return;
  }
  
  island_visited[i][j] = 1;
  
  visit(island_visited, island, i+1, j);
  visit(island_visited, island, i, j+1);
}

function numberOfIslands(island) {
  let number = 0;
  let island_visited = [];
  for(let i=0; i<island.length; i++) {
    island_visited[i] = [];
    for(let j=0; j<island[i].length; j++) {
       island_visited[i][j] = 0;
    }
  }
  
  for(let i=0; i<island.length; i++) {
    for(let j=0; j<island[i].length; j++) {
       if(is_land(island[i][j]) && !island_visited[i][j]) {
         console.log('journey', i, j);
         visit(island_visited, island, i, j);
         number++;
       }
    }
  }
  
  return number;
}
```

## Testcase
```
[
[1, 1, 1, 1, 0],
[1, 1, 0, 1, 0],
[1, 1, 0, 0, 0],
[0, 0, 0, 0, 0]
]
```
Answer: 1

```
[
[1, 1, 0, 0, 0],
[1, 1, 0, 0, 0],
[0, 0, 1, 0, 0],
[0, 0, 0, 1, 1]
]
11000
11000
00100
00011
```
Answer: 3

## Complexity
O(m*n) 
