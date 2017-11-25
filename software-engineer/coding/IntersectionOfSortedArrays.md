## Text
Implement a function which gets the intersection of two sorted arrays. Assuming numbers in each array are unique.
For example, if the two sorted arrays as input are {1, 4, 7, 10, 13} and {1, 3, 5, 7, 9}, it returns an intersection array with numbers {1, 7}.

## Solution
```javascript
function intersection(A, B) {
  if(!A || !B) return;

  var result = [];
  for(var i=0, j=0; i<A.length && j < B.length; ) {
    if(A[i] === B[j]) {
      result.push(A[i]);
      i++;
      j++;
    } else if(A[i] < B[j]) {
       i++;
    } else {
       j++;
    }

 }
 return result;
}
```

## Testcase

## Complexity
- O(m+n)
- for m >> n, complexity O(nlogm), for each number of A we use binary_search on B.
