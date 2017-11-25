## Text
Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.
For example, given the array [2,3,1,2,4,3] and s = 7, the subarray [4,3] has the minimal length under the problem constraint.

## Solution
```javascript
function minimumSizeSubarraySum(A, s) {
  if(!A || A.length === 0) return 0;
  
  var minSize = Infinity;
  var j = 0;
  var i = 1;
  var sum = A[0];
  
  for(; i <= A.length && j < i;) {
     /*if(A[j] === s || A[i] === s) {
       return 1;
     }*/
     console.log(j, i, sum);
     
     if(sum === s) {
       minSize = Math.min(i - j, minSize);
       sum -= A[j];
       j++;
     } else if(sum > s || i === A.length) {
       sum -= A[j];
       j++;
     } else {
       sum += A[i]; 
       i++;
     }
  }
  
  return minSize === Infinity ? 0 : minSize;
}
```

## Testcase

## Complexity
O(n)
