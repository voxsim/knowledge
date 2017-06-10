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

### this
- The this parameter contains a reference to the object of invocation.
- this allows a method to know what object it is concerned with.
- this allows a single function object to service many functions.
- this is key to prototypal inheritance.
The this variable is attached to functions. Whenever you invoke a function, this is given a certain value, depending on how you invoke the function. This is often called the invocation pattern.
