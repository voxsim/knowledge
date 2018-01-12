# Encapsulation
Encapsulation means ensures that the behavior of an object can only be affected through its API. It lets us control how much a change to one object will impact other parts of the system by ensuring that there are no unexpected dependencies between unrelated components.

And It's different from [Information Hiding](https://github.com/voxsim/knowledge/blob/master/software-engineer/information-hiding.md)

Many object-oriented languages support encapsulation by providing control over the visibility of an object’s features to other objects, but that’s not enough. Objects can break encapsulation by sharing references to mutable objects, an effect known as aliasing. Aliasing is essential for conventional object-oriented systems (otherwise no two objects would be able to communicate), but accidental aliasing can couple unrelated parts of a system so it behaves mysteriously and is inflexible to change.

We follow standard practices to maintain encapsulation when coding: define immutable value types, avoid global variables and singletons, copy collections and mutable values when passing them between objects, and so on. 
