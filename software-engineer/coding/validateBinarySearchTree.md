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
    return node.val < max &&
        node.val > min &&
        validate(node.left, min, node.val) && 
        validate(node.right, node.val, max);
}

function validateBinarySearchTree(root) {
    return validate(root.left, -Infinity, root.val) && 
        validate(root.right, root.val, Infinity);
}
```

## Explaining

## Testcase
- validateBinarySearchTree({val: 2, left: null, right: null})
- validateBinarySearchTree({val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}}) = true
- validateBinarySearchTree({val: 1, left: {val: 2, left: null, right: null}, right: {val: 3, left: null, right: null}}) = false
- validateBinarySearchTree({val: 4, left: {val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}}, right: {val: 6, left: {val: 5, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = true
- validateBinarySearchTree({val: 4, left: {val: 2, left: {val: 1, left: null, right: null}, right: {val: 4, left: null, right: null}}, right: {val: 6, left: {val: 5, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = false
- validateBinarySearchTree({val: 4, left: {val: 2, left: {val: 1, left: null, right: null}, right: {val: 3, left: null, right: null}}, right: {val: 6, left: {val: 4, left: null, right: null}, right: {val: 7, left: null, right: null}}}) = false

## Complexity
O(n)
