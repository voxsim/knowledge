An algorithm that searches a value divinding constantly the space in two.

Recursive approach:
```javascript
function binary_search(array, valueToSearch, begin=0, end=array.length-1) {
  if(end === 0) {
    return -1;
  }
  
  const mid = Math.floor(begin + (end - begin)/2);
  if(array[mid] === valueToSearch) {
    return mid;
  }
  
  if(array[mid] > valueToSearch) {
    return binary_search(array, valueToSearch, mid+1, end);
  }
  
  return binary_search(array, valueToSearch, 0, mid-1);
}
```

Iterative approach:
```javascript
function binary_search(array, valueToSearch, begin=0, end=array.length-1) {
  for(;begin <= end;) {
    const mid = Math.floor(begin + (end - begin)/2);
    if(array[mid] === valueToSearch) {
      return mid;
    }
    
    if(array[mid] < valueToSearch) {
      begin = mid + 1;
    } else {
      end = mid - 1;
    }
  }
  
  return -1;
}
```
