An algorithm that searches a value divinding constantly the space in two.

Recursive approach:
```javascript
function binary_search(array, valueToSearch) {
  if(array.length === 0) {
    return;
  }
  if(array.length === 1) {
    return valueToSearch === array[0] ? 0 : undefined;
  }

  const mid = Math.ceil(array.length/2);
  if(array[mid] === valueToSearch) {
    return mid;
  } else {
    if(valueToSearch > array[mid]) {
      let result = binary_search(array.slice(mid), valueToSearch);
      return result ? mid + result : result;
    } else {
      return binary_search(array.slice(0, mid), valueToSearch);
    }
  }
}
```

Iterative approach:
```javascript
function binary_search(array, valueToSearch) {
  let low = 0;
  let high = array.length;

  for(;low <= high;) {
    const mid = Math.ceil((low + high)/2);
    if(array[mid] === valueToSearch) {
      return mid;
    } else {
      if(valueToSearch > array[mid]) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
  }
}
```
