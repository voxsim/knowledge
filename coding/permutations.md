## Text
Given an array A, return a set with every permutation of that array

## Solution

```javascript
function permute(A){
  if(!A) return;
  if(A.length <= 1) return [A];

  var permutations = this.permute(A.slice(1));
  var results = [];

  for(var i=0; i<permutations.length; i++) {
    results.push([A[0]].concat(permutations[i]));
  }

  for(var i=0; i<permutations.length; i++) {
    for(var j=1; j<A.length; j++) {
      results.push(permutations[i].slice(0, j).concat([A[0]]).concat(permutations[i].slice(j)));
    }
  }
  return results;
}
```

## Testcase

# Complexity


