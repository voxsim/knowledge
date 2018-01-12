# Object

Objects are instances of [Classes](https://github.com/voxsim/knowledge/blob/master/software-engineer/class.md)

Objects use mutable state to model their behavior over time. Two objects of the same type have separate identities even if they have exactly the same state now, because their states can diverge if they receive different messages in the future.

## Common communication pattern

We can benefit from this high-level, declarative approach only if our objects are designed to be easily pluggable.

In practice, this means that they follow common communication patterns and that the dependencies between them are made explicit.

A communication pattern is a set of rules that govern how a group of objects talk to each other: the roles they play, what messages they can send and when, and so on.

In languages like Java, we identify object roles with (abstract) interfaces, rather than (concrete) classes, although interfaces don’t define everything we need to say.
