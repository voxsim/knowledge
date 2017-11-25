## Text
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.
Calling next() will return the next smallest number in the BST.
Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.

## Solution
```javascript
function binarySearchTreeIterator(root) {
  let stack = [];
  for(let node=root;node;node=node.left) {
    stack.push(node);
  }
  return {
    hasNext: () => stack.length > 0,
    next: () => {
      let nextSmallest = stack.pop();
      for(let node=nextSmallest.right;node;node=node.left) {
        stack.push(node);
      }
      return nextSmallest.val;
    }
  };
}
```

## Testcase
- binarySearchTreeIterator({val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}})
- binarySearchTreeIterator({val: 4, left: {val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}}, right: {val: 6, left: {val: 5, left: null, right: null}, right: {val: 7, left: null, right: null}}})

## Complexity
