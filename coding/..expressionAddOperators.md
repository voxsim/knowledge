## Text
Given a string that contains only digits 0-9 and a target value, return all possibilities to add binary operators (not unary) +, -, or * between the digits so they evaluate to the target value.

## Solution
```javascript
function helper(result, digits, target, path, current, index, multed, number) {
  console.count(digits);
  console.log(path);
  if(index === digits.length) {
    if(current === target) {
      result.push(path);
    }
    return;
  }
  helper(result, digits, target, path + '+' + digits[index], current + (+digits[index]), index+1, (+digits[index]), (+digits[index]));
  helper(result, digits, target, path + '-' + digits[index], current - (+digits[index]), index+1, -(+digits[index]), -(+digits[index]));
  helper(result, digits, target, path + '*' + digits[index], current - multed + multed * (+digits[index]), index+1, multed * (+digits[index]), (+digits[index]));
  if(current !== 0) {
    helper(result, digits, target, path + digits[index], current - number + number * 10 + (+digits[index]), index+1, multed * (+digits[index]), number * 10 + (+digits[index]));
  }
}

function expressionAddOperators(digits, target) {
  var result = [];
  helper(result, digits, target, digits[0], +digits[0], 1, +digits[0], +digits[0]);
  return result;
}
```

## Testcase
- expressionAddOperators('1', 1) = ['1']
- "123", 6 -> ["1+2+3", "1*2*3"] 
- "232", 8 -> ["2*3+2", "2+3*2"]
- "105", 5 -> ["1*0+5","10-5"]
- "00", 0 -> ["0+0", "0-0", "0*0"]
- "3456237490", 9191 -> []

## Complexity
O(4^n)
