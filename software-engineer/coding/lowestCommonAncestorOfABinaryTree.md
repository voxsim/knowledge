## Text
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

```
         _______3______
        /              \
     ___5__          ___1__
    /      \        /      \
    6      2       0       8
          /  \
         7   4
```

For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

## Solution
```javascript
function lowestCommonAncestorOfABinaryTree(node, p, q) {
  if(node === null || node.id === p || node.id === q) {
    return node;
  }
  
  let right = lowestCommonAncestorOfABinaryTree(node.right, p, q);
  let left = lowestCommonAncestorOfABinaryTree(node.left, p, q);
  
  if(left != null && right != null) 
    return node;
    
  return left != null ? left : right;
}
```

## Testcase
- lowestCommonAncestorOfABinaryTree(root, 5, 1) => 3
- lowestCommonAncestorOfABinaryTree(root, 2, 1) => 3
- lowestCommonAncestorOfABinaryTree(root, 2, 0) => 3
- lowestCommonAncestorOfABinaryTree(root, 2, 6) => 5
- lowestCommonAncestorOfABinaryTree(root, 2, 4) => 2

## Complexity
O(n)
