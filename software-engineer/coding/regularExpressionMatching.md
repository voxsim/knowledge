## Text
Implement regular expression matching with support for '.' and '*'.
- '.' Matches any single character
- '*' Matches zero or more of the preceding element

The matching should cover the entire input string (not partial).

## Solution
```javascript
function isMatch(string, pattern) {
  if(typeof string !== 'string' || typeof pattern !== 'string') {
    return false;
  }
  
  if(string === '' && pattern === '') {
    return true;
  }
  
  if(string === '' && pattern !== '') {
    return false;
  }
  
  if(string !== '' && pattern === '') {
    return false;
  }
  
  if(pattern[0] === '*') {
    return false;
  }
  
  var i=0, j=0;
  for(; i<string.length && j<pattern.length;) {
    if(string[i] === pattern[j]) {
      if(pattern[j+1] === '*') {
        for(; i<string.length && string[i] === pattern[j]; i++);
        j = j+2;
      } else {
        i++;
        j++;
      }
    } else if(pattern[j] === '.') {
      if(pattern[j+1] === '*') {
        return true;
      } else {
        i++;
        j++;
      }
    } else if(pattern[j+1] === '*') {
      j = j+2;
    } else {
      return false;
    }
  }
  
  return i === string.length && j === pattern.length;
}
```

## Testcase
- isMatch("aa","a") → false
- isMatch("aa","aa") → true
- isMatch("aaa","aa") → false
- isMatch("aa", "a*") → true
- isMatch("aa", ".*") → true
- isMatch("ab", ".*") → true
- isMatch("aab", "c*a*b") → true

# Complexity
O(max(m,n)) where string has m characters and pattern has n characters
