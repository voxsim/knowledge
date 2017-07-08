## Text
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## Solution
```javascript
function mergeKSortedLists(kSortedLists) {
  let sortedList = [], indexes = [], lengths = [];
  for(let i=0; i<kSortedLists.length; i++) {
    indexes[i] = 0;
    lengths[i] = kSortedLists[i].length;
  }
  
  let min = Infinity, minIndex = 0;
  for(;minIndex >= 0;) {
    min = Infinity, minIndex = -1;
    for(let i=0; i<kSortedLists.length; i++) {
       if(indexes[i] < lengths[i] && kSortedLists[i][indexes[i]] < min) {
         min = kSortedLists[i][indexes[i]];
         minIndex = i;
       }
    }
    if(minIndex !== -1) {
      sortedList.push(kSortedLists[minIndex][indexes[minIndex]]);
      indexes[minIndex]++;
    }
  }
  return sortedList;
}
```

## Explaining

## Testcase
- mergeKSortedLists([]) = []
- mergeKSortedLists([[1]]) = [1]
- mergeKSortedLists([[1], [2]]) = [1, 2]
- mergeKSortedLists([[1, 2], [1, 2]]) = [1, 1, 2, 2]
- mergeKSortedLists([[1, 2], [2]]) = [1, 2, 2]
- mergeKSortedLists([[2], [1, 2]]) = [1, 2, 2]
- mergeKSortedLists([[2], [1, 2], []]) = [1, 2, 2]

## Complexity
O(n*k) where n is the size of the maximum list and k the number of sorted list
