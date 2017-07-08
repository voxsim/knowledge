## Text
Given a roman numeral, convert it to an integer.
Input is guaranteed to be within the range from 1 to 3999

## Solution
```javascript
function romanToInteger(roman) {
  if(roman.length === 0) return 0;
  let map = {
    'I': 1,
    'V': 5,
    'X': 10,
    'L': 50,
    'C': 100,
    'D': 500,
    'M': 1000
  };
  
  let integer = map[roman[0]], last = map[roman[0]];
  for(let i=1; i<roman.length; i++) {
    if(map[roman[i]] > last) {
      integer += map[roman[i]] - last * 2;
    } else {
      integer += map[roman[i]];
    }
    last = map[roman[i]];
  }
  return integer;
}
```

## Explaining

## Testcase
- romanToInteger('I') = 1
- romanToInteger('III') = 3
- romanToInteger('V') = 5
- romanToInteger('IV') = 4
- romanToInteger('VI') = 6
- romanToInteger('IX') = 9
- romanToInteger('X') = 10
- romanToInteger('XI') = 11
- romanToInteger('XIV') = 14
- romanToInteger('XV') = 15

## Complexity
O(n)
