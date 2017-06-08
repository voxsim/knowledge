## Text
Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

Follow up:
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

## Solution
```javascript
function productOfArrayExceptSelf(A) {
  if(!A) return;
  
  var result = [];
  var left = 1;
  for(var i=0; i<A.length; i++) {
    if(i > 0) {
      left *= A[i-1];
    }
    result.push(left);
  }
  
  var right=1;
  for(var i=A.length-1; i>-1; i--) {
     if(i < A.length-1) {
       right *= A[i+1];
     }
     result[i] = result[i]*right;
  }
  
  return result;
}
```

## Testcase
-

# Complexity
-
