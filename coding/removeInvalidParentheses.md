## Text
Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.
Note: The input string may contain letters other than the parentheses ( and ).

## Solution
```javascript
function removeInvalidParentheses(expression) {
  let opens = [], closes = [];
  for(let i=0; i<expression.length; i++) {
    if(expression[i] === '(') {
      opens.push(i);
    } else if(expression[i] === ')') {
      closes.push(i);
    }
  }
}
```

## Explaining

## Testcase
- removeInvalidParentheses("()())()") = ["()()()", "(())()"]
- removeInvalidParentheses("()()())") = ["()()()", "()(())", "(()())"]
- removeInvalidParentheses("()())())") = ["()()()", "(())()"]
- removeInvalidParentheses("(a)())()") = ["(a)()()", "(a())()"]
- removeInvalidParentheses(")(") -> [""]
- removeInvalidParentheses(")") -> [""]
- removeInvalidParentheses("(") -> [""]
- removeInvalidParentheses("())") -> ["()"]
- removeInvalidParentheses("()(") -> ["()"]

## Complexity
