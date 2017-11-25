## Text
Given two strings S and T, determine if they are both one edit distance apart.

## Solution
```javascript
function oneEditDistance(S, T) {
  if(typeof S !== 'string' || typeof T !== 'string') {
    return false;
  }
  
  if(Math.abs(S.length - T.length) > 1) {
    return false;
  }
  
  for(let i=0; i<Math.min(S.length, T.length); i++) {
     if(S[i] !== T[i]) {
       return S.slice(i+1) === T.slice(i+1) ||
         S.slice(i+1) === T.slice(i) ||
         S.slice(i) === T.slice(i+1);
     }
  }
  
  return Math.abs(S.length - T.length) === 1;
}
```

## Testcase
- oneEditDistance(null, 'a') = false OK
- oneEditDistance('a', null) = false OK
- oneEditDistance(null, null) = false OK
- oneEditDistance('a', 'b') = true OK
- oneEditDistance('ac', 'bc') = true OK
- oneEditDistance('ca', 'cb') = true OK
- oneEditDistance('a', 'ba') = true
- oneEditDistance('a', 'ab') = true OK
- oneEditDistance('a', '') = true OK
- oneEditDistance('ab', 'a') = true OK
- oneEditDistance('abb', 'a') = false OK
- oneEditDistance('a', 'a') = false OK

## Complexity
O(n)
