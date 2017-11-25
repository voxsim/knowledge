## Text
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library's sort function for this problem.

## Solution
```javascript
function sortColors(arr) {
  let map = { 0: [], 1: [], 2: [] };
  for(let i=0; i<arr.length; i++) {
    map[arr[i]].push(arr[i]);
  }
  return [...map[0], ...map[1], ...map[2]];
}
```

## Explaining

## Testcase
- sortColors([0, 1, 2]) = [0, 1, 2];
- sortColors([0, 1, 2, 1]) = [0, 1, 1, 2];

## Complexity
O(n)
