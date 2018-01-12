# Design software

When we grow our systems a slice of functionality at a time.
As the code scales up, the only way we can continue to understand and maintain it is by structuring the functionality into objects, objects into packages, 2 packages into programs, and programs into systems.

We use two principal heuristics to guide this structuring:
* [Separation of concerns](https://github.com/voxsim/knowledge/blob/master/software-engineer/separation-of-concerns.md)
* [Abstraction](https://github.com/voxsim/knowledge/blob/master/software-engineer/abstraction-principle.md)

Applied consistently we can achieve an [Hexagonal architecture](https://github.com/voxsim/knowledge/blob/master/software-engineer/hexagonal-architecture.md).

We design systems for maintainability, readability, testability, and comprehensibility.
