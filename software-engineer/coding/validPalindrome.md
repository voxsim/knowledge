## Text
Check if a palindrome is valid

## Solution
```javascript
function validPalindrome(arr) {
  let isValid = true;
  for(let i=0; i<Math.floor(arr.length/2) && isValid; i++) {
    isValid = isValid && arr[i] === arr[arr.length - i - 1];
  }
  return isValid;
}
```

## Explaining

## Testcase
- validPalindrome([]) = true
- validPalindrome([1]) = true
- validPalindrome([1, 1]) = true
- validPalindrome([1, 2, 1]) = true
- validPalindrome([1, 2]) = false
- validPalindrome([1, 2, 2]) = false

## Complexity
O(n/2)
