## Text
Given a collection of integers that might contain duplicates, nums, return all possible subsets. Note: The solution set must not contain duplicate subsets.

## Solution
```javascript
// We assume that the col lection is sorted otherwise we can run A.sort((a, b) => a - b); before
function subsetsII(values) {
  if(values.length === 0) {
    return [[]];
  }
  if(values.length === 1) {
    return [[], [values[0]]];
  }
  let j = values.length-2;
  let duplicates = 1;
  for(; j >= -1 && values[j] === values[values.length-1]; j--, duplicates++);
  let sets = subsetsII(values.slice(0, j+1));
  console.log(sets, j, duplicates);
  const length = sets.length;
  let value = [];
  for(let k=0; k<duplicates; k++) {
    value.push(values[values.length-1]);
    for(let i=1; i<length; i++) {
      sets.push([...sets[i], ...value]);
    }
    sets.push([...value]);
  }
  return sets;
}
```

## Explaining

## Testcase
```
For example,
If nums = [1,2,2], a solution is:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
- subsetsII([]) = [[]]
- subsetsII([1]) = [[], [1]]
- subsetsII([1, 1]) = [[], [1], [1, 1]]
- subsetsII([1, 2]) = [[], [1], [2], [1, 2]]
- subsetsII([1, 1, 1]) = [[], [1], [1, 1], [1, 1, 1]]
- subsetsII([1, 1, 2]) = [[], [1], [2], [1, 1], [1, 2], [1, 1, 2]]
- subsetsII([1, 2, 2]) = [[], [1], [2], [1, 2], [2, 2], [1, 2, 2]]

## Complexity
