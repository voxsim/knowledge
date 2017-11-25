## Text
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

## Solution
```javascript
function validParentheses(input) {
  if(input.length === 0) {
    return true;
  }
  
  const open_parantheses = ['(', '[', '{'];
  const close_parantheses = [')', ']', '}'];
  
  let last_open_parantheses = [];
  for(let i=0; i<input.length; i++) {
     if(open_parantheses.indexOf(input[i]) != -1) {
       last_open_parantheses.push(input[i]);
     } else {
       let index = close_parantheses.indexOf(input[i]);
       if(last_open_parantheses.length === 0 || last_open_parantheses.pop() !== open_parantheses[index]) {
         return false;
       }
     }
  }
  
  return last_open_parantheses.length === 0;
}
```

## Explaining

## Testcase
- validParentheses('') = true
- validParentheses('(') = false
- validParentheses('[') = false
- validParentheses('{') = false
- validParentheses(')') = false
- validParentheses(']') = false
- validParentheses('}') = false
- validParentheses('()') = true
- validParentheses('[]') = true
- validParentheses('{}') = true
- validParentheses('()[]{}') = true
- validParentheses('{[()]}') = true
- validParentheses('(]') = false
- validParentheses('([)]') = false

## Complexity
