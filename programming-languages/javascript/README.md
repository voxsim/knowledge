# Javascript

## Identifiers
- Starts with a letter or _ or $
- Followed by zero or more letters, digits, _ or $
- By convention all variables starts with lowercase letter
- Constructor functions start with uppercase letter
- Initial _ should be reserved for implementation
- $ should be reserved for machines

## Scoping
In JavaScript, functions are our de facto scope delimiters for declaring vars, which means that usual blocks from loops and conditionals (such as if, for, while, switch and try) DON'T delimit scope, unlike most other languages. Therefore, those blocks will share the same scope as the function which contains them. This way, it might be dangerous to declare vars inside blocks as it would seem the var belongs to that block only.

## Hoisting
On runtime, all var and function declarations are moved to the beginning of each function (its scope) - this is known as Hoisting. Having said so, it is a good practice to declare all the vars altogether on the first line, in order to avoid false expectations with a var that got declared late but happened to hold a value before - this is a common problem for programmers coming from languages with block scope.

```javascript
/* Function declaration */

foo(); // "bar"

function foo() {
  console.log('bar');
}


/* Function expression */

baz(); // TypeError: baz is not a function

var baz = function() {
  console.log('bar2');
};
```

## Statements
- A block statement is something between { }
- A function statement is something inside a function

## Primitive types
There are seven primitive types: null, undefined, Number, String, Boolean, Object, Symbol.

### null
The value null is written with a literal: null. null is not an identifier for a property of the global object, like undefined can be. Instead, null expresses a lack of identification, indicating that a variable points to no object. 

```
+null // 0
typeof null        // "object" (not "null" for legacy reasons)
typeof undefined   // "undefined"
null === undefined // false
null  == undefined // true
null === null //true
null == null //true
!null // true
isNaN(1 + null) //false
isNaN(1 + undefined) //true
```

### undefined
- a value that isn't even that
- the default value for variables and parameters
- the value of missing members in objects

```
+undefined // NaN
```

### Number
- Immutable
- 64 bit floating point
- IEEE-754 (aka "Double")
- Associative law does not hold: (a + b) + c === a + (b + c).
Produce false for some values of a, b, c, e.g. decimal fractions, big integers

#### NaN
- Special number: Not a Number
- It is result of undefined or erronous operations
- Toxic: any operations with NaN as an input will have NaN as output
- NaN is not equal to anything, including NaN itself

### String
- Immutable
- A sequence of 0 or more 16-bit Unicode characters
- No separate type for character type (they are just string with length 1)
- Strings are immutable
- Similar string are equal (===)
- String literals can use single/double quotes with \ for escapment

#### Template strings
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

### Boolean
- Immutable
- literal form: true, false

### Object

#### Prototype
Every JavaScript object has a prototype. The prototype is also an object.
All JavaScript objects inherit their properties and methods from their prototype.
The standard way to create an object prototype is to use an object constructor function.
With a constructor function, you can use the new keyword to create new objects from the same prototype.

#### Object literal
An expressive notation to define object.

```JavaScript
var obj = {
    // __proto__
    __proto__: theProtoObj,
    // Shorthand for ‘handler: handler’
    handler,
    // Methods
    toString() {
     // Super calls
     return "d " + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};
```

#### Get, set and delete
- get
  object.name
  object[expression]

- set
  object.name = value
  object[expression] = value

- delete
  delete object.name
  delete object[expression]

#### Properties
A property is a named collection of attribute
- value -> any Javascript value
- writeble -> boolean
- enumerable -> boolean
- configurable -> boolean
- get -> function() { ... return value }
- set -> function(value) { ... }

#### New operator
```javascript
function new(func, arguments) {
  var that = Object.create(func.prototype),
      result = func.apply(that, arguments);
  return (typeof result === 'object' && result) || that;
}
```

#### Reference
Objects can be passed as arguments to functions, and can be returned by functions
- Objects are passed by references
- Objects are not passed by value
The === operator compares object references, not values (true if only it is the same object)
Loosely typed: any of these can be stored in a variable, or passed as a parameter to any function, the language is not "untyped"

#### Array
- Array inherits from Object
- Indexes are converted to strings and used as names for retrieving values
- Very efficient for sparse array
- Not very efficient in most of other cases
- One advantage: No need to provide a length or type when creating an array
- Literal form: []
- It can contain any number of expressions separated by commas
- New items can be appendend
- The dot notation should be not used by arrays

sort myArray:
-> it sorts alphabetically (everything number too, but we can pass a function in sort)

delete myArray[1];
-> it puts undefined in number 1 index;
-> we need to use splice to delete the element and resize the array

## typeof
- object -> 'object'
- function -> 'function'
- array -> 'object' ???
- number -> 'number'
- string -> 'string'
- boolean -> 'boolean'
- null -> 'object' ???
- undefined -> 'undefined'

## Falsy values
- false
- null
- undefined
- ""
- 0
- NaN
- all other values (including objects) are thruthy, e.g. "0", "false"

Thruthy means that if you put in if statemnt it will go in the then branch, otherwise falsy means that it will go in the else branch

## Variables
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
- the statement gets split into two parts:
  - the declaration part gets hoisted to the top of the function, initializing with undefined
  - the initialization part turns into an ordinary assignment
- if you define a variable without var it will be attached to the global object window

```javascript
var myvar = 0;
```

became

```javascript
var myvar = undefined;

myvar = 0;
```

the `let` keyword:
- it is block scoped
- you can't redeclare a variable with the same name in the same scope
- you can update it
- if you use the variable before its definition you will get a not defined error. this is called temporal dead zone.

If you write something like this:
```javascript
for(var i=0; i<10; i++) {
  setTimeout(function() {
    console.log('The number is +'i);
  }, 1000);
}
```
You will display ten times `The number is 10` and because `var` is function scoped, instead if you use `let` you will display correctly the sequence because they are block scoped.

The `const` keyword:
- it is read only variable. I. e. you can't update it.
- it is block scoped
- you can't redeclare a variable with the same name in the same scope
- if you define an object you can still update its attribute. In case you want something immutable you can use`Object.freeze`
- If you use the variable before its definition you will get a not defined error. This is called temporal dead zone.

## Functions
- if a function is called with too many arguments, the extra args are ignored
- if a function is called with few parameters, the remains will be setted to undefined
- no type checking on parameters

### Invocation
There are four ways to invoke functions in javascript. You can invoke the function as a method, as a function, as a constructor, and with apply/call.

#### As a Method

A method is a function that's attached to an object

```javascript
var foo = {};
foo.someMethod = function(){
    alert(this);
}
```

When invoked as a method, this will be bound to the object the function/method is a part of. In this example, this will be bound to foo.

#### As A Function

If you have a stand alone function, the this variable will be bound to the "global" object, almost always the window object in the context of a browser.

```javascript
 var foo = function(){
    alert(this);
 }
 foo();
```
 
This may be what's tripping you up, but don't feel bad. Many people consider this a bad design decision. Since a callback is invoked as a function and not as a method, that's why you're seeing what appears to be inconsistent behavior.

Many people get around the problem by doing something like, um, this

```javascript
var foo = {};
foo.someMethod = function (){
    var that=this;
    function bar(){
        alert(that);
    }
}
```

You define a variable that which points to this. Closure (a topic all it's own) keeps that around, so if you call bar as a callback, it still has a reference.

Another way to attach a different object to this is `bind`: it attaches this into function and it needs to be invoked separately like this:
```javascript
var person = {
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

var helloFunc = person.hello.bind(person);
helloFunc("world");  // output: "James Smith says hello world"
```

Its implementation:
```javascript
Function.prototype.bind = function(){ 
  var fn = this, args = Array.prototype.slice.call(arguments), object = args.shift(); 
  return function(){ 
    return fn.apply(object, 
      args.concat(Array.prototype.slice.call(arguments))); 
  }; 
};
```

### As a Constructor

You can also invoke a function as a constructor. Based on the naming convention you're using (TestObject) this also may be what you're doing and is what's tripping you up.

You invoke a function as a Constructor with the new keyword.

```javascript
function Foo(){
    this.confusing = 'hell yeah';
}
var myObject = new Foo();
```

When invoked as a constructor, a new Object will be created, and this will be bound to that object. Again, if you have inner functions and they're used as callbacks, you'll be invoking them as functions, and this will be bound to the global object. Use that var that = this trick/pattern.

Some people think the constructor/new keyword was a bone thrown to Java/traditional OOP programmers as a way to create something similar to classes.

### With the Apply/Call Method.

Finally, every function has two methods (yes, functions are objects in Javascript) named "apply" and "call". 

Apply lets you determine what the value of this will be, and also lets you pass in an array of arguments.

```javascript
var person = {
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

person.hello.apply(person, ["world"]); // output: "James Smith says hello world"

Call is the same but we do not pass an array, but a list of arguments.

```javascript
var person = {
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

person.hello.call(person, "world"); // output: "James Smith says hello world"
```

### Function expression
- Produce an instance of a function object
- Function object are first class object
- Function objects inherit from Function.prototype
- Also called closures

### Function statement
- the function statement is just a short-hand for a var statement with a function value

```javascript
function foo() {}
```

expands to

```javascript
var foo = function foo() {}
```

expands to

```javascript
var foo = undefined;
foo = function foo() {}
```

- function statement is when function word is defined otherwise is a function expression (e.g. inside another function)
- For return statement if there is no expression, then the return value is undefined.
- Except for constructors, whose default return value is this.
- It has a special parameter called arguments, it is array-like object. Treat as read-only structure.
- arguments.calee is the function itself in case of constructor

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

### Default Arguments
You can define default arguments: if you want to trigger one default argument pass `undefined`.

## Destructuring
It allows us to extract data from an object or array.

```javascript
const person = {
  first: 'Simon',
  last: 'Vocella',
  country: 'Italy',
  city: 'Milan',
  twitter: '@simonvocella'
};
const { first, last, twitter } = person;
```

We can:

- rename one property using `const { twitter: tweet} = person;` and in this case we have a variable named `tweet`
- add default values using `const { facebook = 'unknown' } = person;`

We can destructuring array with:

```javascript
const details = ['Wes Bos', 123, 'wesbos.com'];
const [name, id, website] = details;
```

We can use destructuring in function:

```javascript
function tipCalc({ total = 100, tip = 0.15, tax = 0.13 }) {
  return total + (tip * total) + (tax * total);
}
const bill = tipCalc({ tip: 0.20, total: 200 });
```

In this case `bill` has tax `0.13` and we can specify parameters in any order.
If we want `const bill = tipCalc();` we need to declare in this way.

```javascript
function tipCalc({ total = 100, tip = 0.15, tax = 0.13 } = {}) {
  return total + (tip * total) + (tax * total);
}
```

In this case `bill` will be `128`.

## Looping
We can loop with:

```javascript

const cuts = ['Chuck', 'Brisket', 'Shank', 'Short Rib'];

// 1. normal way
for (let i = 0; i < cuts.length; i++) {
  console.log(cuts[i]);
}

// 2. for each and anonymous function
cuts.forEach((cut) => {
  console.log(cut);
  if(cut === 'Brisket') {
    continue;
  }
});

// 3. for in loop
for (const index in cuts) {
  console.log(cuts[index]);
}

// 4. for of loop
for (const cut of cuts) {
  console.log(cut);
}
```

- For the second case you can't use `break` or `continue`.
- For the third case it iterates *absolutely* through the array including properties or what we add to the prototype of Array. It is useful if you want to iterate through object properties. Another problem that there is no guarantee about the order of the iteration.
The fourth case works as normal `foreach`. If you want to iterate through object properties you should use `Object.keys` or `entries`.

## Operators

### Spread
In functions:

```javascript
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
console.log(f(...[1,2,3]))
```

In arrays:

```javascript
var parts = ["shoulders", "knees"];
var lyrics = ["head", ...parts, "and", "toes"];

console.log(lyrics)
```

### Rest
We can allow unlimited params to function by using the rest operator.
```javascript
function demo(part1, ...part2) {
  return {part1, part2}
}

console.log(demo(1,2,3,4,5,6))
```

## Promises
Promises are a library for asynchronous programming. Promises are a first class representation of a value that may be made available in the future. Promises are used in many existing JavaScript libraries.

```JavaScript
function timeout(duration = 0) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, duration);
    })
}

var p = timeout(1000).then(() => {
    return timeout(2000);
}).then(() => {
    throw new Error("hmm");
}).catch(err => {
    return Promise.all([timeout(100), timeout(200)]);
})
```

### Quick Promise

```javascript

var p1 = Promise.resolve("1")
var p2 = Promise.reject("2")

Promise.race([p1, p2]).then((res) => {
   console.log(res)
})
```

### Fail fast
If a promise fails, `all` and `race` will reject as well.

```javascript
var p1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("1"), 1001)
})
var p2 = new Promise((resolve, reject) => {
  setTimeout(() => reject("2"), 1)
})

Promise.race([p1, p2]).then((res) => {
   console.log("success" + res)
}, res => {
   console.log("error " + res)
})

Promise.all([p1, p2]).then((res) => {
   console.log("success" + res)
}, res => {
   console.log("error " + res)
})
```

## Strict mode
ECMAScript 5's strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode isn't just a subset: it intentionally has different semantics from normal code. Browsers not supporting strict mode will run strict mode code with different behavior from browsers that do, so don't rely on strict mode without feature-testing for support for the relevant aspects of strict mode. Strict mode code and non-strict mode code can coexist, so scripts can opt into strict mode incrementally.
- No more implied global variables within a function
- this is not bound to global object in function form
- apply and call do not default to global object
- No with statement
- Setting writeble: false a property will throw
- Delete a configurable: false will throw
- Restrinctions on eval
- eval and arguments are reserved
- arguments not linked to parameters
- No more arguments.caller or arguments.callee
- No more octal literal
- Duplicate names in object literals are syntax errors
- Forgetting to use the new operator will throw an exception, instead to be attached silently on the global object
- No more is implicity attached to the global object (the default one will be undefined)

## Immediately-invoked function expression (IIFE)
An immediately-invoked function expression is a pattern which produces a lexical scope using JavaScript's function scoping. Immediately-invoked function expressions can be used to avoid variable hoisting from within blocks, protect against polluting the global environment and simultaneously allow public access to methods while retaining privacy for variables defined within the function.

## this
- The this parameter contains a reference to the object of invocation.
- this allows a method to know what object it is concerned with.
- this allows a single function object to service many functions.
- this is key to prototypal inheritance.
The this variable is attached to functions. Whenever you invoke a function, this is given a certain value, depending on how you invoke the function. This is often called the invocation pattern.

## Timing events
`var myTimeoutID = setTimeout(func, X)` call a function after X milliseconds.
`clearTimeout(myTimeoutID)` can clear the timeout function before it is called.
`var myIntervalID = setInterval(func, X)` call a function every X milliseconds.
`clearInterval(myIntervalID)` can clear the interval function before it is called.

## Literals
- Array -> []
- Object -> {}
- Boolean -> true, false
- Integer -> 1, 2, etc..
- Floating point -> 1.3, -3.1E+12 etc..
- Regexp literal -> /ab+c/
- String literal -> "hello"

## throw statement
```javascript
throw 'Error2';   // String type
throw 42;         // Number type
throw true;       // Boolean type
throw {toString: function() { return "I'm an object!"; } };
```

## try/catch statement
```javascript
openMyFile();
try {
  writeMyFile(theData); //This may throw a error
} catch(e) {  
  handleError(e); // If we got a error we handle it
} finally {
  closeMyFile(); // always close the resource
}
```

## Regexp
Regular expressions are patterns used to match character combinations in strings. In JavaScript, regular expressions are also objects. These patterns are used with the exec and test methods of RegExp, and with the match, replace, search, and split methods of String.

More info:
- http://benalman.com/news/2012/09/partial-application-in-javascript/
- https://johnresig.com/apps/learn
