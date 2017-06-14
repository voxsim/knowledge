### Object

#### Prototype
- Every JavaScript object has a prototype.
- The prototype is also an object
- All JavaScript objects inherit their properties and methods from their prototype
- The standard way to create an object prototype is to use an object constructor function
- With a constructor function, you can use the new keyword to create new objects from the same prototype
- `Object.getPrototypeOf` returns the prototype of an object
- `Object.create(prototype)` creates an object with prototype `prototype`, if it is null it doesn't have a prototype
- `hasOwnProperty` check if an object has a property and not his ancestors

##### Class Inheritance
instances inherit from classes (like a blueprint — a description of the class), and create sub-class relationships: hierarchical class taxonomies. Instances are typically instantiated via constructor functions with the `new` keyword. Class inheritance may or may not use the `class` keyword from ES6.

##### Prototypal Inheritance
instances inherit directly from other objects. Instances are typically instantiated via factory functions or `Object.create()`. Instances may be composed from many different objects, allowing for easy selective inheritance.

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

#### Property Lookup
When accessing the properties of an object, JavaScript will traverse the prototype chain upwards until it finds a property with the requested name.
If it reaches the top of the chain - namely Object.prototype - and still hasn't found the specified property, it will return the value undefined instead.

#### Performance

The lookup time for properties that are high up on the prototype chain can have a negative impact on performance, and this may be significant in code where performance is critical. Additionally, trying to access non-existent properties will always traverse the full prototype chain.

Also, when iterating over the properties of an object every property that is on the prototype chain will be enumerated.

#### Extension of Native Prototypes

One mis-feature that is often used is to extend Object.prototype or one of the other built in prototypes.

This technique is called monkey patching and breaks encapsulation. While used by popular frameworks such as Prototype, there is still no good reason for cluttering built-in types with additional non-standard functionality.

The only good reason for extending a built-in prototype is to backport the features of newer JavaScript engines; for example, Array.forEach.

#### hasOwnProperty
To check whether an object has a property defined on itself and not somewhere on its prototype chain, it is necessary to use the hasOwnProperty method which all objects inherit from Object.prototype.

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
