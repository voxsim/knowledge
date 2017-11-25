## Text
Given an unsorted array, find the max length of subsequence in which the numbers are in incremental order.
For example: If the input array is {7, 2, 3, 1, 5, 8, 9, 6}, a subsequence with the most numbers in incremental order is {2, 3, 5, 8, 9} and the expected output is 5. 

## Solution
```javascript
function longestIncreasingSubsequence(A) {
   var ml = [];
   ml[0] = 1;
   for(var i = 1; i<A.length; i++) {
       var max = 0;
       for(var j=0; j<i; j++) {
            if(A[i] > A[j] && ml[j] > max) {
              max = ml[j];
            }
       }
       if(ml[i-1] > max + 1) {
         ml[i] = ml[i-1];
       } else {
         ml[i] = max + 1;
       }
   }
   return ml[A.length-1];
}
```

## Testcase

## Complexity
O(n^2).
