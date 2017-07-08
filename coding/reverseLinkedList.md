## Text
Reverse a singly linked list.

## Solution
```javascript
function helper(node) {
  if(!node.next) {
    return {head: node, tail: node};
  }
  
  var next = node.next;
  node.next = null;
  var obj = helper(next);
  obj.tail.next = node;
  return {head: obj.head, tail: node};
}

function reverseLinkedList(node) {
   return helper(node).head;
}
```

## Explaining

## Testcase
- reverseLinkedList({val: 1, next: null}) = {val: 1, next: null}
- reverseLinkedList({val: 1, next: {val: 2, next: null}}) = {val: 2, next: {val: 1, next: null}}
- reverseLinkedList({val: 1, next: {val: 2, next: {val: 3, next: null}}}) = {val: 3, next: {val: 2, next: {val: 1, next: null}}}

## Complexity
O(n)
