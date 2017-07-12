## Text
Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

```
// Examples:
// Given binary tree [3,9,20],
//    3
//   /\
//  /  \
//  9  20
// return its vertical order traversal as:
// [
//   [9],
//   [3],
//   [20]
// ]
// Given binary tree [3,9,20,null,null,15,7],
//    3
//   /\
//  /  \
//  9  20
//     /\
//    /  \
//   15   7
// return its vertical order traversal as:
// [
//   [9],
//   [3,15],
//   [20],
//   [7]
// ]
// Given binary tree [3,9,8,4,0,1,7],
//      3
//     /\
//    /  \
//    9   8
//   /\  /\
//  /  \/  \
//  4  01   7
// return its vertical order traversal as:
// [
//   [4],
//   [9],
//   [3,0,1],
//   [8],
//   [7]
// ]
// Given binary tree [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5),
//      3
//     /\
//    /  \
//    9   8
//   /\  /\
//  /  \/  \
//  4  01   7
//     /\
//    /  \
//    5   2
// return its vertical order traversal as:
// [
//   [4],
//   [9,5],
//   [3,0,1],
//   [8,2],
//   [7]
// ]
// Given binary tree [3,9,8,4,0,1,7,null,6,null,2,5] (0's right child is 2 and 1's left child is 5),
//      3
//     /\
//    /  \
//    9   8
//   /\  /\
//  /  \/  \
//  4  01   7
//  \  /\
//   \/  \
//   65   2
// return its vertical order traversal as:
// [
//   [4],
//   [9,5],
//   [3,0,1],
//   [8,2],
//   [7]
// ]
```

## Solution
```javascript
function binaryTreeVerticalOrderTraversal(root) {
     let nodes = [];
     function addAtRightLevel(node, acc, index) {
          if(!node) {
               return index;
          }
          console.log(node.val, index);
          if(!acc[index]) {
               acc[index] = [];
          }
          acc[index].push(node.val);
          addAtRightLevel(node.left, acc, index-1);
          addAtRightLevel(node.right, acc, index+1);
          return index+1;
     }
     let index=0;
     for(var node=root;node;node=node.left, index++);
     addAtRightLevel(root, nodes, index-1);
     return nodes;
}
```

## Testcase
*   binaryTreeVerticalOrderTraversal({val: 3, left: {val: 9, left: null, right: null}, right: {val: 20, left: null, right: null}}) = [[9], [3], [20]]
*   binaryTreeVerticalOrderTraversal({val: 3, left: {val: 9, left: null, right: null}, right: {val: 20, left: {val: 15, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = [[9], [3,15], [20], [7]]
*   binaryTreeVerticalOrderTraversal({val: 3, left: {val: 9, left: {val: 4, left: null, right: null}, right: {val: 0, left: null, right: null}}, right: {val: 20, left: {val: 15, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = [[4], [9], [3,0,15], [20], [7]]

## Complexity
O(h+n)
