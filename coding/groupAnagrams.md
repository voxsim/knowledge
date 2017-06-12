## Text
Given an array of strings, group anagrams together. Note: All inputs will be in lower-case.

## Solution
```javascript
function groupAnagrams(array) {
  var result = {};
  for(var i=0; i<array.length; i++) {
    var key = array[i].split('').sort().join('');
    if(!(key in result)) {
      result[key] = [];
    }
    result[key].push(array[i]);
  }
  return Object.values(result);
}
```

## Testcase
For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]

## Complexity
