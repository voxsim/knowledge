## Text
A message containing letters from A-Z is being encoded to numbers using the following mapping:
- 'A' -> 1
- 'B' -> 2
- ...
- 'Z' -> 26

Given an encoded message containing digits, determine the total number of ways to decode it.

## Solution
Determine all encoded messages
```javascript
function decodeWays(n) {
  var chars = {};
  
  for(var i=1; i<27; i++) {
    if(i < 10 || i % 10 === 0) {
      chars[""+i] = [String.fromCharCode(64+i)];
    } else {
      chars[""+i] = [String.fromCharCode(64+i), chars[Math.floor(i/10)]+chars[i%10]];
    }
  }
  var cache = {};
  
  return function decode(n) {
    if(n in chars) return chars[n];
    if(n in cache) return cache[n];
    
    var result = [];
    var decodes = decode(n.slice(1));
    for(var i=0; i<decodes.length; i++) {
      result.push(chars[n[0]] + decodes[i]);
    }
    var pre = n.slice(0, 2);
    if(pre in chars) {
      var decodes = decode(n.slice(2));
      for(var i=0; i<decodes.length; i++) {
        result.push(chars[pre][0] + decodes[i]);
      }
    }
    return result;
  }(n);
}
```

Determine only the number of ways of encoding
```
function decodeWays(n) {
  if(n === '0') return 0;
  
  var l = n.length;
  var dp = {};
  dp[0] = 1;
  var pre = +n.slice(0, 2)
  dp[1] = pre >= 10 && pre <= 26 ? 2 : 1;
  
  if(n[1] === '0') {
    dp[1] -= 1;
  }
  
  for(var i=2; i<l; i++) {
     if(n[i] === '0') {
       dp[i] = 0;
       continue;
     }
     
     dp[i] = dp[i-1];
     var pre = +n.slice(0, 2);
     if(pre >= 10 && pre <= 26)
       dp[i] += dp[i-2];
  }
  
  return dp[l-1];
}
```

## Testcase
For example, Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

- decodeWays('1') => ['A']
- decodeWays('11') => ['K', 'AA']
- decodeWays('20') => ['T']
- decodeWays('21') => ['U', 'BA']
- decodeWays('31') => ['CA']
- decodeWays('311') => ['CI', 'CAA']
- decodeWays('111') => ['AK', 'KA', 'AAA']
- decodeWays('1111') => ['AAK', 'KAA', 'AAAA', 'AKA', 'KK']

## Complexity





