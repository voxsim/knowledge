## Text
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
Note: If there is no such window in S that covers all characters in T, return the empty string "". If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

## Solution
```javascript
function minimumWindowSubstring(S, T) {
  if(T.length === 0) {
    return '';
  }
  
  if(T.length > S.length) {
    return '';
  }
  
  if(S === T) {
    return S;
  }
  
  let map = {}, limitMap = {}, salients = [], minimumWindow = S;
  for(let i=0; i<T.length; i++) {
    map[T[i]] = 0;
    if(typeof limitMap[T[i]] === 'undefined') {
      limitMap[T[i]] = 1;
    } else {
      limitMap[T[i]]++;
    }
  }
  
  for(var i=0; i<S.length; i++) {
    // console.log(S[i], map[S[i]], salients, map, limitMap);
    if(typeof map[S[i]] === 'undefined') {
      continue;
    }
    map[S[i]]++;
    for(;map[S[salients[0]]] > limitMap[S[salients[0]]];) {
      map[S[salients[0]]]--;
      salients.shift();
    }
    salients.push(i);
    if(salients.length >= T.length) {
      let possibleMinimumWindow = S.slice(salients[0], salients[salients.length - 1] + 1);
      console.log(possibleMinimumWindow);
      if(possibleMinimumWindow.length < minimumWindow.length) {
        minimumWindow = possibleMinimumWindow;
      }
    }
  }
  
  return minimumWindow === S ? '' : minimumWindow;
}
```

## Testcase
- minimumWindowSubstring('A', 'A') = 'A'
- minimumWindowSubstring('A', '') = ''
- minimumWindowSubstring('', 'A') = ''
- minimumWindowSubstring('AB', 'A') = 'A'
- minimumWindowSubstring('AB', 'B') = 'B'
- minimumWindowSubstring('ADOBECODEBANC', 'ABC') = 'BANC'
- minimumWindowSubstring('AAB', 'AA') = 'AA'

## Complexity
O(n) if we use a queue for salients.
