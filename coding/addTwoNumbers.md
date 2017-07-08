

## Text
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

## Solution
```javascript
function addTwoNumbers(num1, num2) {
  let sum = null, tail = sum, curry = 0;
  for(; !!num1 && !!num2; num1 = num1.next, num2 = num2.next) {
    let partialsum = curry + num1.val + num2.val;
    if(!tail) {
      tail = {val: partialsum % 10, next: null};
      sum = tail;
    } else {
      tail.next = {val: partialsum % 10, next: null};
      tail = tail.next;
    }
    curry = Math.floor(partialsum / 10);
  }
  for(; !!num1; num1 = num1.next) {
    let partialsum = curry + num1.val;
    if(!tail) {
      tail = {val: partialsum % 10, next: null};
      sum = tail;
    } else {
      tail.next = {val: partialsum % 10, next: null};
      tail = tail.next;
    }
    curry = Math.floor(partialsum / 10);
  }
  for(; !!num2; num2 = num2.next) {
    let partialsum = curry + num2.val;
    if(!tail) {
      tail = {val: partialsum % 10, next: null};
      sum = tail;
    } else {
      tail.next = {val: partialsum % 10, next: null};
      tail = tail.next;
    }
    curry = Math.floor(partialsum / 10);
  }
  if(curry > 0) {
    tail.next = {val: curry, next: null};
  }
  console.log(sum, tail);
  if(!sum) {
    sum = {val: 0, next: null};
  }
  return sum;
}
```

## Explaining

## Testcase
- addTwoNumbers({val: 2, next: {val: 4, next: {val: 3, next: null}}}, {val: 5, next: {val: 6, next: {val: 4, next: null}}}) = {val: 7, next: {val: 0, next: {val: 8, next: null}}}
- addTwoNumbers({val: 2, next: {val: 4, next: {val: 3, next: null}}}, {val: 5, next: {val: 6, next: null}}) = {val: 7, next: {val: 0, next: {val: 4, next: null}}}
- addTwoNumbers({val: 2, next: null}, {val: 5, next: {val: 6, next: null}}) = {val: 7, next: {val: 6, next: null}}
- addTwoNumbers({val: 1, next: null}, {val: 9, next: {val: 9, next: null}}) = {val: 0, next: {val: 0, next: {val: 1, next: null}})

## Complexity
O(max(length(num1), length(num2)))
