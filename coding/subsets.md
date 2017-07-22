## Text
Given a collection of distinct integers, nums, return all possible subsets. Note: The solution set must not contain duplicate subsets.

## Solution
```javascript
function subsets(values) {
  if(values.length === 0) {
    return [[]];
  }
  if(values.length === 1) {
    return [[], [values[0]]];
  }
  const sets = subsets(values.slice(0, -1));
  let length = sets.length
  sets.push([values[values.length-1]]);
  for(let i=1; i<length; i++) {
    sets.push([...sets[i], values[values.length-1]]);
  }
  return sets;
}
```

## Explaining

## Testcase
```
- subsets([]) = [[]]
- subsets([1]) = [[], [1]]
- subsets([1, 2]) = [[], [1], [2], [1, 2]]
- subsets([1, 2, 3]) = [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]
```

## Complexity
