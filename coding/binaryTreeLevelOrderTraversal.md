## Text
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
```
     3
    / \
   9  20
     /  \
    15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```

## Solution
```javascript
function binaryTreeLevelOrderTraversal(root) {
     let nodes = [];
     function addAtRightLevel(node, acc, index) {
          if(!node) {
               return;
          }
          if(!acc[index]) {
               acc[index] = [];
          }
          acc[index].push(node.val);
          addAtRightLevel(node.left, acc, index+1);
          addAtRightLevel(node.right, acc, index+1);
     }
     addAtRightLevel(root, nodes, 0);
     return nodes;
}
```

## Testcase
- binaryTreeLevelOrderTraversal({val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}}) = [[2], [1,3]]
- binaryTreeLevelOrderTraversal({val: 3, left: {val: 9, left: null, right: null}, right: {val: 20, left: {val: 15, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = [[3], [9,20], [15, 7]]
- binaryTreeLevelOrderTraversal({val: 3, left: {val: 9, left: {val: 1, left: null, right: null}, right: {val: 2, left: null, right: null}}, right: {val: 20, left: {val: 15, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = [[3], [9,20], [1, 2, 15, 7]]

## Complexity
O(n)
