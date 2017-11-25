## Text
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).
You may assume that the intervals were initially sorted according to their start times.

## Solution
```javascript
function insertInterval(oldIntervals, newInterval) {
  let intervals = [], newStart = newInterval[0], newEnd = newInterval[1];
  for(let i=0; i<oldIntervals.length; i++) {
    if(oldIntervals[i][1] < newInterval[0]) {
      intervals.push(oldIntervals[i]);
    } else if(oldIntervals[i][0] > newInterval[1]) {
      intervals.push([newStart, newEnd]);
      intervals.push(oldIntervals[i]);
    } else {
      newStart = Math.min(oldIntervals[i][0], newStart);
      newEnd = Math.max(oldIntervals[i][1], newEnd);
    }
  }
  return intervals;
}
```

## Explaining

## Testcase
- insertInterval([[1,3],[6,9]], [2,5]) = [[1,5],[6,9]]
- insertInterval([[1,3],[6,9]], [4,5]) = [[1,3],[4,5],[6,9]]
- insertInterval([[1,2],[3,5],[6,7],[8,10],[12,16]], [4,9]) = [[1,2],[3,10],[12,16]]

## Complexity
O(n)
