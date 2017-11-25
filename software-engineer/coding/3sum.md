## Text
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

## Solution
```javascript
function twosum(A, x) {
  if(!A || A.length === 0) return [];
  
  var result = [];
  for(var begin=0, end=A.length-1; begin < end; ) {
    if(A[begin] + A[end] === x) {
      result.push([begin, end]);
      begin++;
      end--;
      for(; begin < end && A[begin] === A[begin-1]; begin++);
      for(; begin < end && A[end] === A[end+1]; end--);
    } else if(A[begin] + A[end] < x) {
      begin++; 
    } else {
      end--;
    }
  }
  
  return result;
}

function threesum(S) {
  if(!S || S.length === 0) return [];
  
  S.sort((a, b) => a - b);
  console.log(S);
  
  var result = [];
  for(var i=0; i<S.length-2; i++) {
     if(i > 0 && S[i] === S[i-1]) {
       continue;
     }
     
     var opposites = twosum(S.slice(i+1), -S[i]);
     console.log(S[i], opposites);
     if(opposites.length > 0) {
       for(var j=0; j<opposites.length; j++) {
        result.push([S[i], S[opposites[j][0]+i+1], S[opposites[j][1]+i+1]]);
       }
     }
  }
  return result;
}
```

## Testcase
- threesum([-1, -1, 2, -4]) => [[-1, -1, 2]]
- threesum([-1, 0, 1, 2, -4]) => [[-1, 0, 1]]
- threesum([-1, 0, 1, 2, -1, -4]) => [[-1, 0, 1], [-1, -1, 2]]
- threesum([-1, 0, 1, 2, -1, -4, 0, 0]) => [[0, 0, 0], [-1, 0, 1], [-1, -1, 2]]
- threesum([-1, 0, 1, 2, -3, -4, 0, 0]) => [[0, 0, 0], [-1, 0, 1], [-3, 2, -1]]
- threesum([-1, 0, 1, 2, -1, -1, -4, 0, 0]) => [[0, 0, 0], [-1, 0, 1]]
- threesum([]) => []
- threesum(undefined) => []
- threesum([-1, 0, 1, 2, -1, -1, -1, -4, 0, 0, 2]) => [[-4, 2, 2], [0, 0, 0], [-1, 0, 1], [-1, -1, 2]]

# Complexity
Time Complexity: O(n^2)
Space Complexity: O(n!/(k!(n-k)!))
