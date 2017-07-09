## Text
Given a binary tree, return all root-to-leaf paths.

## Solution
```javascript
function allPathsFrom(node) {
  if(node === null) {
    return [];
  }
  
  let pathsAtLeft = allPathsFrom(node.left);
  let pathsAtRight = allPathsFrom(node.right);
  
  if(/* isALeaf */ pathsAtLeft.length === 0 && pathsAtRight.length === 0) {
    return [[node.val]];
  }
  
  let paths = [];
  for(var i=0; i<pathsAtLeft.length; i++) {
    paths.push([node.val, ...pathsAtLeft[i]]);
  }
  for(var i=0; i<pathsAtRight.length; i++) {
    paths.push([node.val, ...pathsAtRight[i]]);
  }
  return paths;
}
```

## Testcase
- allPathsFrom(null) = []
- allPathsFrom({val: 1, left: null, right: null}) = [[1]]
- allPathsFrom({val: 1, left: {val: 2, left: null, right: null}, right: null}) = [[1, 2]]
- allPathsFrom({val: 1, left: null, right: {val: 2, left: null, right: null}}) = [[1, 2]]
- allPathsFrom({val: 1, left: {val: 2, left: null, right: null}, right: {val: 3, left: null, right: null}}) = [[1, 2], [1, 3]]
- allPathsFrom({val: 1, left: {val: 2, left: null, right: null}, right: {val: 3, left: {val: 4, left: null, right: null}, right: null}}) = [[1, 2], [1, 3, 4]]

## Complexity
O(n^2)
