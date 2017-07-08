## Text
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

## Solution
```javascript
function mergeSortedArray(num1, num2) {
  let i=0, j=0, merged = [];
  for(; i<num1.length && j < num2.length;) {
    if(num1[i] <= num2[j]) {
      merged.push(num1[i]);
      i++;
    } else {
      merged.push(num2[j]);
      j++;
    }
  }
  for(; i<num1.length; i++) {
    merged.push(num1[i]);
  }
  for(; j<num2.length; j++) {
    merged.push(num2[j]);
  }
  return merged;
}
```

## Explaining

## Testcase
- mergeSortedArray([1], [2]) = [1, 2]
- mergeSortedArray([1], [1]) = [1, 1]
- mergeSortedArray([1], [1, 2]) = [1, 1, 2]
- mergeSortedArray([1, 3], [2]) = [1, 2, 3]
- mergeSortedArray([2], [1, 3]) = [1, 2, 3]

## Complexity
O(max(length(num1), length(num2)))
