## Text
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element. Note: You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solution
```javascript
function kthLargestElementInAnArray(arr, k) {
  arr.sort((a, b) => b - a);
  return arr[k-1];
}
```

## Explaining

## Testcase
- kthLargestElementInAnArray([3,2,1,5,6,4], 2) = 5
- kthLargestElementInAnArray([3,2,1,4,6,4], 3) = 4

## Complexity
O(nlogn)
