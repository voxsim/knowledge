## Text
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

## Solution
```javascript
function removeDuplicatesFromSortedArray(arr) {
  if(arr.length === 0) return [0, arr];
  
  let lastNotDuplicate = 0, length = 1;
  for(let i=1; i<arr.length; i++) {
    if(arr[i] != arr[lastNotDuplicate]) {
      if(i === lastNotDuplicate+1) {
        lastNotDuplicate = i;
      } else {
        lastNotDuplicate++;
        arr[i] = arr[i] + arr[lastNotDuplicate];
        arr[lastNotDuplicate] = arr[i] - arr[lastNotDuplicate];
        arr[i] = arr[i] - arr[lastNotDuplicate];
      }
      length++;
    }
  }
  return [length, arr];
}
```

## Explaining
We memorize our last not duplicates, so every time we meet a new unique value if it is successive of the last one we just increase a count, otherwise we switch in place with the next of the last one.

## Testcase
- removeDuplicatesFromSortedArray([]) = [0, []]
- removeDuplicatesFromSortedArray([1]) = [1, [1]]
- removeDuplicatesFromSortedArray([1,1,2]) = [2, [1,2,1]]
- removeDuplicatesFromSortedArray([1,2,2]) = [2, [1,2,2]]
- removeDuplicatesFromSortedArray([1,1,2,2]) = [2, [1,2,1,2]]

## Complexity
O(n)
