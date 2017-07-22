## Text
Given a digit string, return all possible letter combinations that the number could represent.
A mapping of digit to letters (just like on the telephone buttons) is given below.
```
2 - abc
3 - def
4 - ghi
5 - jkl
6 - mno
7 - pqrs
8 - tuv
9 - wxyz
```

## Solution
```javascript
function letterCombinationsOfAPhoneNumber(digits) {
  const digitToLetters = {
    '0': [],
    '1': [],
    '2': "abc".split(''),
    '3': "def".split(''),
    '4': "ghi".split(''),
    '5': "jkl".split(''),
    '6': "mno".split(''),
    '7': "pqrs".split(''),
    '8': "tuv".split(''),
    '9': "wxyz".split('')
  };
  
  function transform(digits) {
    if(digits.length === 0) {
      return [];
    }
    
    const letters = digitToLetters[digits[0]];
    const nextResults = transform(digits.slice(1));
    if(letters.length === 0) {
      return nextResults;
    }
    if(nextResults.length === 0) {
      return letters;
    }
    let result = [];
    for(let i=0; i<letters.length; i++) {
      for(let j=0; j<nextResults.length; j++) {
        result.push([letters[i], ...nextResults[j]]);
      }
    }
    return result;
  };
  
  return transform(digits);
}
```

## Explaining

## Testcase
- letterCombinationsOfAPhoneNumber("") = []
- letterCombinationsOfAPhoneNumber("23") = ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
- letterCombinationsOfAPhoneNumber("0") = []
- letterCombinationsOfAPhoneNumber("1") = []
- letterCombinationsOfAPhoneNumber("02") = ["a", "b", "c"]
- letterCombinationsOfAPhoneNumber("20") = ["a", "b", "c"]

## Complexity
