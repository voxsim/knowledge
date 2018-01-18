# Pointfree

It means functions that never mention the data upon which they operate.

First class functions, currying, and composition all play well together to create this style. 

```javascript
//not pointfree because we mention the data: word
var snakeCase = function(word) {   return word.toLowerCase().replace(/\s+/ig, '_'); };

//pointfree
var snakeCase = compose(replace(/\s+/ig, '_'), toLowerCase)(word);

// with |> (pipe) operator
var snakeCase = word |> toLowerCase |> replace(/\s+/ig, '_')
```
