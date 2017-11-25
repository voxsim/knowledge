## Text

## Solution
```javascript
function addBinary(x, y) {
  if(!x || !y || typeof x !== 'string' || typeof y !== 'string') return;
  
  var i=x.length-1, j=y.length-1, sum='', carry=0;
  for(;i > -1 && j > -1; i--, j--) {
    var result = (+x[i]) + (+y[j]) + carry;
    sum = ("" + result % 2) + sum;
    carry = Math.floor(result/2);
  }
  
  for(;i > -1; i--) {
    var result = (+x[i]) + carry;
    sum = ("" + result % 2) + sum;
    carry = Math.floor(result/2);
  }
  
  for(;j > -1; j--) {
    var result = (+y[j]) + carry;
    sum = ("" + result % 2) + sum;
    carry = Math.floor(result/2);
  }
  
  if(carry === 1) {
    sum = "1" + sum;
  }
  
  return sum;
}
```

## Testcase
- addBinary(undefined, undefined) => undefined
- addBinary(11, 1) => undefined
- addBinary("1", "0") => "1"
- addBinary("1", "1") => "10";
- addBinary("11", "11") => "110";
- addBinary("1000", "1") => "1001";
- addBinary("1", "1000") => "1001";

# Complexity
Time complexity: O(m+n) where x has m characters and y has n characters
Space complexity: O(1)
