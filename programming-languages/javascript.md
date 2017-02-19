# Javascript

## ES6

A block statement is something between { }

### Variables

We have three way of declaring variables:

```javascript
var width = 100;
let height = 200;
const key = 'key';
```

The `var` keyword is the oldest one and:
- you can assign and update them
- when you update one variable we can still define the keyword `var`in front of them and it does not throw any errors (to remember in case you define two variables with the same name in the same scope)
- they are function scope or globally scope
- if you define a var inside an if statement thinking it will work as temporary variable, it will not, because is function scope and if you define the if in global scope, the variable it will leaked outside
- One way to not leaked out the variables is something called Immediately-Invoked Function Expression.
- If you use the variable before its definition you will get `undefined`

The `let` keyword:
- it is block scoped
- you can't redeclare a variable with the same name in the same scope
- you can update it
- If you use the variable before its definition you will get a not defined error. This is called temporal dead zone.

The `const` keyword:
- it is block scoped
- you can't redeclare a variable with the same name in the same scope
- you can't update it
- if you define an object you can still update its attribute. In case you want something immutable you can use`Object.freeze`
- If you use the variable before its definition you will get a not defined error. This is called temporal dead zone.

If you write something like this:
```javascript
for(var i=0; i<10; i++) {
  setTimeout(function() {
    console.log('The number is +'i);
  }, 1000);
}
```
You will display ten times `The number is 10` and because `var` is function scoped, instead if you use `let` you will display correctly the sequence because they are block scoped.

### Arrow functions
Benefits:
- They are more concise
- They have implicit return
- It does not rebind the value of `this` and inherits it from the parent
- They are anonymous function
- When you need to use `var self = this` now instead you can use an arrow function

Do not use:
- in `addEventListener` because arrow function does not rebind this and it will be `window`
- when you need to bind to an object
- when you need to add a prototype method
- when you need `arguments` object

Before:
```javascript
const names = ['a', 'b', 'c'];
const hinames = names.map(function(name) {
  return `hi ${name}`;
});
```

After:
```javascript
const names = ['a', 'b', 'c'];
const hinames = names.map(name => `hi ${name}`);
```

In case you don't have parameters:
```javascript
const hinames = names.map(() => `hi simon`);
```

### Functions
You can define default arguments: if you want to trigger one default argument pass `undefined`.

### Template strings
You can use backtick to:

- stick variables inside a string. E.g.:

```javascript
const name = 'simon';
const sentence = `hi ${name}`;
```

- to create string multiline like html fragment
- you can tag it with a function. E.g.:

```javascript
# In this case we have:
# strings = ['hi', '']
# values = ['simon']
function highlight(strings, ...values) {
  let str = ''
  strings.forEach((string, i) => {
   str += `${string} <span>${values[i] || ''}</span>`;
  });
  return str;
}

const name = 'simon';
const sentence = highlight`hi ${name}`;
```

The value of `sentence` will be `hi  <span>simon</span> <span></span>`.

### Destructuring
It allows us to extract data from an object or array. TBD
