## Text
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.

## Solution
```javascript
function searchInRotatedSortedArray(A, target) {
  if(!Array.isArray(A)) return -1;
  if(A.length === 0) return -1;
  
  var begin = 0;
  var end = A.length-1;
  
  for(; begin <= end; ) {
    var mid = begin + Math.floor((end - begin)/2);
    
    if(target === A[mid]) {
      return mid;
    }
    
    if(target < A[mid]) {
      if(target >= A[begin]) {
        end = mid-1;
      } else {
        begin = mid+1;
      }
    } else {
      if(target <= A[end]) {
        begin = mid+1;
      } else {
        end = mid-1;
      }
    }
  }
  
  return -1;
}
```

## Testcase
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 4) => 0
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 5) => 1
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 6) => 2
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 7) => 3
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 0) => 4
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 1) => 5
- searchInRotatedSortedArray([4, 5, 6, 7, 0, 1, 2], 2) => 6
- searchInRotatedSortedArray([], 1) => -1
- searchInRotatedSortedArray(undefined, 1) => -1
- searchInRotatedSortedArray([], undefined) => -1
- searchInRotatedSortedArray([1], 1) => 0

## Complexity
O(logn)
