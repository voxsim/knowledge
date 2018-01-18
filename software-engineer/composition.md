# Composition

A composition describes a relationship in which one object completely controls another object that has not an independent lifecycle.

We can compose objects and functions.

## Three Different Forms of Object Composition
* Aggregation When an object is formed from an enumerable collection of subobjects. In other words, an object which contains other objects. Each subobject retains its own reference identity, such that it could be destructured from the aggregation without information loss.
* Concatenation When an object is formed by adding new properties to an existing object. Properties can be concatenated one at a time or copied from existing objects, e.g., jQuery plugins are created by concatenating new methods to the jQuery delegate prototype, jQuery.fn.
* Delegation When an object forwards or delegates to another object. e.g., Ivan Sutherland’s Sketchpad (1962) included instances with references to “masters” which were delegated to for shared properties. Photoshop includes “smart objects” that serve as local proxies which delegate to an external resource. JavaScript’s prototypes are also delegates: Array instances forward built-in array method calls to Array.prototype, objects to Object.prototype, etc...
