# Python

## Token

### Identifiers
- Starts with a letter or _
- in v2, A to Z or a to z are allowed
- in v3, other characters that Unicode classifies as letters are also allowed
- Punctuation characters such as @, $, and ! are not allowed
- By convention all variables starts with lowercase letter
- By convention class name starts with uppercase letter
- By convention starting with _ should be reserved for private identifier
- By convention starting with __ should be reserved for strongly private identifiere
- By convention if the identifier starts and ends with __ this means that the identifier is a language-defined special name

### Keyword
- `True` and `False` are keyword for boolean
- `None` is keyword for null
- `and`, `or` and `not` are the logical operators
- `as` is used to create an alias while importing a module
- `assert` is used for debugging
- `for` and `while` looping
- `break`, `continue` are used inside `for` and `while` loops to alter their normal behavior
- `class` for user-defined object
- `def` is used to define a user-defined function. Use `return` to return value.
- `del` is used to delete the reference to an object
- `if`, `else`, `elif` are used for conditional branching or decision making
- `except`, `raise`, `try` are used with exceptions
- `finally` is used with `try`…`except` block to close up resources or file streams
- `import` keyword is used to import modules into the current namespace
- `from`…`import` is used to import specific attributes or functions into the current namespace
- `in` is used to test if a sequence (list, tuple, string etc.) contains a value
- `is` is used for object identity
- `lambda` is used to create an anonymous function, it has inline `return` statement.
- `pass` is a null statement. Nothing happens when it is executed
- `with` statement is used to wrap the execution of a block of code within methods defined by the context manager
- `yield` is used inside a function like a return statement. But yield returns a generator
- `async`, `await` for asynchronous tasks

### Literals

## Statement
- Simple statement
- Compound statement









## Execution context
TODO

## Scoping
TODO

## Name Resolution Order
All scopes in JavaScript, including the global scope, have the special name this, defined in them, which refers to the current object.

Function scopes also have the name arguments, defined in them, which contains the arguments that were passed to the function.

For example, when trying to access a variable named foo inside the scope of a function, JavaScript will look up the name in the following order:
- If the function itself is called foo, use that.
- In case there is a var foo statement in the current scope and it is initialized, use that.
- If one of the function parameters is named foo, use that.
- In case there is a var foo statement in the current scope and it is not initialized, use that.
- Go to the next outer scope, and start with #1 again.

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

### Symbol
Symbols allow for private(ish) properties on objects. Before ECMAScript 6 all properties for an object could be accessed through for in, since symbols are not enumerable they cannot be accessed in this way. However, the symbolised properties are not truly private since they can be accessed directly. Symbols are immutable and unique.

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

- in foreach you can't use `break` or `continue`
- for in loops over enumerable property names of an object. It iterates *absolutely* through the array including properties or what we add to the prototype of Array. It is useful if you want to iterate through object properties. Another problem that there is no guarantee about the order of the iteration.
- for of (new in ES6) uses the object-specific iterator and loop over the values generated by that.

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

## Error Handling

### throw statement
```javascript
throw 'Error2';   // String type
throw 42;         // Number type
throw true;       // Boolean type
throw {toString: function() { return "I'm an object!"; } };
throw new Error('I am an error')
```

### try/catch statement
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

## undefined and null
JavaScript has two distinct values for nothing, null and undefined, with the latter being more useful.

### The Value undefined

undefined is a type with exactly one value: undefined.

The language also defines a global variable that has the value of undefined; this variable is also called undefined. However, this variable is neither a constant nor a keyword of the language. This means that its value can be easily overwritten.

ES5 Note: undefined in ECMAScript 5 is no longer writable in strict mode, but its name can still be shadowed by for example a function with the name undefined.
Here are some examples of when the value undefined is returned:
- Accessing the (unmodified) global variable undefined.
- Accessing a declared but not yet initialized variable.
- Implicit returns of functions due to missing return statements.
- return statements that do not explicitly return anything.
- Lookups of non-existent properties.
- Function parameters that do not have any explicit value passed.
- Anything that has been set to the value of undefined.
- Any expression in the form of void(expression)
- Handling Changes to the Value of undefined

Since the global variable undefined only holds a copy of the actual value of undefined, assigning a new value to it does not change the value of the type undefined.

Still, in order to compare something against the value of undefined, it is necessary to retrieve the value of undefined first.

To protect code against a possible overwritten undefined variable, a common technique used is to add an additional parameter to an anonymous wrapper that gets no argument passed to it.

```javascript
var undefined = 123;
(function(something, foo, undefined) {
    // undefined in the local scope does 
    // now again refer to the value `undefined`

})('Hello World', 42);
```

Another way to achieve the same effect would be to use a declaration inside the wrapper.

```javascript
var undefined = 123;
(function(something, foo) {
    var undefined;
    ...

})('Hello World', 42);
```

The only difference here is that this version results in 4 more bytes being used in case it is minified, and there is no other var statement inside the anonymous wrapper.

### Uses of null

While undefined in the context of the JavaScript language is mostly used in the sense of a traditional null, the actual null (both a literal and a type) is more or less just another data type.

It is used in some JavaScript internals (like declaring the end of the prototype chain by setting Foo.prototype = null), but in almost all cases, it can be replaced by undefined.

## Automatic Semicolon Insertion

Although JavaScript has C style syntax, it does not enforce the use of semicolons in the source code, so it is possible to omit them.

JavaScript is not a semicolon-less language. In fact, it needs the semicolons in order to understand the source code. Therefore, the JavaScript parser automatically inserts them whenever it encounters a parse error due to a missing semicolon.

```javascript
var foo = function() {
} // parse error, semicolon expected
test()
```

Insertion happens, and the parser tries again.

```javascript
var foo = function() {
}; // no error, parser continues
test()
```

The automatic insertion of semicolon is considered to be one of biggest design flaws in the language because it can change the behavior of code.

### How it Works

The code below has no semicolons in it, so it is up to the parser to decide where to insert them.

```javascript
(function(window, undefined) {
    function test(options) {
        log('testing!')

        (options.list || []).forEach(function(i) {

        })

        options.value.test(
            'long string to pass here',
            'and another long string to pass'
        )

        return
        {
            foo: function() {}
        }
    }
    window.test = test

})(window)

(function(window) {
    window.someLibrary = {}

})(window)
```

Below is the result of the parser's "guessing" game.

```javascript
(function(window, undefined) {
    function test(options) {

        // Not inserted, lines got merged
        log('testing!')(options.list || []).forEach(function(i) {

        }); // <- inserted

        options.value.test(
            'long string to pass here',
            'and another long string to pass'
        ); // <- inserted

        return; // <- inserted, breaks the return statement
        { // treated as a block

            // a label and a single expression statement
            foo: function() {} 
        }; // <- inserted
    }
    window.test = test; // <- inserted

// The lines got merged again
})(window)(function(window) {
    window.someLibrary = {}; // <- inserted

})(window); //<- inserted
```

The parser drastically changed the behavior of the code above. In certain cases, it does the wrong thing.
Note: The JavaScript parser does not "correctly" handle return statements that are followed by a new line. While this is not necessarily the fault of the automatic semicolon insertion, it can still be an unwanted side-effect.

### Leading Parenthesis

In case of a leading parenthesis, the parser will not insert a semicolon.

```javascript
log('testing!')
(options.list || []).forEach(function(i) {})
```

This code gets transformed into one line.

```javascript
log('testing!')(options.list || []).forEach(function(i) {})
```

Chances are very high that log does not return a function; therefore, the above will yield a TypeError stating that undefined is not a function.

## The delete Operator

In short, it's impossible to delete global variables, functions and some other stuff in JavaScript which have a DontDelete attribute set.

### Global code and Function code

When a variable or a function is defined in a global or a function scope it is a property of either the Activation object or the Global object. Such properties have a set of attributes, one of which is DontDelete. Variable and function declarations in global and function code always create properties with DontDelete, and therefore cannot be deleted.

```javascript
// global variable:
var a = 1; // DontDelete is set
delete a; // false
a; // 1

// normal function:
function f() {} // DontDelete is set
delete f; // false
typeof f; // "function"

// reassigning doesn't help:
f = 1;
delete f; // false
f; // 1
```

### Explicit properties

Explicitly set properties can be deleted normally.

```javascript
// explicitly set property:
var obj = {x: 1};
obj.y = 2;
delete obj.x; // true
delete obj.y; // true
obj.x; // undefined
obj.y; // undefined
In the example above, obj.x and obj.y can be deleted because they have no DontDelete attribute. That's why the example below works too.

// this works fine, except for IE:
var GLOBAL_OBJECT = this;
GLOBAL_OBJECT.a = 1;
a === GLOBAL_OBJECT.a; // true - just a global var
delete GLOBAL_OBJECT.a; // true
GLOBAL_OBJECT.a; // undefined
Here we use a trick to delete a. this here refers to the Global object and we explicitly declare variable a as its property which allows us to delete it.
```

IE (at least 6-8) has some bugs, so the code above doesn't work.

### Function arguments and built-ins

Functions' normal arguments, arguments objects and built-in properties also have DontDelete set.

```javascript
// function arguments and properties:
(function (x) {

  delete arguments; // false
  typeof arguments; // "object"

  delete x; // false
  x; // 1

  function f(){}
  delete f.length; // false
  typeof f.length; // "number"

})(1);
```

# Array

*   Array inherits from Object
*   Indexes are converted to strings and used as names for retrieving values
*   Very efficient for sparse array
*   Not very efficient in most of other cases
*   One advantage: No need to provide a length or type when creating an array
*   Literal form: []
*   It can contain any number of expressions separated by commas
*   New items can be appendend
*   The dot notation should be not used by arrays

sort myArray: -> it sorts alphabetically (everything number too, but we can pass a function in sort)

delete myArray[1]; -> it puts undefined in number 1 index; -> we need to use splice to delete the element and resize the array

## Array.from
`Array.from(arrayLike[, mapFn[, thisArg]])` method creates a new Array instance from an array-like or iterable object.

```javascript
const bar = ["a", "b", "c"];
Array.from(bar);
// ["a", "b", "c"]

Array.from('foo');
// ["f", "o", "o"]

// Using an arrow function as the map function to
// manipulate the elements
Array.from([1, 2, 3], x => x + x);      
// [2, 4, 6]


// Generate a sequence of numbers
// Since the array is initialized with `undefined` on each position,
// the value of `v` below will be `undefined`
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

## Array.isArray
The `Array.isArray(obj)` function determines whether the passed value is an Array

```javascript
// all following calls return true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
// Little known fact: Array.prototype itself is an array:
Array.isArray(Array.prototype); 

// all following calls return false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ __proto__: Array.prototype });
```

## Array.of
The `Array.of(element0[, element1[, ...[, elementN]]])` method creates a new Array instance with a variable number of arguments, regardless of number or type of the arguments.

## Array.prototype.concat
The concat() method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

## Array.prototype.entries
The entries() method returns a new Array Iterator object that contains the key/value pairs for each index in the array.

## Array.prototype.every / Array.prototype.some
The every() method tests whether all/some elements in the array pass the test implemented by the provided function

```javascript
function isBigEnough(element, index, array) { 
  return element >= 10; 
} 

[12, 5, 8, 130, 44].every(isBigEnough);   // false 
[12, 54, 18, 130, 44].every(isBigEnough); // true
```

## Array.prototype.filter
The `var newArray = arr.filter(callback[, thisArg])` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
var words = ["spray", "limit", "elite", "exuberant", "destruction", "present"];

var longWords = words.filter(function(word){
  return word.length > 6;
});

// Filtered array longWords is ["exuberant", "destruction", "present"]
```

## Array.prototype.map
The map() method creates a new array with the results of calling a provided function on every element in the calling array

```javascript
var numbers = [1, 5, 10, 15];
var doubles = numbers.map(function(x) {
   return x * 2;
});
// doubles is now [2, 10, 20, 30]
// numbers is still [1, 5, 10, 15]

var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots is now [1, 2, 3]
// numbers is still [1, 4, 9]
```

## Array.prototype.reduce
The reduce(accumulator(accumulator, currentValue, currentIndex)[, initialValue]) method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

```javascript
var total = [0, 1, 2, 3].reduce(function(sum, value) {
  return sum + value;
}, 0);
// total is 6

var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
  return a.concat(b);
}, []);
// flattened is [0, 1, 2, 3, 4, 5]
```

## Array.prototype.slice
The `slice([, start[, end]])`  method returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included). The original array will not be modified.

# What is asynchronous programming, and why is it important in JavaScript?
Javascript has one single thread and one single call stack -> It can do one thing at a time.

Synchronous programming means that, barring conditionals and function calls, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.

Asynchronous programming means that the engine runs in an event loop. When a blocking operation is needed, the request is started, and the code keeps running without blocking for the result. When the response is ready, an interrupt is fired, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations.

User interfaces are asynchronous by nature, and spend most of their time waiting for user input to interrupt the event loop and trigger event handlers.

Node is asynchronous by default, meaning that the server works in much the same way, waiting in a loop for a network request, and accepting more incoming requests while the first one is being handled.
This is important in JavaScript, because it is a very natural fit for user interface code, and very beneficial to performance on the server.

# ECMAScript 6

## Introduction
ECMAScript 6, also known as ECMAScript 2015, is the latest version of the ECMAScript standard. ES6 is a significant update to the language, and the first update to the language since ES5 was standardized in 2009.

See the [ES6 standard](http://www.ecma-international.org/ecma-262/6.0/) for full specification of the ECMAScript 6 language.

ES6 includes the following new features:
- [arrows](#arrows)
- [classes](#classes)
- [enhanced object literals](#enhanced-object-literals)
- [template strings](#template-strings)
- [destructuring](#destructuring)
- [default](#default)
- [spread](#spread)
- [spread + Object Literals](#spread--object-literals)
- [rest](#rest)
- [let](#let)
- [const](#const)
- [for..of](#forof)
- [iterators](#iterators)
- [generators](#generators)
- [unicode](#unicode)
- [Modules & Module Loaders](#modules--module-loaders)
- [map + set + weakmap + weakset](#map--set--weakmap--weakset)
- [proxies](#proxies)
- [symbols](#symbols)
- [subclassable built-ins](#subclassable-built-ins)
- [promises](#promises)
- [new libraries(math + number + string + array + object APIs)](#new-libraries-math--number--string--array--object-apis)
- [binary and octal literals](#binary-and-octal-literals)
- [promises](#promises)
- [reflect api](#reflect-api)
- [tail calls](#tail-calls)

## ECMAScript 6 Features

### Arrows
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

### Classes
ES6 classes are a simple sugar over the prototype-based OO pattern.  Having a single convenient declarative form makes class patterns easier to use, and encourages interoperability.  Classes support prototype-based inheritance, super calls, instance and static methods and constructors.

```JavaScript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //...
    super.update();
  }
  get boneCount() {
    return this.bones.length;
  }
  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```

### Enhanced Object Literals
Object literals are extended to support setting the prototype at construction, shorthand for `foo: foo` assignments, defining methods, making super calls, and computing property names with expressions.  Together, these also bring object literals and class declarations closer together, and let object-based design benefit from some of the same conveniences.

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

### Template Strings
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

## Destructuring

Array can be destructured.
```javascript
// list "matching"
var [a, , b] = [1,2,3];
console.log(a)
console.log(b)
```

Objects can be destructured as well.

```javascript
nodes = () => { return {op: "a", lhs: "b", rhs: "c"}}
var { op: a, lhs: b , rhs: c } = nodes()
console.log(a)
console.log(b)
console.log(c)
```

Using Shorthand notation.

 ```javascript
nodes = () => { return {lhs: "a", op: "b", rhs: "c"}}

// binds `op`, `lhs` and `rhs` in scope
var {op, lhs, rhs} = nodes()

console.log(op)
console.log(lhs)
console.log(rhs)
```

Can be used in parameter position

 ```javascript

function g({name: x}) {
  return x
}

function m({name}) {
  return name
}

console.log(g({name: 5}))
console.log(m({name: 5}))
```

Fail-soft destructuring

```javascript
var [a] = []
var [b = 1] = []
var c = [];
console.log(a)
console.log(b);
console.log(c);
```

## Default
```javascript
function f(x, y=12) {
  return x + y;
}

console.log(f(3))
```

## Spread

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

## Spread + Object Literals

We can do cool stuff with this in object creations.

```javascript
no-eval
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1
console.log(y); // 2
console.log(z); // { a: 3, b: 4 }

// Spread properties
let n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 }
console.log(obj)
```

Sadly it is not supported yet:

`npm install --save-dev babel-plugin-transform-object-rest-spread`

## Rest
We can allow unlimited params to function by using the rest operator.
```javascript
function demo(part1, ...part2) {
  // part2 is an array
  return {part1, part2}
}

console.log(demo(1,2,3,4,5,6))
```

## Let
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

## Const
- it is read only variable. I. e. you can't update it.
- it is block scoped
- you can't redeclare a variable with the same name in the same scope
- if you define an object you can still update its attribute. In case you want something immutable you can use`Object.freeze`
- If you use the variable before its definition you will get a not defined error. This is called temporal dead zone.

## For..of
New type of iterator, an alternative to `for..in`. It returns the values instead of the `keys`.

```javascript
let list = [4, 5, 6];

console.log(list)

for (let i in list) {
   console.log(i);
}
```

```javascript
let list = [4, 5, 6];

console.log(list)


for (let i of list) {
   console.log(i);
}
```

### Iterators
The iterator is a more dynamic type than an array.

```javascript
let infinite = {
  [Symbol.iterator]() {
    let c = 0;
    return {
      next() {
        c++;
        return { done: false, value: c }
      }
    }
  }
}

console.log("start");

for (var n of infinite) {
  // truncate the sequence at 1000
  if (n > 10)
    break;
  console.log(n);
}
```

### Generators
Generators simplify iterator-authoring using `function*` and `yield`.  A function declared as function* returns a Generator instance.  Generators are subtypes of iterators which include additional  `next` and `throw`.  These enable values to flow back into the generator, so `yield` is an expression form which returns a value (or throws).

Note: Can also be used to enable ‘await’-like async programming, see also ES7 `await` proposal.

```JavaScript
var fibonacci = {
  [Symbol.iterator]: function*() {
    var pre = 0, cur = 1;
    for (;;) {
      var temp = pre;
      pre = cur;
      cur += temp;
      yield cur;
    }
  }
}

for (var n of fibonacci) {
  // truncate the sequence at 1000
  if (n > 1000)
    break;
  console.log(n);
}
```

### Unicode
Non-breaking additions to support full Unicode, including new Unicode literal form in strings and new RegExp `u` mode to handle code points, as well as new APIs to process strings at the 21bit code points level.  These additions support building global apps in JavaScript.

```JavaScript
// same as ES5.1
"𠮷".length == 2

// new RegExp behaviour, opt-in ‘u’
"𠮷".match(/./u)[0].length == 2

// new form
"\u{20BB7}"=="𠮷"=="\uD842\uDFB7"

// new String ops
"𠮷".codePointAt(0) == 0x20BB7

// for-of iterates code points
for(var c of "𠮷") {
  console.log(c);
}
```

## Modules & Module Loaders
Native support for modules.
Module loaders support:
- Dynamic loading
- State isolation
- Global namespace isolation
- Compilation hooks
- Nested virtualization

The default module loader can be configured, and new loaders can be constructed to evaluate and load code in isolated or constrained contexts.

```javascript
no-eval
import defaultMember from "module-name";
import * as name from "module-name";
import { member } from "module-name";
import { member as alias } from "module-name";
import { member1 , member2 } from "module-name";
import { member1 , member2 as alias2 , [...] } from "module-name";
import defaultMember, { member [ , [...] ] } from "module-name";
import defaultMember, * as name from "module-name";
import "module-name";

```

```javascript
no-eval
export { name1, name2, …, nameN };
export { variable1 as name1, variable2 as name2, …, nameN };
export let name1, name2, …, nameN; // also var
export let name1 = …, name2 = …, …, nameN; // also var, const

export expression;
export default expression;
export default function (…) { … } // also class, function*
export default function name1(…) { … } // also class, function*
export { name1 as default, … };

export * from …;
export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;

```

### Map + Set + WeakMap + WeakSet
Efficient data structures for common algorithms. WeakMap/WeakSet provides leak-free object-key’d side tables.

```JavaScript
// Sets
var s = new Set();
s.add("hello").add("goodbye").add("hello");
s.size === 2;
s.has("hello") === true;

// Maps
var m = new Map();
m.set("hello", 42);
m.set(s, 34);
m.get(s) == 34;

// Weak Maps
var wm = new WeakMap();
wm.set(s, { extra: 42 });
wm.size === undefined

// Weak Sets
var ws = new WeakSet();
ws.add({ data: 42 });
// Because the added object has no other references, it will not be held in the set
```

### Proxies
Proxies enable creation of objects with the full range of behaviors available to host objects.  Can be used for interception, object virtualization, logging/profiling, etc.

```JavaScript
// Proxying a normal object
var target = {};
var handler = {
  get: function (receiver, name) {
    return `Hello, ${name}!`;
  }
};

var p = new Proxy(target, handler);
p.world === 'Hello, world!';
```

```JavaScript
// Proxying a function object
var target = function () { return 'I am the target'; };
var handler = {
  apply: function (receiver, ...args) {
    return 'I am the proxy';
  }
};

var p = new Proxy(target, handler);
p() === 'I am the proxy';
```

There are traps available for all of the runtime-level meta-operations:

```JavaScript
var handler =
{
  get:...,
  set:...,
  has:...,
  deleteProperty:...,
  apply:...,
  construct:...,
  getOwnPropertyDescriptor:...,
  defineProperty:...,
  getPrototypeOf:...,
  setPrototypeOf:...,
  enumerate:...,
  ownKeys:...,
  preventExtensions:...,
  isExtensible:...
}
```

### Symbols
Symbols enable access control for object state.  Symbols allow properties to be keyed by either `string` (as in ES5) or `symbol`.  Symbols are a new primitive type. Optional `description` parameter used in debugging - but is not part of identity.  Symbols are unique (like gensym), but not private since they are exposed via reflection features like `Object.getOwnPropertySymbols`.


```JavaScript
var MyClass = (function() {

  // module scoped symbol
  var key = Symbol("key");

  function MyClass(privateData) {
    this[key] = privateData;
  }

  MyClass.prototype = {
    doStuff: function() {
      ... this[key] ...
    }
  };

  return MyClass;
})();

var c = new MyClass("hello")
c["key"] === undefined
```

### Subclassable Built-ins
In ES6, built-ins like `Array`, `Date` and DOM `Element`s can be subclassed.

Object construction for a function named `Ctor` now uses two-phases (both virtually dispatched):
- Call `Ctor[@@create]` to allocate the object, installing any special behavior
- Invoke constructor on new instance to initialize

The known `@@create` symbol is available via `Symbol.create`.  Built-ins now expose their `@@create` explicitly.

```JavaScript
// Pseudo-code of Array
class Array {
    constructor(...args) { /* ... */ }
    static [Symbol.create]() {
        // Install special [[DefineOwnProperty]]
        // to magically update 'length'
    }
}

// User code of Array subclass
class MyArray extends Array {
    constructor(...args) { super(...args); }
}

// Two-phase 'new':
// 1) Call @@create to allocate object
// 2) Invoke constructor on new instance
var arr = new MyArray();
arr[1] = 12;
arr.length == 2
```
It is not possible to override the getter function without using Proxies of arrays.

### New Libraries (Math + Number + String + Array + Object APIs)
Many new library additions, including core Math libraries, Array conversion helpers, String helpers, and Object.assign for copying.

```JavaScript
Number.EPSILON
Number.isInteger(Infinity) // false
Number.isNaN("NaN") // false

Math.acosh(3) // 1.762747174039086
Math.hypot(3, 4) // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

"abcde".includes("cd") // true
"abc".repeat(3) // "abcabcabc"

Array.from(document.querySelectorAll('*')) // Returns a real Array
Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
[0, 0, 0].fill(7, 1) // [0,7,7]
[1, 2, 3].find(x => x == 3) // 3
[1, 2, 3].findIndex(x => x == 2) // 1
[1, 2, 3, 4, 5].copyWithin(3, 0) // [1, 2, 3, 1, 2]
["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
["a", "b", "c"].keys() // iterator 0, 1, 2
["a", "b", "c"].values() // iterator "a", "b", "c"

Object.assign(Point, { origin: new Point(0,0) })
```

### Binary and Octal Literals
Two new numeric literal forms are added for binary (`b`) and octal (`o`).

```JavaScript
0b111110111 === 503 // true
0o767 === 503 // true
```

### Promises
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
Need a quick always resolved promise?

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

### Reflect API
Full reflection API exposing the runtime-level meta-operations on objects.  This is effectively the inverse of the Proxy API, and allows making calls corresponding to the same meta-operations as the proxy traps.  Especially useful for implementing proxies.

```JavaScript

var z = {w: "Super Hello"}
var y = {x: "hello", __proto__: z};

console.log(Reflect.getOwnPropertyDescriptor(y, "x"));
console.log(Reflect.has(y, "w"));
console.log(Reflect.ownKeys(y, "w"));

console.log(Reflect.has(y, "x"));
console.log(Reflect.deleteProperty(y,"x"))
console.log(Reflect.has(y, "x"));

```

### Tail Calls
Calls in tail-position are guaranteed to not grow the stack unboundedly.  Makes recursive algorithms safe in the face of unbounded inputs.

```JavaScript
function factorial(n, acc = 1) {
    'use strict';
    if (n <= 1) return acc;
    return factorial(n - 1, n * acc);
}

// Stack overflow in most implementations today,
// but safe on arbitrary inputs in ES6
factorial(100000)
```

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
- They are not hoisted
- Named function expression are useful if you want to refer to the current function inside the function body

### Function statement/declaration
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

- function statement is when function word is defined otherwise is a function expression
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

# Object

## Prototype
- Every JavaScript object has a prototype.
- The prototype is also an object
- All JavaScript objects inherit their properties and methods from their prototype
- The standard way to create an object prototype is to use an object constructor function
- With a constructor function, you can use the new keyword to create new objects from the same prototype
- `Object.getPrototypeOf` returns the prototype of an object
- `Object.create(prototype)` creates an object with prototype `prototype`, if it is null it doesn't have a prototype
- `hasOwnProperty` check if an object has a property and not his ancestors
- The `Object.assign(target, ...sources)` method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.
- `Object.defineProperty(obj, prop, descriptor)` defines a new property directly on an object, or modifies an existing property on an object, and returns the object.

### Class Inheritance
instances inherit from classes (like a blueprint — a description of the class), and create sub-class relationships: hierarchical class taxonomies. Instances are typically instantiated via constructor functions with the `new` keyword. Class inheritance may or may not use the `class` keyword from ES6.

### Prototypal Inheritance
instances inherit directly from other objects. Instances are typically instantiated via factory functions or `Object.create()`. Instances may be composed from many different objects, allowing for easy selective inheritance.

### When is prototypal inheritance an appropriate choice?
There is more than one type of prototypal inheritance:
- Delegation (i.e., the prototype chain).
- Concatenative (i.e. mixins, `Object.assign()`).
- Functional (Not to be confused with functional programming. A function used to create a closure for private state/encapsulation).
Each type of prototypal inheritance has its own set of use-cases, but all of them are equally useful in their ability to enable composition, which creates has-a or uses-a or can-do relationships as opposed to the is-a relationship created with class inheritance.

## Object literal
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

## Get, set and delete
- get
  object.name
  object[expression]

- set
  object.name = value
  object[expression] = value

- delete
  delete object.name
  delete object[expression]

## Properties
A property is a named collection of attribute
- value -> any Javascript value
- writeble -> boolean
- enumerable -> boolean
- configurable -> boolean
- get -> function() { ... return value }
- set -> function(value) { ... }

## New operator
```javascript
function new(func, arguments) {
  var that = Object.create(func.prototype),
      result = func.apply(that, arguments);
  return (typeof result === 'object' && result) || that;
}
```

## Reference
Objects can be passed as arguments to functions, and can be returned by functions
- Objects are passed by references
- Objects are not passed by value
The === operator compares object references, not values (true if only it is the same object)
Loosely typed: any of these can be stored in a variable, or passed as a parameter to any function, the language is not "untyped"

## Property Lookup
When accessing the properties of an object, JavaScript will traverse the prototype chain upwards until it finds a property with the requested name.
If it reaches the top of the chain - namely Object.prototype - and still hasn't found the specified property, it will return the value undefined instead.

## Performance
The lookup time for properties that are high up on the prototype chain can have a negative impact on performance, and this may be significant in code where performance is critical. Additionally, trying to access non-existent properties will always traverse the full prototype chain.
Also, when iterating over the properties of an object every property that is on the prototype chain will be enumerated.

## Extension of Native Prototypes
One mis-feature that is often used is to extend Object.prototype or one of the other built in prototypes.

This technique is called monkey patching and breaks encapsulation. While used by popular frameworks such as Prototype, there is still no good reason for cluttering built-in types with additional non-standard functionality.

The only good reason for extending a built-in prototype is to backport the features of newer JavaScript engines; for example, Array.forEach.

## defineProperty
This method allows precise addition to or modification of a property on an object. Normal property addition through assignment creates properties which show up during property enumeration (for...in loop or Object.keys method), whose values may be changed, and which may be deleted. This method allows these extra details to be changed from their defaults. By default, values added using Object.defineProperty() are immutable.

Property descriptors present in objects come in two main flavors: data descriptors and accessor descriptors. A data descriptor is a property that has a value, which may or may not be writable. An accessor descriptor is a property described by a getter-setter pair of functions. A descriptor must be one of these two flavors; it cannot be both.

Both data and accessor descriptors are objects. They share the following required keys:
- configurable: true if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object. Defaults to false.
- enumerable: true if and only if this property shows up during enumeration of the properties on the corresponding object. Defaults to false.

A data descriptor also has the following optional keys:
- value: The value associated with the property. Can be any valid JavaScript value (number, object, function, etc). Defaults to undefined.
- writable: true if and only if the value associated with the property may be changed with an assignment operator. Defaults to false.

An accessor descriptor also has the following optional keys:
- get: A function which serves as a getter for the property, or undefined if there is no getter. The function return will be used as the value of property. Defaults to undefined.
- set: A function which serves as a setter for the property, or undefined if there is no setter. The function will receive as only argument the new value being assigned to the property. Defaults to undefined.

## Object.assign
The `Object.assign(target, ...sources)` method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.

The Object.assign() method only copies enumerable and own properties from a source object to a target object. It uses [[Get]] on the source and [[Set]] on the target, so it will invoke getters and setters. Therefore it assigns properties versus just copying or defining new properties. This may make it unsuitable for merging new properties into a prototype if the merge sources contain getters. For copying property definitions, including their enumerability, into prototypes Object.getOwnPropertyDescriptor() and Object.defineProperty() should be used instead.

### Cloning an object
```javascript
var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```

### Merging objects
```javascript
var o1 = { a: 1 };
var o2 = { b: 2 };
var o3 = { c: 3 };

var obj = Object.assign(o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1);  // { a: 1, b: 2, c: 3 }, target object itself is changed.
```

## Object.create
The `Object.create(proto[, propertiesObject])` method creates a new object with the specified prototype object and properties.

```javascript
// Shape - superclass
function Shape() {
  this.x = 0;
  this.y = 0;
}

// superclass method
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};

// Rectangle - subclass
function Rectangle() {
  Shape.call(this); // call super constructor.
}

// subclass extends superclass
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;

var rect = new Rectangle();

console.log('Is rect an instance of Rectangle?',
  rect instanceof Rectangle); // true
console.log('Is rect an instance of Shape?',
  rect instanceof Shape); // true
rect.move(1, 1); // Outputs, 'Shape moved.'
```

## Object.defineProperty
The `Object.defineProperty(obj, prop, descriptor)` method defines a new property directly on an object, or modifies an existing property on an object, and returns the object.

## Object.entries
The `Object.entries(obj)` method returns an array of a given object's own enumerable property [key, value] pairs, in the same order as that provided by a for...in loop (the difference being that a for-in loop enumerates properties in the prototype chain as well).

## Object.freeze / Object.isFrozen
The `Object.freeze(obj)` method freezes an object: that is, prevents new properties from being added to it; prevents existing properties from being removed; and prevents existing properties, or their enumerability, configurability, or writability, from being changed, it also prevents the prototype from being changed.  The method returns the object in a frozen state.

## Object.getOwnPropertyDescriptor
The `Object.getOwnPropertyDescriptor(obj)` method returns a property descriptor for an own property (that is, one directly present on an object and not in the object's prototype chain) of a given object.

## Object.getPrototypeOf
The `Object.getPrototypeOf(obj)` method returns the prototype (i.e. the value of the internal [[Prototype]] property) of the specified object.

## Object.is
The `Object.is(value1, value2)` method determines whether two values are the same value: two values are the same if one of the following holds:
* both undefined
* both null
* both true or both false
* both strings of the same length with the same characters
* both the same object
* both numbers and
    * both +0
    * both -0
    * both NaN
    * or both non-zero and both not NaN and both have the same value

This is not the same as being equal according to the == operator. The == operator applies various coercions to both sides (if they are not the same Type) before testing for equality (resulting in such behavior as "" == false being true), but Object.is doesn't coerce either value.

This is also not the same as being equal according to the === operator. The === operator (and the == operator as well) treats the number values -0 and +0 as equal and treats Number.NaN as not equal to NaN.

## Object.isExtensible
The `Object.isExtensible(obj) method determines if an object is extensible (whether it can have new properties added to it).

```javascript
// New objects are extensible.
var empty = {};
Object.isExtensible(empty); // === true

// ...but that can be changed.
Object.preventExtensions(empty);
Object.isExtensible(empty); // === false

// Sealed objects are by definition non-extensible.
var sealed = Object.seal({});
Object.isExtensible(sealed); // === false

// Frozen objects are also by definition non-extensible.
var frozen = Object.freeze({});
Object.isExtensible(frozen); // === false
```

## Object.keys
The `Object.keys(obj)` method returns an array of a given object's own enumerable properties, in the same order as that provided by a for...in loop (the difference being that a for-in loop enumerates properties in the prototype chain as well).

```javascript
var arr = ['a', 'b', 'c'];
console.log(Object.keys(arr)); // console: ['0', '1', '2']

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); // console: ['0', '1', '2']

// array like object with random key ordering
var anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(anObj)); // ['2', '7', '100']

// getFoo is property which isn't enumerable
var myObj = Object.create({}, {
  getFoo: {
    value: function () { return this.foo; }
  } 
});
myObj.foo = 1;
console.log(Object.keys(myObj)); // console: ['foo']
```

## Object.seal / Object.isSealed
The `Object.seal(obj)` method seals an object, preventing new properties from being added to it and marking all existing properties as non-configurable. Values of present properties can still be changed as long as they are writable.

## Object.values
The `Object.values(obj)` method returns an array of a given object's own enumerable property values, in the same order as that provided by a for...in loop (the difference being that a for-in loop enumerates properties in the prototype chain as well).

Let's review the ES6 `Promise` API that we've already seen unfold in bits and pieces throughout this chapter.

**Note:** The following API is native only as of ES6, but there are specification-compliant polyfills (not just extended Promise libraries) which can define `Promise` and all its associated behavior so that you can use native Promises even in pre-ES6 browsers. One such polyfill is "Native Promise Only" (http://github.com/getify/native-promise-only), which I wrote!

### new Promise(..) Constructor

The *revealing constructor* `Promise(..)` must be used with `new`, and must be provided a function callback that is synchronously/immediately called. This function is passed two function callbacks that act as resolution capabilities for the promise. We commonly label these `resolve(..)` and `reject(..)`:

```js
var p = new Promise( function(resolve,reject){
	// `resolve(..)` to resolve/fulfill the promise
	// `reject(..)` to reject the promise
} );
```

`reject(..)` simply rejects the promise, but `resolve(..)` can either fulfill the promise or reject it, depending on what it's passed. If `resolve(..)` is passed an immediate, non-Promise, non-thenable value, then the promise is fulfilled with that value.

But if `resolve(..)` is passed a genuine Promise or thenable value, that value is unwrapped recursively, and whatever its final resolution/state is will be adopted by the promise.

### Promise.resolve(..) and Promise.reject(..)

A shortcut for creating an already-rejected Promise is `Promise.reject(..)`, so these two promises are equivalent:

```js
var p1 = new Promise( function(resolve,reject){
	reject( "Oops" );
} );

var p2 = Promise.reject( "Oops" );
```

`Promise.resolve(..)` is usually used to create an already-fulfilled Promise in a similar way to `Promise.reject(..)`. However, `Promise.resolve(..)` also unwraps thenable values (as discussed several times already). In that case, the Promise returned adopts the final resolution of the thenable you passed in, which could either be fulfillment or rejection:

```js
var fulfilledTh = {
	then: function(cb) { cb( 42 ); }
};
var rejectedTh = {
	then: function(cb,errCb) {
		errCb( "Oops" );
	}
};

var p1 = Promise.resolve( fulfilledTh );
var p2 = Promise.resolve( rejectedTh );

// `p1` will be a fulfilled promise
// `p2` will be a rejected promise
```

And remember, `Promise.resolve(..)` doesn't do anything if what you pass is already a genuine Promise; it just returns the value directly. So there's no overhead to calling `Promise.resolve(..)` on values that you don't know the nature of, if one happens to already be a genuine Promise.

### then(..) and catch(..)

Each Promise instance (**not** the `Promise` API namespace) has `then(..)` and `catch(..)` methods, which allow registering of fulfillment and rejection handlers for the Promise. Once the Promise is resolved, one or the other of these handlers will be called, but not both, and it will always be called asynchronously (see "Jobs" in Chapter 1).

`then(..)` takes one or two parameters, the first for the fulfillment callback, and the second for the rejection callback. If either is omitted or is otherwise passed as a non-function value, a default callback is substituted respectively. The default fulfillment callback simply passes the message along, while the default rejection callback simply rethrows (propagates) the error reason it receives.

`catch(..)` takes only the rejection callback as a parameter, and automatically substitutes the default fulfillment callback, as just discussed. In other words, it's equivalent to `then(null,..)`:

```js
p.then( fulfilled );

p.then( fulfilled, rejected );

p.catch( rejected ); // or `p.then( null, rejected )`
```

`then(..)` and `catch(..)` also create and return a new promise, which can be used to express Promise chain flow control. If the fulfillment or rejection callbacks have an exception thrown, the returned promise is rejected. If either callback returns an immediate, non-Promise, non-thenable value, that value is set as the fulfillment for the returned promise. If the fulfillment handler specifically returns a promise or thenable value, that value is unwrapped and becomes the resolution of the returned promise.

### Promise.all([ .. ]) and Promise.race([ .. ])

The static helpers `Promise.all([ .. ])` and `Promise.race([ .. ])` on the ES6 `Promise` API both create a Promise as their return value. The resolution of that promise is controlled entirely by the array of promises that you pass in.

For `Promise.all([ .. ])`, all the promises you pass in must fulfill for the returned promise to fulfill. If any promise is rejected, the main returned promise is immediately rejected, too (discarding the results of any of the other promises). For fulfillment, you receive an `array` of all the passed in promises' fulfillment values. For rejection, you receive just the first promise rejection reason value. This pattern is classically called a "gate": all must arrive before the gate opens.

For `Promise.race([ .. ])`, only the first promise to resolve (fulfillment or rejection) "wins," and whatever that resolution is becomes the resolution of the returned promise. This pattern is classically called a "latch": first one to open the latch gets through. Consider:

```js
var p1 = Promise.resolve( 42 );
var p2 = Promise.resolve( "Hello World" );
var p3 = Promise.reject( "Oops" );

Promise.race( [p1,p2,p3] )
.then( function(msg){
	console.log( msg );		// 42
} );

Promise.all( [p1,p2,p3] )
.catch( function(err){
	console.error( err );	// "Oops"
} );

Promise.all( [p1,p2] )
.then( function(msgs){
	console.log( msgs );	// [42,"Hello World"]
} );
```

**Warning:** Be careful! If an empty `array` is passed to `Promise.all([ .. ])`, it will fulfill immediately, but `Promise.race([ .. ])` will hang forever and never resolve.

The ES6 `Promise` API is pretty simple and straightforward. It's at least good enough to serve the most basic of async cases, and is a good place to start when rearranging your code from callback hell to something better.

But there's a whole lot of async sophistication that apps often demand which Promises themselves will be limited in addressing. In the next section, we'll dive into those limitations as motivations for the benefit of Promise libraries.

## Promise Limitations

Many of the details we'll discuss in this section have already been alluded to in this chapter, but we'll just make sure to review these limitations specifically.

### Sequence Error Handling

We covered Promise-flavored error handling in detail earlier in this chapter. The limitations of how Promises are designed -- how they chain, specifically -- creates a very easy pitfall where an error in a Promise chain can be silently ignored accidentally.

But there's something else to consider with Promise errors. Because a Promise chain is nothing more than its constituent Promises wired together, there's no entity to refer to the entire chain as a single *thing*, which means there's no external way to observe any errors that may occur.

If you construct a Promise chain that has no error handling in it, any error anywhere in the chain will propagate indefinitely down the chain, until observed (by registering a rejection handler at some step). So, in that specific case, having a reference to the *last* promise in the chain is enough (`p` in the following snippet), because you can register a rejection handler there, and it will be notified of any propagated errors:

```js
// `foo(..)`, `STEP2(..)` and `STEP3(..)` are
// all promise-aware utilities

var p = foo( 42 )
.then( STEP2 )
.then( STEP3 );
```

Although it may seem sneakily confusing, `p` here doesn't point to the first promise in the chain (the one from the `foo(42)` call), but instead from the last promise, the one that comes from the `then(STEP3)` call.

Also, no step in the promise chain is observably doing its own error handling. That means that you could then register a rejection error handler on `p`, and it would be notified if any errors occur anywhere in the chain:

```
p.catch( handleErrors );
```

But if any step of the chain in fact does its own error handling (perhaps hidden/abstracted away from what you can see), your `handleErrors(..)` won't be notified. This may be what you want -- it was, after all, a "handled rejection" -- but it also may *not* be what you want. The complete lack of ability to be notified (of "already handled" rejection errors) is a limitation that restricts capabilities in some use cases.

It's basically the same limitation that exists with a `try..catch` that can catch an exception and simply swallow it. So this isn't a limitation **unique to Promises**, but it *is* something we might wish to have a workaround for.

Unfortunately, many times there is no reference kept for the intermediate steps in a Promise-chain sequence, so without such references, you cannot attach error handlers to reliably observe the errors.

### Single Value

Promises by definition only have a single fulfillment value or a single rejection reason. In simple examples, this isn't that big of a deal, but in more sophisticated scenarios, you may find this limiting.

The typical advice is to construct a values wrapper (such as an `object` or `array`) to contain these multiple messages. This solution works, but it can be quite awkward and tedious to wrap and unwrap your messages with every single step of your Promise chain.

#### Splitting Values

Sometimes you can take this as a signal that you could/should decompose the problem into two or more Promises.

Imagine you have a utility `foo(..)` that produces two values (`x` and `y`) asynchronously:

```js
function getY(x) {
	return new Promise( function(resolve,reject){
		setTimeout( function(){
			resolve( (3 * x) - 1 );
		}, 100 );
	} );
}

function foo(bar,baz) {
	var x = bar * baz;

	return getY( x )
	.then( function(y){
		// wrap both values into container
		return [x,y];
	} );
}

foo( 10, 20 )
.then( function(msgs){
	var x = msgs[0];
	var y = msgs[1];

	console.log( x, y );	// 200 599
} );
```

First, let's rearrange what `foo(..)` returns so that we don't have to wrap `x` and `y` into a single `array` value to transport through one Promise. Instead, we can wrap each value into its own promise:

```js
function foo(bar,baz) {
	var x = bar * baz;

	// return both promises
	return [
		Promise.resolve( x ),
		getY( x )
	];
}

Promise.all(
	foo( 10, 20 )
)
.then( function(msgs){
	var x = msgs[0];
	var y = msgs[1];

	console.log( x, y );
} );
```

Is an `array` of promises really better than an `array` of values passed through a single promise? Syntactically, it's not much of an improvement.

But this approach more closely embraces the Promise design theory. It's now easier in the future to refactor to split the calculation of `x` and `y` into separate functions. It's cleaner and more flexible to let the calling code decide how to orchestrate the two promises -- using `Promise.all([ .. ])` here, but certainly not the only option -- rather than to abstract such details away inside of `foo(..)`.

#### Unwrap/Spread Arguments

The `var x = ..` and `var y = ..` assignments are still awkward overhead. We can employ some functional trickery (hat tip to Reginald Braithwaite, @raganwald on Twitter) in a helper utility:

```js
function spread(fn) {
	return Function.apply.bind( fn, null );
}

Promise.all(
	foo( 10, 20 )
)
.then(
	spread( function(x,y){
		console.log( x, y );	// 200 599
	} )
)
```

That's a bit nicer! Of course, you could inline the functional magic to avoid the extra helper:

```js
Promise.all(
	foo( 10, 20 )
)
.then( Function.apply.bind(
	function(x,y){
		console.log( x, y );	// 200 599
	},
	null
) );
```

These tricks may be neat, but ES6 has an even better answer for us: destructuring. The array destructuring assignment form looks like this:

```js
Promise.all(
	foo( 10, 20 )
)
.then( function(msgs){
	var [x,y] = msgs;

	console.log( x, y );	// 200 599
} );
```

But best of all, ES6 offers the array parameter destructuring form:

```js
Promise.all(
	foo( 10, 20 )
)
.then( function([x,y]){
	console.log( x, y );	// 200 599
} );
```

We've now embraced the one-value-per-Promise mantra, but kept our supporting boilerplate to a minimum!

**Note:** For more information on ES6 destructuring forms, see the *ES6 & Beyond* title of this series.

### Single Resolution

One of the most intrinsic behaviors of Promises is that a Promise can only be resolved once (fulfillment or rejection). For many async use cases, you're only retrieving a value once, so this works fine.

But there's also a lot of async cases that fit into a different model -- one that's more akin to events and/or streams of data. It's not clear on the surface how well Promises can fit into such use cases, if at all. Without a significant abstraction on top of Promises, they will completely fall short for handling multiple value resolution.

Imagine a scenario where you might want to fire off a sequence of async steps in response to a stimulus (like an event) that can in fact happen multiple times, like a button click.

This probably won't work the way you want:

```js
// `click(..)` binds the `"click"` event to a DOM element
// `request(..)` is the previously defined Promise-aware Ajax

var p = new Promise( function(resolve,reject){
	click( "#mybtn", resolve );
} );

p.then( function(evt){
	var btnID = evt.currentTarget.id;
	return request( "http://some.url.1/?id=" + btnID );
} )
.then( function(text){
	console.log( text );
} );
```

The behavior here only works if your application calls for the button to be clicked just once. If the button is clicked a second time, the `p` promise has already been resolved, so the second `resolve(..)` call would be ignored.

Instead, you'd probably need to invert the paradigm, creating a whole new Promise chain for each event firing:

```js
click( "#mybtn", function(evt){
	var btnID = evt.currentTarget.id;

	request( "http://some.url.1/?id=" + btnID )
	.then( function(text){
		console.log( text );
	} );
} );
```

This approach will *work* in that a whole new Promise sequence will be fired off for each `"click"` event on the button.

But beyond just the ugliness of having to define the entire Promise chain inside the event handler, this design in some respects violates the idea of separation of concerns/capabilities (SoC). You might very well want to define your event handler in a different place in your code from where you define the *response* to the event (the Promise chain). That's pretty awkward to do in this pattern, without helper mechanisms.

**Note:** Another way of articulating this limitation is that it'd be nice if we could construct some sort of "observable" that we can subscribe a Promise chain to. There are libraries that have created these abstractions (such as RxJS -- http://rxjs.codeplex.com/), but the abstractions can seem so heavy that you can't even see the nature of Promises anymore. Such heavy abstraction brings important questions to mind such as whether (sans Promises) these mechanisms are as *trustable* as Promises themselves have been designed to be. We'll revisit the "Observable" pattern in Appendix B.

### Inertia

One concrete barrier to starting to use Promises in your own code is all the code that currently exists which is not already Promise-aware. If you have lots of callback-based code, it's far easier to just keep coding in that same style.

"A code base in motion (with callbacks) will remain in motion (with callbacks) unless acted upon by a smart, Promises-aware developer."

Promises offer a different paradigm, and as such, the approach to the code can be anywhere from just a little different to, in some cases, radically different. You have to be intentional about it, because Promises will not just naturally shake out from the same ol' ways of doing code that have served you well thus far.

Consider a callback-based scenario like the following:

```js
function foo(x,y,cb) {
	ajax(
		"http://some.url.1/?x=" + x + "&y=" + y,
		cb
	);
}

foo( 11, 31, function(err,text) {
	if (err) {
		console.error( err );
	}
	else {
		console.log( text );
	}
} );
```

Is it immediately obvious what the first steps are to convert this callback-based code to Promise-aware code? Depends on your experience. The more practice you have with it, the more natural it will feel. But certainly, Promises don't just advertise on the label exactly how to do it -- there's no one-size-fits-all answer -- so the responsibility is up to you.

As we've covered before, we definitely need an Ajax utility that is Promise-aware instead of callback-based, which we could call `request(..)`. You can make your own, as we have already. But the overhead of having to manually define Promise-aware wrappers for every callback-based utility makes it less likely you'll choose to refactor to Promise-aware coding at all.

Promises offer no direct answer to that limitation. Most Promise libraries do offer a helper, however. But even without a library, imagine a helper like this:

```js
// polyfill-safe guard check
if (!Promise.wrap) {
	Promise.wrap = function(fn) {
		return function() {
			var args = [].slice.call( arguments );

			return new Promise( function(resolve,reject){
				fn.apply(
					null,
					args.concat( function(err,v){
						if (err) {
							reject( err );
						}
						else {
							resolve( v );
						}
					} )
				);
			} );
		};
	};
}
```

OK, that's more than just a tiny trivial utility. However, although it may look a bit intimidating, it's not as bad as you'd think. It takes a function that expects an error-first style callback as its last parameter, and returns a new one that automatically creates a Promise to return, and substitutes the callback for you, wired up to the Promise fulfillment/rejection.

Rather than waste too much time talking about *how* this `Promise.wrap(..)` helper works, let's just look at how we use it:

```js
var request = Promise.wrap( ajax );

request( "http://some.url.1/" )
.then( .. )
..
```

Wow, that was pretty easy!

`Promise.wrap(..)` does **not** produce a Promise. It produces a function that will produce Promises. In a sense, a Promise-producing function could be seen as a "Promise factory." I propose "promisory" as the name for such a thing ("Promise" + "factory").

The act of wrapping a callback-expecting function to be a Promise-aware function is sometimes referred to as "lifting" or "promisifying". But there doesn't seem to be a standard term for what to call the resultant function other than a "lifted function", so I like "promisory" better as I think it's more descriptive.

**Note:** Promisory isn't a made-up term. It's a real word, and its definition means to contain or convey a promise. That's exactly what these functions are doing, so it turns out to be a pretty perfect terminology match!

So, `Promise.wrap(ajax)` produces an `ajax(..)` promisory we call `request(..)`, and that promisory produces Promises for Ajax responses.

If all functions were already promisories, we wouldn't need to make them ourselves, so the extra step is a tad bit of a shame. But at least the wrapping pattern is (usually) repeatable so we can put it into a `Promise.wrap(..)` helper as shown to aid our promise coding.

So back to our earlier example, we need a promisory for both `ajax(..)` and `foo(..)`:

```js
// make a promisory for `ajax(..)`
var request = Promise.wrap( ajax );

// refactor `foo(..)`, but keep it externally
// callback-based for compatibility with other
// parts of the code for now -- only use
// `request(..)`'s promise internally.
function foo(x,y,cb) {
	request(
		"http://some.url.1/?x=" + x + "&y=" + y
	)
	.then(
		function fulfilled(text){
			cb( null, text );
		},
		cb
	);
}

// now, for this code's purposes, make a
// promisory for `foo(..)`
var betterFoo = Promise.wrap( foo );

// and use the promisory
betterFoo( 11, 31 )
.then(
	function fulfilled(text){
		console.log( text );
	},
	function rejected(err){
		console.error( err );
	}
);
```

Of course, while we're refactoring `foo(..)` to use our new `request(..)` promisory, we could just make `foo(..)` a promisory itself, instead of remaining callback-based and needing to make and use the subsequent `betterFoo(..)` promisory. This decision just depends on whether `foo(..)` needs to stay callback-based compatible with other parts of the code base or not.

Consider:

```js
// `foo(..)` is now also a promisory because it
// delegates to the `request(..)` promisory
function foo(x,y) {
	return request(
		"http://some.url.1/?x=" + x + "&y=" + y
	);
}

foo( 11, 31 )
.then( .. )
..
```

While ES6 Promises don't natively ship with helpers for such promisory wrapping, most libraries provide them, or you can make your own. Either way, this particular limitation of Promises is addressable without too much pain (certainly compared to the pain of callback hell!).

### Promise Uncancelable

Once you create a Promise and register a fulfillment and/or rejection handler for it, there's nothing external you can do to stop that progression if something else happens to make that task moot.

**Note:** Many Promise abstraction libraries provide facilities to cancel Promises, but this is a terrible idea! Many developers wish Promises had natively been designed with external cancelation capability, but the problem is that it would let one consumer/observer of a Promise affect some other consumer's ability to observe that same Promise. This violates the future-value's trustability (external immutability), but moreover is the embodiment of the "action at a distance" anti-pattern (http://en.wikipedia.org/wiki/Action_at_a_distance_%28computer_programming%29). Regardless of how useful it seems, it will actually lead you straight back into the same nightmares as callbacks.

Consider our Promise timeout scenario from earlier:

```js
var p = foo( 42 );

Promise.race( [
	p,
	timeoutPromise( 3000 )
] )
.then(
	doSomething,
	handleError
);

p.then( function(){
	// still happens even in the timeout case :(
} );
```

The "timeout" was external to the promise `p`, so `p` itself keeps going, which we probably don't want.

One option is to invasively define your resolution callbacks:

```js
var OK = true;

var p = foo( 42 );

Promise.race( [
	p,
	timeoutPromise( 3000 )
	.catch( function(err){
		OK = false;
		throw err;
	} )
] )
.then(
	doSomething,
	handleError
);

p.then( function(){
	if (OK) {
		// only happens if no timeout! :)
	}
} );
```

This is ugly. It works, but it's far from ideal. Generally, you should try to avoid such scenarios.

But if you can't, the ugliness of this solution should be a clue that *cancelation* is a functionality that belongs at a higher level of abstraction on top of Promises. I'd recommend you look to Promise abstraction libraries for assistance rather than hacking it yourself.

**Note:** My *asynquence* Promise abstraction library provides just such an abstraction and an `abort()` capability for the sequence, all of which will be discussed in Appendix A.

A single Promise is not really a flow-control mechanism (at least not in a very meaningful sense), which is exactly what *cancelation* refers to; that's why Promise cancelation would feel awkward.

By contrast, a chain of Promises taken collectively together -- what I like to call a "sequence" -- *is* a flow control expression, and thus it's appropriate for cancelation to be defined at that level of abstraction.

No individual Promise should be cancelable, but it's sensible for a *sequence* to be cancelable, because you don't pass around a sequence as a single immutable value like you do with a Promise.

### Promise Performance

This particular limitation is both simple and complex.

Comparing how many pieces are moving with a basic callback-based async task chain versus a Promise chain, it's clear Promises have a fair bit more going on, which means they are naturally at least a tiny bit slower. Think back to just the simple list of trust guarantees that Promises offer, as compared to the ad hoc solution code you'd have to layer on top of callbacks to achieve the same protections.

More work to do, more guards to protect, means that Promises *are* slower as compared to naked, untrustable callbacks. That much is obvious, and probably simple to wrap your brain around.

---
title: Promises
category: JavaScript
---

Based on the [Promise API reference][promise] (mozilla.org).
{:.brief-intro.center}

[promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

### Creating promises

```js
new Promise(function (ok, err) {
  doStuff(function () {
    if (success) { ok(); }
    else { err(); }
  });
})
```

### Consuming promises

```js
promise
  .then(okFn, errFn)
  .catch(errFn)
```

### Multiple promises

```js
var promises = [
  promise1(), promise2(), ...
]

// succeeds when all succeed
Promise.all(promises)
  .then(function (results) {
  });

// succeeds when one finishes first
Promise.race(promises)
  .then(function (result) {
  });
```

### Converting other promises

```js
return Promise.resolve("result");
return Promise.resolve(promise);
return Promise.resolve(thenable);

return Promise.reject("reason");

Promise.resolve($.get('http://google.com'))
.then(...)
```
