## Pure Functions
A pure function's return value is determined only by its input values (arguments) with no side effects. When given the same argument, the result will always be the same.

In summary:

Pure functions must take arguments.
The same input (arguments) will always produce the same output (return).
Pure functions rely only on local state and do not mutate external state.
Pure functions do not produce side effects.
Pure functions cannot call impure functions.

## Impure Functions
An impure function mutates state outside its scope. Any function that has side effects (see below) is impure. Procedural functions with no utilized return value are also impure.

## State
State refers to the information a program has access to and can operate on at a point in time. This includes data stored in memory as well as OS memory, input/output ports, database, etc. For example, the contents of variables in an application at any given instant are representative of the application's state.

## Stateful
Stateful programs, apps, or components store data in memory about the current state.

## Stateless
Stateless functions or components perform tasks as though running them for the first time, every time. This means they do not reference or utilize any information from earlier in their execution. Statelessness enables referential transparency.

## Immutable

If an object is immutable, its value cannot be modified after creation.

## Mutable

If an object is mutable, its value can be modified after creation.

## Higher-order Function
A higher-order function is a function that:
- accepts another function as an argument, or
- returns a function as a result.

To see:
- SICP
- The little schemer
- https://stackoverflow.com/questions/210835/what-is-referential-transparency/9859966#9859966
