## Text
Given a collection of intervals, merge all overlapping intervals.

## Solution
```javascript
function mergeIntervals(A) {
  A.sort(function(a, b) { return a[0] - b[0] });
  var intervals = [A[0]];
  
  for(var i = 1; i<A.length; i++) {
    if(intervals[intervals.length-1][1] >= A[i][0]) {
      intervals[intervals.length-1][1] = Math.max(intervals[intervals.length-1][1], A[i][1]);
    } else {
      intervals.push(A[i]);
    }
  }
  
  return intervals;
}
```

## Testcase
- mergeIntervals([[1, 3], [2, 4]]) = [[1, 4]]
- mergeIntervals([[2, 4], [1, 3]]) = [[1, 4]]
- mergeIntervals([[1,3],[2,6],[8,10],[15,18]]) = [[1,6],[8,10],[15,18]]

## Complexity
O(n)
