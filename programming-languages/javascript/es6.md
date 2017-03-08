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
- [let](#let)
- [const](#const)
- [iterators](#iterators)
- [generators](#generators)
- [unicode](#unicode)
- [modules](#modules)
- [module loaders](#module-loaders)
- [map + set + weakmap + weakset](#map--set--weakmap--weakset)
- [proxies](#proxies)
- [symbols](#symbols)
- [subclassable built-ins](#subclassable-built-ins)
- [promises](#promises)
- [math + number + string + array + object APIs](#math--number--string--array--object-apis)
- [binary and octal literals](#binary-and-octal-literals)
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
