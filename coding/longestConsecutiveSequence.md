## Text
Given an unsorted array of integers, find the length of the longest consecutive elements sequence

## Solution
```javascript
function longestConsecutiveSequence(array) {
  var map = {};
  var max = 0;
  
  for(var i=0; i<array.length; i++) {
    if(!(array[i] in map)) {
      var r = 1;
      if((array[i]-1) in map) {
        r += map[array[i]-1];
      }
      if((array[i]+1) in map) {
        r += map[array[i]+1];
      }
      max = Math.max(max, r);
      map[array[i]] = r;
    }
  }
  
  return max;
}
```

## Testcase
- longestConsecutiveSequence([100, 4, 200, 1, 3, 2]) => 4

## Complexity
O(n)
