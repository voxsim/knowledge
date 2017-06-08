## Text
Design a data structure that supports the following two operations:
- void addWord(word)
- bool search(word): search(word) can search a literal word or a regular expression string containing only letters a-z or `.` . 
  A `.` means it can represent any one letter.
  
For simplicity the data structure will supports only lower-case letters.

## Solution
```javascript
class WordDictionary {
  constructor() {
    this.trie = {data: '', children: {}, final: false};
  }
  
  addWord(word) {
    if(typeof word !== 'string' || !/^[a-z]*$/.test(word))
      throw 'addWord accepts only strings that have lower case letters';
    
    var node = this.trie;
    for(var i=0; i<word.length; i++) {
      if(!node.children[word[i]]) {
        node.children[word[i]] = { data: word[i], children: {}, final: false };
      }
      node = node.children[word[i]];
    }
    node.final = true;
  }
  
  search(word, node = undefined) {
    if(typeof word !== 'string' || !/^[a-z.]*$/.test(word))
      throw 'search accepts only strings that have lower case letters or points';
    
    if(!node && word.length === 0) {
      return this.trie.final;
    }
    
    if(!node) {
      node = this.trie;
    }
    
    if(word[0] === '.') {
      for(var letter in node.children) {
        if(word.length === 1 && node.children[letter].final) {
          return true;
        } else if(word.length > 1 && this.search(word.slice(1), node.children[letter])) {
          return true;
        }
      }
      return false;
    }
    
    if(!node.children[word[0]]) {
      return false;
    }
    
    if(word.length === 1) {
      return node.children[word[0]].final;
    }
    
    return this.search(word.slice(1), node.children[word[0]]);
  }
}
```

## Testcase

# Complexity

- var wordDictionary = new WordDictionary();
- wordDictionary.addWord("bad")
- wordDictionary.addWord("dad")
- wordDictionary.addWord("mad")
- wordDictionary.search("pad") -> false
- wordDictionary.search("bad") -> true
- wordDictionary.search(".ad") -> true
- wordDictionary.search("b..") -> true
- wordDictionary.search("b") -> false
- wordDictionary.search('') -> false
- wordDictionary.addWord('')
- wordDictionary.search('') -> true

- wordDictionary.addWord(undefined) -> error
- wordDictionary.search(undefined) -> error
- wordDictionary.addWord('A') -> error
- wordDictionary.search('A') -> error
- wordDictionary.addWord(1) -> error
- wordDictionary.search(1) -> error
- wordDictionary.addWord('.') -> error
