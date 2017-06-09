## Text
The count-and-say sequence is the sequence of integers beginning as follows:
1, 11, 21, 1211, 111221, ...
- 1 is read off as "one 1" or 11.
- 11 is read off as "two 1s" or 21.
- 21 is read off as "one 2, then one 1" or 1211.
- Given an integer n, generate the nth sequence.
Note: The sequence of integers will be represented as a string.

## Solution
```javascript
function countAndSay(n) {
  if(n <= 1) return '1';
  
  var prev = countAndSay(n-1);
  var result = '';
  var count = 1;
  var character = prev[0];
  for(var i=1; i<prev.length; i++) {
    if(character !== prev[i]) {
      result += count + character;
      count = 1;
      character = prev[i];
    } else {
      count++;
    }
  }
  
  return result + count + character;
}
```

## Testcase

# Complexity


