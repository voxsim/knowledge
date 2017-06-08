## Text
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

## Solution
```javascript
function moveZeros(A) {
  if(!A) return;
  
  var zeroIndexes = [];
  for(var i=0; i < A.length; i++) {
    if(A[i] === 0) {
      zeroIndexes.push(i);
    } else if(zeroIndexes.length > 0) {
      var zeroIndex = zeroIndexes.shift(); // if we use a queue this is O(1)
      A[zeroIndex] = A[i];
      A[i] = 0;
      zeroIndexes.push(i);
    }
  }
  
  return A;
}
```

## Testcase
moveZeros([1, 2, 3]) = [1, 2, 3]
moveZeros([]) = []
moveZeros([1, 2, 3, 0]) = [1, 2, 3, 0]
moveZeros([1, 2, 3, 0, 0]) = [1, 2, 3, 0, 0]
moveZeros([1, 0]) = [1, 0]
moveZeros([0, 1]) = [1, 0]
moveZeros([0, 1, 2]) = [1, 2, 0]
moveZeros([0, 0, 1]) = [1, 0, 0]

# Complexity
Time Complexity: O(n) if we use a queue
Space Complexity: O(n) if we have all zeroes
