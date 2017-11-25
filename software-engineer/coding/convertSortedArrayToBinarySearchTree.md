## Text
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

## Solution
```javascript
function convertSortedArrayToBinarySearchTree(array) {
  if(array.length === 0) {
    return null;
  }
  
  let mid = Math.floor(array.length/2);
  return node = {
    val: array[mid],
    left: convertSortedArrayToBinarySearchTree(array.slice(0, mid)),
    right: convertSortedArrayToBinarySearchTree(array.slice(mid+1))
  };
}
```

## Explaining

## Testcase
- convertSortedArrayToBinarySearchTree([1, 2, 3, 4, 5, 6, 7])
- convertSortedArrayToBinarySearchTree([1, 2, 3, 4, 5])

## Complexity
O(nlogn)
