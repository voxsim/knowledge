## Text

Given an integer x and a sorted array A of N distinct integers, design a linear-time algorithm to determine if there exists two distinct indices i and j such that a[i] + a[j] == x.

## Solution

```javascript
function twosum(A, x) {
  if(!A) return;
  
  var begin = 0;
  var end = A.length-1;
  for(; begin < end;) {
    if(A[begin] + A[end] === x) {
      return [begin, end];
    }
    
    if(A[begin] + A[end] < x) {
      begin++;
    } else {
      end--;
    }
  }
  
  return;
}
```

## Testcase

- twosum([1, 2, 3, 4], 6) => [1, 3]
- twosum(undefined, 1) => undefined
- twosum([], 1) => undefined
- twosum([1, 2, 3, 4], undefined) => undefined
- twosum([1, 2, 3, 4], -1) => undefined

# Complexity
Time: O(n)
Space: O(1)
