Functional programming produces programs by composing mathematical functions and avoids shared state & mutable data. Lisp (specified in 1958) was among the first languages to support functional programming, and was heavily inspired by lambda calculus. Lisp and many Lisp family languages are still in common use today.

FP Pros: Using the functional paradigm, programmers avoid any shared state or side-effects, which eliminates bugs caused by multiple functions competing for the same resources. With features such as the availability of point-free style (aka tacit programming), functions tend to be radically simplified and easily recomposed for more generally reusable code compared to OOP.
FP also tends to favor declarative and denotational styles, which do not spell out step-by-step instructions for operations, but instead concentrate on what to do, letting the underlying functions take care of the how. This leaves tremendous latitude for refactoring and performance optimization, even allowing you to replace entire algorithms with more efficient ones with very little code change. (e.g., memoize, or use lazy evaluation in place of eager evaluation.)
Computation that makes use of pure functions is also easy to scale across multiple processors, or across distributed computing clusters without fear of threading resource conflicts, race conditions, etc…

FP Cons: Over exploitation of FP features such as point-free style and large compositions can potentially reduce readability because the resulting code is often more abstractly specified, more terse, and less concrete.
More people are familiar with OO and imperative programming than functional programming, so even common idioms in functional programming can be confusing to new team members.
FP has a much steeper learning curve than OOP because the broad popularity of OOP has allowed the language and learning materials of OOP to become more conversational, whereas the language of FP tends to be much more academic and formal. FP concepts are frequently written about using idioms and notations from lambda calculus, algebras, and category theory, all of which requires a prior knowledge foundation in those domains to be understood.

## Pure Functions
A pure function's return value is determined only by its input values (arguments) with no side effects. When given the same argument, the result will always be the same.

In summary:
- Pure functions must take arguments.
- The same input (arguments) will always produce the same output (return).
- Pure functions rely only on local state and do not mutate external state.
- Pure functions do not produce side effects.
- Pure functions cannot call impure functions.

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
- accepts another function as an argument
- returns a function as a result.

## Currying
A common technique in FP is currying. Currying is the process of converting a function that
takes multiple arguments into a function that takes one argument at a time, returning
another function.

Let's look at an example to clarify the concept.
Instead of writing:
```javascript
const add = (x, y) => x + y
```

We define the function like this:
```javascript
const add = x => y => x + y
```

And we use it in the following way:
```javascript
constadd1 = add(1)
add1(2) // 3
add1(3) // 4
```

This is a pretty convenient way of writing functions because since the first value is stored
after the application of the first parameter, we can reuse the second function multiple times.

## Composition
Functions can be combined to produce new functions with more advanced features.

To see:
- SICP
- The little schemer
- https://stackoverflow.com/questions/210835/what-is-referential-transparency/9859966#9859966
- https://github.com/MostlyAdequate/mostly-adequate-guide
- http://haskell.cs.yale.edu/wp-content/uploads/2015/03/HSoM.pdf
- https://github.com/stuartsierra/reducible-stream
