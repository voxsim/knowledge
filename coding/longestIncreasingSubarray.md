## Text
Given an unsorted array, find the max length of subarray in which the numbers are in incremental order.
For example: If the input array is {7, 2, 3, 1, 5, 8, 9, 6}, a subarray with the most numbers in incremental order is {1, 5, 8, 9} and the expected output is 4. Complexity O(n). Subarray is contiguous respect than a subsequence.

## Solution
```javascript
function longest_increasing_subsubarray(A) {
  var lis = [];
  lis[0] = 1;
  var max = 0;
  
  for(var i=1; i < A.length; i++) {
     if(A[i-1] <= A[i]) {
       lis[i] = lis[i-1] + 1;
     } else {
       lis[i] = 1;
     }
     if(max < lis[i]) {
       max = lis[i];
     }
  }
  
  console.log(lis);
  return max;
}
```

## Testcase

## Complexity
