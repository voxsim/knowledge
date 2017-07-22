## Text
Given a binary tree, determine if it is a valid binary search tree (BST).
Assume a BST is defined as follows:
The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.

## Solution
```javascript
function validate(node, min, max) {
    if(node === null) {
        return true;
    }
    return 
        node.val < max &&
        node.val > min &&
        validate(node.left, min, node.val) && 
        validate(node.right, node.val, max);
}

function validateBinarySearchTree(root) {
    return
        root.val < root.right.val &&
        root.val > root.left.val &&
        validate(root.left, -Infinity, root.val) && 
        validate(root.right, root.val, Infinity);
}
```

## Explaining

## Testcase
```
Example 1:
    2
   / \
  1   3
Binary tree [2,1,3], return true.
```
```
Example 2:
    1
   / \
  2   3
Binary tree [1,2,3], return false.
```

## Complexity
O(n)
