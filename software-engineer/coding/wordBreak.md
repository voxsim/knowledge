## Text
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

## Solution
```javascript
function wordBreak(dict, s) {
  let isOK = false;
  for(let i=0; i<=s.length && !isOK; i++) {
    if(dict.includes(s.slice(0, i))) {
      let partialWord = s.slice(i);
      isOK = partialWord.length === 0 || wordBreak(dict, partialWord);
    }
  }
  
  return isOK;
}
```

## Explaining

## Testcase
- wordBreak(["leet", "code"], "leetcode") = true

## Complexity

