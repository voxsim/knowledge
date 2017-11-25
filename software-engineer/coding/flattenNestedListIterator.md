## Text
Given a nested list of integers, implement an iterator to flatten it.

## Solution
```javascript
function flattenNestedListIterator(array) {
  function flatten(array) {
    var result = [];
    for(var i=0; i<array.length; i++) {
      if(Array.isArray(array[i])) {
        result = result.concat(flatten(array[i]));
      } else {
        result.push(array[i]);
      }
    }
    return result;
  }
  return {
    memory: flatten(array),
    index: 0,
    next: function() { return this.hasNext() ? this.memory[this.index++] : undefined; },
    hasNext: function() { return this.index < this.memory.length; }
  }
}
```

## Testcase
Given the list [[1,1],2,[1,1]] by calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].
Given the list [1,[4,[6]]] by calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6]. 

## Complexity
