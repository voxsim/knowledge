## Text
Given a 2D board and a word, find if the word exists in the grid.
The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Solution
```javascript
function wordSearch(board, word) {
  let visited = [];
  for(let i=0; i<board.length; i++) {
    visited[i] = [];
    for(let j=0; j<board[i].length; j++) {
      visited[i][j] = false;
    }
  }
  
  function _search(word, index) {
    let found = false;
    for(let i=0; i<board.length && !found; i++) {
      for(let j=0; j<board[i].length && !found; j++) {
        if(visited[i][j]) continue;
        if(word[index] != board[i][j]) continue;
        visited[i][j] = true;
        found = index === word.length-1 || _search(word, index+1);
        visited[i][j] = false;
      }
    }
    return found;
   }
   
   return _search(word, 0);
}
```

## Explaining

## Testcase
- wordSearch([['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E']], 'ABCCED') = true
- wordSearch([['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E']], 'SEE') = true
- wordSearch([['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E']], 'ABCB') = false

## Complexity
O(n^2)
